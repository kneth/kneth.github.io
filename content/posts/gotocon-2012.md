---
title: "GotoCon 2012"
date: 2012-10-08T21:06:23+02:00
categories: [conference]
tags: [conference, meetup, big data, NoSQL]
draft: false
---

## GotoCon 2012 in Århus

I attended [GotoCon 2012](http://gotocon.com/aarhus-2012/) in Århus last week. To be more precise, I attended the [Big Data track](http://gotocon.com/aarhus-2012/tracks/show_track.jsp?trackOID=615) Monday. My educational background is somewhat related to supercomputing (yeah, I did my share of Fortran-77 programming as a graduate student), and I have over the years worked on various "Big Data" project: bioinformatics, credit card fraud detection, building Linux clusters, etc. Currently, I work for a small NoSQL database vendor, and our solution could fit the Big Data quite nicely. Given all this, going to Århus and spend a day listening to the open source Big Data vendors sounded like a treat.

### Neo4j - Jim Webber

First speaker was Jim Webber from [Neo4j](http://neo4j.org/). Neo4j is a graph database, and I like graph theory a lot. Jim is not just a speaker - he is an entertainer. He began his talk by looking back on the database history. As you might be aware of, relational databases were developed in 1970s, and through the 1980s, Oracle became The Database. In the last decade, a number of companies has gone "google scale" that is, they have vast amount of data. Handling big data requires different data models than relational databases.
Jim pointed out that the complexity of an application is a function of data size, connectness, and uniformity. Of course, his graph database can help you if your data is highly connected. He demonstrated a number of data sets and how to query them using Neo4j.

### Couchbase - Chris Andersen

Chris noted that the database industry is changing rapidly these years. Companies are required to shrink and grow databases on demand. In particular in the mobile app world where an app can go virtal over night. As an example, he mentioned Instagram who gained about one million new users on one day when they released their Android app.

He boils down the requirements to:

* grow and shrink databases on demand
* easy cluster node deployment
* multiple masters in the cluster (for availability)
* multiple datacenters (for availability)
* auto sharding
  
The old-school approach to scalability of the data layer is to sharded MySQL instances and memcached. But this approach typically requires some high availability handling in the application code. With Couchbase (and probably other NoSQL databases), the applications are free of this complexity.

Couchbase has conducted a survey among NoSQL users, and the flexible schemas are reported as the most important feature.

### Cassandra - Matthew Dennis

Matthew began his talk by discussing the relevance of Big Data. According to studies, companies using Big Data products and techniques seem to be out perform companies not using Big Data. [Cassandra](http://cassandra.apache.org/) is offering a master-free cluster database, and it scales well. When data sets are larger than physical memory, it slows down gracefully. A personal note: data sets smaller than physical memory are not big data.

According to Matthew Solid State Disks (SSD) are pushing the limit as they lower the latency. Cassandra is SSD aware: it does not overwrite data but only append data. Files (probably, its blocks) are reclaimed by the database when they are not used any more. Latency is important for Matthew, and he argues that linear scalability means that latency is constant when:

* increasing throughput and increasing number of nodes
* increasing load and increasing nodes

The nodes in a Cassandra cluster are equal, and queries are proxies from node to node. This implies that Cassandra is eventually consistent.

### MongoDB - Alvin Richards

Last speaker in the track was about [MongoDB](http://www.mongodb.org/). Alvin talked about scaling up without spending (too much) money and that is where the NoSQL revolution fits in. In the last 40 years, we have seen a dramatic growth in computing power for example, memory has increased from 1 Kb to 4 GB, and disk space has gone from 100 MB to 3 TB.

For MongoDB, availability is some important than consistency. Together with the [CAP theorem](http://en.wikipedia.org/wiki/CAP_theorem), this gives some consequences for the architectural choices for MongoDB. The asynchronous replication within a MongoDB cluster implies that MongoDB is eventually consistent.
Storing and analyzing time series is an important use case for NoSQL. 

### Panel discussion

The organizers has arrange a panel discussion with the major NoSQL vendors - and [Martin Fowler](http://martinfowler.com/). Martin has just published a [book about NoSQL](http://martinfowler.com/books/nosql.html). I have read it - and I will return with a review in the near future.

Martin noted that NoSQL is still immature. But the good news is that NoSQL brings us past "one model fits all". It is worth noticing that most NoSQL databases are released under an open source license - and backed by companies.

The panelists agreed that the CAP theorem and the application should drive which database to choose. The major issue here is that the majority of software developers only read 1 computer science book per year.
