---
title: "When Memmove Fails"
date: 2017-05-04T11:33:50+02:00
categories: [programming]
tags: [Android, Realm, bug]
draft: false
---

**This blog post was first published as [When memmove fails](https://academy.realm.io/posts/when-memmove-fails/)**

It was late October last year, and as we began preparations for Realmstravaganza — our annual all-hands gathering in Copenhagen — we started receiving bug reports with some serious native crashes. No one could have guessed just how deep of a rabbit hole we’d have to go down to find a fix. Before we were done, we’d be neck deep in compiler-level optimizations of fundamental C functions, looking for a smoking gun that wouldn’t even set off our unit tests.

For a while, we weren’t even sure what devices were affected, and so we couldn’t even reproduce the crashes [our users were sending us](https://github.com/realm/realm-java/issues/3651). But as early reports trickled in, it seemed that the crashes were limited to certain older Android devices — running Android 4.2 Jelly Bean and 4.4 Kit Kat. By now, both versions are unsupported, but that doesn’t mean they’re unused. [About 30%](https://developer.android.com/about/dashboards/index.html) of all Android devices are still running a pre-Lollipop version. We couldn’t slack on fixing this.

The popularity of older Android versions didn’t make finding a test device any easier. After a lot of searching and bartering, we dug up an end-of-life [Samsung Galaxy Tab 3 Lite (SM-T111)](http://www.gsmarena.com/samsung_galaxy_tab_3_lite_7_0_3g-5975.php). If there was a smoking gun in here somewhere, our Tab 3 would let us find it.

After all, the incoming comments on the original GitHub issue name this specific Samsung tablet as one of the devices which shows the mysterious native crashes. But even with the device, none of our unit tests failed. Only our example apps showed signs of this mysterious bug; combined with the stack traces reported by users, we thought it pointed to a bug in the way Realm Core [stores strings](https://github.com/realm/realm-core/blob/master/src/realm/array_string.cpp#L72).

Still, that would have been strange. The `ArrayString::set()` method is used very widely, so we had no reason to believe it contained a bug — especially a bug limited to such a narrow range of devices and Android versions. The next alternative wasn’t an appealing one: we had to look at the possibility that we were dealing with a native bug.

Really pesky native bugs tend to present themselves infrequently and only on certain hardware, and we were about to discover that we were facing one of the peskiest bugs around. Our challenge would be magnified because, until recently, the support for C++ and native debugging has been less than stellar.

Simply put: on the Android platform, native crashes can be hard to debug even when you know what you’re looking for.

It took us this long just to be able to reproduce the bug, but we weren’t anywhere close to uncovering its cause. We had to realize that the truth about this bug went much deeper than we’d hoped: we were looking at a bug on the device, not in our code.

But one day, a lucky breakthrough came from one of our users, and we found that other developers had faced the same bug. The culprit was right under our noses all along.

## From bug to understanding

With our trust Tab 3 in hand, and a sample app designed to trigger the native crashes that continued to elude our understanding, we felt closer than ever to a solution.

Our debugging app, [introExample](https://github.com/realm/realm-java/tree/master/examples/introExample), is extremely simple. It initializes Realm, create a Realm file with a couple of classes and inserts some objects. By using a non-stripped version of the native code, the crash from this app produced a stack trace which gave us an indication of what was going on:

```
frame #0: 0x5e61ea68 librealm-jni.so`realm::ArrayString::set(unsigned int, realm::StringData) + 176
frame #1: 0x5e640c1e librealm-jni.so`realm::Group::do_get_or_add_table(realm::StringData, bool (*)(realm::Spec const&), void (*)(realm::Table&), bool*) + 154
frame #2: 0x5e5f8570 librealm-jni.so`(anonymous namespace)::create_metadata_tables(realm::Group&) + 152
frame #3: 0x5e5f86a4 librealm-jni.so`realm::ObjectStore::set_schema_version(realm::Group&, unsigned long long) + 12
frame #4: 0x5e5bb50c librealm-jni.so`Java_io_realm_internal_SharedRealm_nativeSetVersion + 292
```

The `ArrayString::set()` method is taking care of storing strings within Realm Core. It has its share of pointer arithmetic and it has a few calls to standard library functions like `std::fill()` and i`std::copy_backward()`. Disassembling the object file of `ArrayString` shows that the crash happens when calling `memmove()` (at byte 176, the instruction after the call is found):


```
0x5faaf4c2 <+168>: mov    r0, r3
0x5faaf4c4 <+170>: mov    r1, r5
0x5faaf4c6 <+172>: blx    0x5f9e84cc                ; symbol stub for: memmove
0x5faaf4ca <+176>: mov    r3, r0
0x5faaf4cc <+178>: b      0x5faaf47e                ; <+100>
```

Could it really be that `memmove()` — a core C function handled by virtually every operating system — is the source of our bug?

Things got weirder. The `create_metadata_tables()` function in the above stack trace is only called when the Realm file is created. That is, it is only called once and before any objects have been inserted. The function is pretty simple: it creates two tables, adds a few columns to them and add search indices. We swapped the order of creating the tables, which exercised a different code path of `ArrayString::set()`, and that magically solved the issue. In most cases, exercising a different code path doesn’t really fix a bug; it only masks it. So even though it was likely only a [short term work-around](https://github.com/realm/realm-java/pull/4067), we were running out of options, and decided to release this fix in Realm Java 2.2.3 anyway.

Likewise, changing linker flags exercises another code path. But in uncovering what the linker flags changed, and unearthing a long-closed compiler-level issue, we’d discover the real bug.

## A trip down memory lane

The `memmove()` function - together with its cousins `memcpy()` and `bcopy()` - have been [available to UNIX programmers since 1990](https://github.com/dspinellis/unix-history-repo/commit/5fc4877aa0c5088a818786dda9b4b0bc1bac2ef6) as part of [4.3BSD-Reno](http://gunkies.org/wiki/4.3_BSD_Reno). The signature of the function is pretty simple:

```c
#include <string.h>

void *memmove(void *s1, const void *s2, size_t n);
```

The function copies bytes in memory — even if the source and the destination memory areas overlap. The `memcpy()` function is not able to cope with overlaps but is generally faster than `memmove()`.

Virtually every operating system implements a version of `memmove()` and `memcpy()` - either in the kernel or through the C standard library. The functions are often used as primitives to implement other functions. Examples from GNU C++ standard library are `std::copy()` and `std::copy_backward()` — both of which [call an implementation of `memmove()`](https://github.com/gcc-mirror/gcc/blob/master/libstdc%2B%2B-v3/include/bits/stl_algobase.h#L570). In order to have as good performance as possible, it is not uncommon to write optimized versions in assembler. Compilers often have [builtin implementations](https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html) too, and these builtins are inlined at some optimization levels.

In sum: `memmove()` is a very fundamental method, and it can be changed in many different ways that are all hard to introspect.

## Where there’s smoke, there’s fire

A major breakthrough in understanding the issue came from our user [diegomontoya](https://github.com/diegomontoya). [He had systematically built Realm Core](https://github.com/realm/realm-java/issues/3651#issuecomment-288350097) and Realm Java with different optimization flags. We typically use `-Os` which is extremely similar to `-O2`, but the space consuming optimizations are disabled. With optimization `-O1` flag, the bug seems to vanish.

By now, we’ve got a strong indication of an issue in `memmove()` or `memcpy()` in older versions of Android. That led us to a few similar bugs that other developers had documented. In his blog, [ChengYi He](https://github.com/chengyihe) has published a [thorough analysis](https://chengyihe.wordpress.com/2015/08/30/android-binder-arm-segmentation-at-ipcthreadstateexecutecommand-in-libbinder-so/) of a similar crash. Unfortunately, he did not have a solution. Furthermore, Unity has experienced [similar crashes](https://forum.unity3d.com/threads/2-5x-increase-in-crashes-from-samsung-devices-on-android-4-4-2.246258/) but without indicating a solution.

With the optimization flag fix in mind, we found a [closed issue](https://code.google.com/p/android/issues/detail?id=81692) reported by a Qt developer. In the original Qt bug, they found that `gcc` would swap the implementation of `memmove()`. By adding the `-fno-builtin-memmove` flag, they could switch from calling `gcc`’s builtin version of `memmove()` to the standard library version, and it solved their issue.

## Don’t Repeat Yourself

Unfortunately, trying `-fno-builtin-memmove` does not seem to fix the issue for us. Maybe we are going through yet another different code path? The solution, it turns out, was close at hand.

Taking a page from the Qt developer’s workaround, we decided to add our own version of `memmove()` and `memcpy()`. You can simply wrap `gcc`’s builtin functions by adding the flags `-Wl,--wrap,memmove` and `-Wl,--wrap,memcpyi`. Supply your own versions of them, and the calls to these functions will then be changed at linker time. [Our code](https://github.com/realm/realm-java/pull/4402) wraps both functions, and we also added a simple test from the [closed issue](https://code.google.com/p/android/issues/detail?id=81692) that the Qt developer filed with Android:

```c
char *array = strdup("Foobar");
void *ptr = memmove(array + 1, array, sizeof("Foobar") - 2);
assert(ptr == array + 1);
```

We use that test to see if `memmove()` works correctly. If it does, it is likely much faster than any implementation we can come up with. In that case, we just call the version found in the standard library. If `memmove()` does not work, we use our version.

Instead of rolling a brand new version of `memmove()`, we have reviewed existing implementations, which is an exercise in weighing both technical and legal considerations. A strict license can have dramatic consequences for our users, but an incorrect implementation means Realm becomes unusable. In the end, the [D.R.Y. Project](http://dryproject.org/) is our choice. The `libc11` library has easy-to-read implementations of `memcpy()` and `memmove()`, and the code is public domain.

## Conclusion

Developers like having flashy, new toys — so it’s pretty rare that you’ll have an end-of-life device in your pocket. That doesn’t mean your users don’t have them, and because Realm Java has been so broadly adopted, we’re likely to be used on all sort of devices. Even old ones, and even old ones with bugs. It is a great privilege to be able to serve so many devices, and the consequence is that we are likely to see extremely weird bugs — like specific devices with bugs in [signal handling](https://realm.io/news/realm-java-0.85.0/). We consider it part of our duty to not just serve our users by fixing these bugs, but to tell you about the process so that we all know what to look for in the future.

Moreover, we’re reminded of how hard it is to build great software. Even Samsung didn’t pick up on this device-specific bug in `memmove()`. And testing `memmove()` was only added to [CTS](https://source.android.com/compatibility/cts/) in Lollipop. Even if most bugs happen because of silly typos, it doesn’t mean that it’s impossible for there to be a failure point in compiler-level optimizations of fundamental C methods.

At Realm, we are lucky. We have users who give us detailed bug reports, and sometimes from devices we have never heard about. We are lucky to have users who try out unreleased patches on these devices. And we’re lucky to be able to see all the diversity of the mobile ecosystem, and to know that happens because our software matters to so many people. It’s a big responsibility, and we appreciate your trust in our platform. It’s what drives us to find and fix bugs like these, and to tell you about the mystery of a weird little bug on an old Samsung tablet.
