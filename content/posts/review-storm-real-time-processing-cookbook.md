---
title: "Review Storm Real Time Processing Cookbook"
date: 2013-11-10T18:32:45+02:00
categories: [review, big data]
tags: [big data, free software, map/reduce]
draft: false
---

## Review: Storm - real-time processing cookbook

Quinton Anderson has written a book on the analysis platform [Storm](http://storm-project.net/) and published it at [Packt](http://www.packtpub.com/). I have worked a little with [Hadoop](http://hadoop.apache.org/) in the last couple of years, and it is only natural to take a look at the other big data processing platform. Hadoop is a batch processing platform, and Storm is for real-time processing and analysis of data. That means the two projects are not direct competitors, and they might complement each other.

When reviewing a technical book for the general public, it is important not to review the technology but the book. You can easily write a crappy book on excellent technologies while the opposite is very difficult. This review should be read in this context.

The author starts out by explaining how to set up Storm. Storm seems to be quite a complex beast, but Mr. Anderson gets nicely through it. I would have preferred to get an introduction to some of the concept before jumping into the many tasks. But it is my personal preference, and this is a cookbook and not a text book for a university course.

The first couple of chapters is about processing real-time data. Twitter and log files are the canonical examples in this area, and the book utilizes these as well. 

One chapter are on how to use C++ and Qt in your real-time data processing. If you think that Qt is about graphical user interfaces, the book will show you that Qt is a lot more. The author is using Qt's non-GUI parts in his processing.

Another chapter is about machine learning. As part of the big data revolution, machine learning has become popular again. Machine learning is a topic that Mr. Anderson is passionate about, and he analyzes in great detail the problem before showing the recipe. 

One of the major disadvantages of the book is that the assumptions about the reader are pretty hard. The reader is assumed to know at least about:

* Java development using and Maven and Eclipse
* Some functional programming
* Ubuntu or Debian (or any UNIX) command-line
* Web development (HTML, CSS, JavaScript, JSON)
* Data modelling experience
* A little about NoSQL

This problem does not really from the author but from Storm. But the author might have chosen other examples. The book is not a university text book, and therefore I would like many more references to text book and papers.

There is a lot of source code in the cook. You should really download the examples as some of them are longer than a page. It would be great if Packt would do some kind of syntax highlighting. Most programmers find it easier to read syntax highlighted code. In particular, electronic books (I have read the book as PDF) can easily be colorized!

One of the things I really like about the book is that the author has taken time to craft understandable diagrams. A well-composed diagram is worth many words, and he often sums up the key points in a diagram. In general the author writes in a rather dry or fact based language. But on page 111, you find that the author cannot suppress his humor: "... for  automating Clojure projects without setting your hair on fire."

I'm not going to say that Storm is a crappy technology but Quinton Anderson has done the job well by writing a good cook book.

If you are serious in getting into data science and data processing, I wouldn't hesitate to recommend the book. You can find the book at http://www.packtpub.com/storm-realtime-processing-cookbook/book.
