---
title: "Playing With TypeScript"
date: 2012-10-05T17:56:41+02:00
categories: [development]
tags: [javascript, free software, typescript]
draft: false
---

## Taking TypeScript out for a spin

[Microsoft](http://www.microsoft.com/) announced a new programming language by the name [TypeScript](http://www.typescriptlang.org/) this week. The driving philosophy behind the language is to extend JavaScript. Since I have done my shared of JavaScript programming - and given [talks](http://www.slideshare.net/geisshirt/javascript-11922069), [taught classes](http://www.opensourcedays.org/2012/node/18), and written articles and a [book](http://www.libris.dk/produkt/Introduktion_til_Javascript.htm) on the topic - I decided to take TypeScript out for a spin.

The language comes with a specification (97 pages) and a compiler. The compiler is compiling TypeScript to JavaScript. In this way, Microsoft can support virtually any platform in the world. The big trend at the moment is that JavaScript is used as a server-side programming language - [node.js](http://nodejs.org/) is popular. In my day-work, I have recently worked on an extension (in C++) for node.js for employer's database.

### Open Source

One of the interesting developments of TypeScript is that Microsoft has released everything as free or open source software. According to Microsoft, they are an operating systems company and not focusing on development tools. Today, developers are used to open source software, and in order to succeed within the developer community, you are forced to released under these terms.

The TypeScript compiler has a command-line interface. Basically, it is simply a node.js application. I have tested the compiler on my laptop which is currently running Fedora 17.

As an Emacs user, I am happy to see that Microsoft has released a TypeScript mode for Emacs. It is a simple mode as it primarily does syntax highlighting and indention. I have briefly looked at the elisp source code, and it seems to pretty well organized. If TypeScript becomes popular, I do hope that we will see a more advanced mode like [js2](http://code.google.com/p/js2-mode/).

### Classes and strongly typing

As you might know, JavaScript is an object-oriented programming language. But is does not have classes. Over the years, various techniques for encapsulating data and emulating classes have been developed. For example, you can use a function as constructor. TypeScript introduces classes, and it is possible to inherit from a class. This implies that common design patterns can probably be implemented easily in TypeScript.

JavaScript is a dynamical typed languages, and TypeScript brings strongly typing to JavaScript. You must declare variables - with associated types. It is possible for the TypeScript compiler to infer types in many cases, and an `any` type gives you the flexibility of weak typing.

### An example

I am fond of graph theory, and I have written a simple graph class in TypeScript. I implemented typological sorting in JavaScript a few years ago as a non-trivial example for a course I was teaching.

The TypeScript example uses two classes. The `MyNode` class is actually just a convenient way to store collection of data items. For a C programmer, it is just a `struct`. The `Graph` class is somewhat longer. As you can see, a TypeScript class has attributes, a constructor and methods. It is different from JavaScript where you do not have classes and objects do not have methods (but properties can be anonymous functions).

```typescript
class MyNode {
    id: string;
    visited: bool;
    edges: number[];
    payload: string;

    constructor(id : string, payload : string) {
        this.id = id;
        this.payload = payload;
        this.visited = false;
        this.edges = [];
    }
};
    

class Graph {
    name: string;
    nodes: MyNode[];
    
    constructor(name : string) {
        this.name = name;
        this.nodes = [];
    }

    find_node(id : string) : number {
        var i;
        var found;

        if (this.nodes.length == 0) {
            return -1;
        }

        i = 0;
        found = false;
        while (i<this.nodes.length) {
            if (this.nodes[i].id == id) {
                found = true;
            }
            if (found) {
                break;
            }
            i++;
        }
        if (found) {
            return i;
        } else {
            return -1;
        }
    }

    // add nodes - id is a unique string for identification
    add_node(id : string, payload : string) {
        if (this.find_node(id) < 0) {
            var edges = [];
            var n = new MyNode(id, payload);
            this.nodes.push(n);
        }
    }

    // add edge - work well for DAGs
    // if you don't work with DAGs, then use
    // add_edge(i, j) ; add_edge(j, i);
    add_edge(src : string, dst : string) {
        var n;
        var i = this.find_node(src);
        var j = this.find_node(dst);
        if (i>=0 && j>=0) {
            n = this.nodes[i].edges.push(j);
        }
    }

    // topological sorting - return array of IDs
    // see http://en.wikipedia.org/wiki/Topological_sort
    // (alternative algorithm)
    sort() : number[] {
        var i, j, m;
        var L = [], Lid = [];
        var that = this;

        for (i in this.nodes) {
            this.nodes[i].visited = false;
        }

        function _visit(n) {
            var j;
            if (!that.nodes[n].visited) {
                that.nodes[n].visited = true;
                for (j in that.nodes[n].edges) {
                    m = that.nodes[n].edges[j];
                    _visit(m);
                }
                L.push(n);
            }
        }
        for (i in this.nodes) {
            _visit(i);
        }

        for (i in L) {
            j = L[i];
            Lid.push(this.nodes[j].id);
        }
        return Lid;
    }
}

// Test case
var g = new Graph("Software");
g.add_node('Emacs', '23.1');
g.add_node('GTK',   '2.18.3');
g.add_node('Cairo', '1.8.8');
g.add_node('glib',  '2.22.3');
g.add_node('libc',  '2.10.1');
g.add_edge('Emacs', 'libc');
g.add_edge('Emacs', 'GTK');
g.add_edge('GTK',   'glib');
g.add_edge('GTK',   'Cairo');
g.add_edge('Cairo', 'libc');
g.add_edge('glib',  'libc');
var list = g.sort();
console.log('Topological sort: '+list.join('->'));
```

The TypeScript language is an interesting development as it offers (web) programmers a more mainstream approach. To be honest, when I have been teaching JavaScript for seasoned programmers, they have often been puzzled by the odd object system behind JavaScript. The scope rules of JavaScript are always regarded as being odd. I have not yet examined rules in TypeScript, but I hope to return to the topic in the near future.
