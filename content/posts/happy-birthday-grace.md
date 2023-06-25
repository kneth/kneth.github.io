---
title: "Happy Birthday, Grace"
date: 2013-12-10T12:52:46+02:00
categories: [development]
tags: [COBOL, free software, OpenCOBOL]
draft: false
---

## Happy birthday, Grace
Yesterday, [Grace Hopper](http://en.wikipedia.org/wiki/Grace_Hopper) would have turn 107 years old. She was one of the first computer scientists. She worked on compilers but she is probably best known for her development of [COBOL](http://en.wikipedia.org/wiki/COBOL). COBOL is one of the first high-level programming languages (FORTRAN is the other one). Back in the 1950s, computers were used as calculators, but COBOL and Grace Hopper shown us that computers can be used for much more that simple calculations. Today, COBOL is still wildly used.

As a tribute to Grace Hopper, I have played a bit with the [OpenCOBOL](http://opencobol.org/) compiler. OpenCOBOL can translate COBOL source code to C and use a C compiler to generate a real executable program. The compiler is licensed under GNU General Public License (version 3), and the runtime is licensed under GNU Lesser General Public License (version 3). That is, OpenCOBOL is free software!

[Ubuntu Linux](http://www.ubuntu.com/) and [Linux Mint](http://www.linuxmint.com/) have packages for OpenCOBOL. Probably other Linux distributions and FreeBSD have packages as well but I haven't checked. The installation (using Linux Mint) is simple:

```sh
sudo apt-get install open-cobol
```

I haven't tried to write software in COBOL. The closest I ever came is that I worked on converting between 4th generation languages (4GL) a few years ago. 4GL programs are often converted to COBOL. But I have written a short program in COBOL:

```cobol
      * Greeting to Grace Hopper
       IDENTIFICATION DIVISION.
       PROGRAM-ID.    greeting.
       DATA DIVISION.
       WORKING-STORAGE SECTION.
       01 WS-TODAY PIC X(21).
       01 WS-YEAR  PIC 9(4).

       PROCEDURE DIVISION.
       010-Greet.
           MOVE FUNCTION CURRENT-DATE TO WS-TODAY.
           MOVE WS-TODAY (1:4) TO WS-YEAR.
           
           SUBTRACT 1906 FROM WS-YEAR.
           DISPLAY "Happy birthday"
           DISPLAY WS-YEAR
           EXIT PROGRAM
           .
       STOP RUN.
```

Compiling the program using OpenCOBOL is easy:

```sh
cobc -x greeting.cob
```

and running is easy:

```sh
./greeting
```

I am not going to do a lot of COBOL programming in the future, but it seems to possible to replace old legacy operating systems with a modern platform like Linux.

