---
title: "Review - JavaScript Promises Essentials"
date: 2014-12-04T09:52:02+02:00
categories: [development, review]
tags: [javascript, web]
draft: false
---

## Review of JavaScript Promises Essentials

Promises are an old pattern in concurrent programming. In the computer science literature, promises date back to the papers by Friendman and Wise from mid 1970s. Many programming languages have promise - and futures as in Java are a similar idea. A promise is a variable or an object which value is initially unknown and is the result of another task. Modern JavaScript development is highly asynchronous by design: the UI (in the web browser) is updated by calls to the backend using HTTP requests.

JavaScript (ECMAScript to be correct) will soon have promises build into the core of the runtime environment, and promises already exist in many libraries and frameworks. If you haven’t worked with promises in a JavaScript context before, now is a good time to begin. In order to ease the use of promises in JavaScript development, the Promises/A+ standard has emerged.

The book is short and divided in six chapters. The first chapter is an introduction to the state of front-end JavaScript development in general and the asynchronous model in particular. The chapter sets the scene for the rest of the book, and discuss how promises fit well into JavaScript.

The second chapter is written in a very dense format using many bullet lists. You are probably going to read the chapter more than once to get all the information. The good news is that is a lot of information. Chapters 2-4 are a presentation of how to use promises, include error handling.

Chapter 5 is devoted to WinJS - the open source library for development of Windows 8 and Windows mobile applications in  JavaScript. Personally, I don’t develop for any of the Microsoft stacks, but the chapter is still useful as it shows how a widely used library is applying the promise concepts.

The final chapter explains how to implement your own promise library. I guess that there exist many in-house JavaScript libraries. If you have such a library, you will find this chapter useful.

In general, the book is well-written. The usage of bullet list many place (and chapter 2 in particular) can make it hard to read the book. Still, any JavaScript developer should read the book and get ready to the great promise of promises. You can find more information about the book [here](https://subscription.packtpub.com/search?query=javascript%20promises%20essentials).