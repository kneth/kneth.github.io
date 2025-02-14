---
title: "FOSDEM 2025"
date: 2025-02-14T10:43:48+01:00
categories: [conference]
tags: [conference, meetup, free software]
draft: false
---

# FOSDEM 2025

In February 2025 I attended [FOSDEM](https://www.fosdem.org) in Brussels, Belgium for the first time. During two days, 1052 events/talks were held with 933 speakers. As you can imagine, I only attended a fraction of the sessions. As part of FOSDEM, many free software projects have booths, and I also spent time working around in the booth areas to get an impression of the diversity of the free software community today.

## Devroom: tools the docs

### Orgmode witchcraft at Spritely

Presenter: Amy Grinn, tech admin, [Spritely Institute](https://spritely.institute/)

The talk was a general overview on how Spritely Institute uses Emacs in many tasks, include documentation. The entire presentation was done from Emacs!
The documentation is written as org-mode files, and one trick is to use Emacs as shell in Makefiles to write build scripts in Elisp, Scheme, or [WISP](https://github.com/skeeto/wisp):

```
SHELL = emacs
SHELLOPTIONS = -Q --batch --l setup.el --eval
```

To support multiple programming languages, a picker is added to the documentation. It is primarily using CSS to pick the language, and if JavaScript is disabled in the browser (the Tor browser in particular), a default language is shown only.
Org-mode and Emacs on mobile, the presenter recommends using `termux` and Syncthing is a good option to sync between laptop/desktop and mobile.
For bookkeeping, Spritely is using the ledger [Beancount](https://github.com/beancount/beancount) which has a good integration with Emacs. The Emacs package[Boxy](https://elpa.gnu.org/packages/boxy.html) (maintained by the presenter) is usedto render tree of accounts.

### CLI magic tricks for docs projects

Presenter: Lorna Mitchell, between jobs (a vim and Linux user)
The take-home message in this talk is that command-line (CLI) tools are important for document. Arguments to learn CLI tools are:

- never go out of fashion
- are searchable and the internet has many resources
- are scriptable (for batch processing)

The talk was a primarily a demo of useful tools: `ls`, `tree`, `wc`, `grep`, `sed`, `diff` (remember to set diff tool for git: `git config diff.tool`). Due to limited time, the presenter was not able to show any advanced use cases or tools.

### Patterns for maintainer and tech writer collaboration

Presenter: Daniel D. Beck

The talk explained why many open source maintainers is failing to recognize (by under and overestimating) tech writers' capacity and skills, and their own support. In that way, they are failing to link resources to project's need. The consequence is that tech writers and maintainers often don't collaborate.
The presenter has done research documentation project archetypes, and he has identified-

- Planning and evaluation
- Production (manual, samples)
- Revision and transformation
- Tools and processes

#### References

- https://ddbeck.com/fosdem2025/
- https://innersourcecommons.org/

### Evolving real-world AsciiDoc into a specification and how it will help the ecosystem

Presenter: Alexander Schwartz, Redhat
AsciiDoc is a lightweight text format, and currently Eclipse Foundation is working on a formal specification.

The presenter explained about the three stages of a typical workflow when working with documentation: author -> convert -> publish. For documentation in AsciiDoc, [Antora](https://antora.org/) is a tool for generating static web sites.

#### Reference

- https://asciidoc.org

### Docs straight from the code - AST powered automation

Presenter: James Shubin, https://purpleidea.com/

With this talk, the presenter introduced and demoed his own tool to generate API documentation for Go code. As most modern languages store comments in AST, you can generate the documentation from the comments.

### No more broken docs: keep docs accurate with Doc Detective

Presenters: Jake Cahill and Ariel Kaiser

As a beginning, the presenters highlighted the challenges to keep docs in sync with product:

- product updates
- share responsibilities -> no responsible
- lack of knowledge: tech writers don't know the product well enough

When the document is out of sync with the product, the consequences can include

- user frustrations
- support overhead
- user retention

One solution is to use [docs as test](https://www.docsastests.com/) to automate testing of documentation.
The talk explained and demoed [Doc Detective](https://doc-detective.com/) which is a test framework for CLI tools, web UI, and API calls. It used JSON as format to describe tests, and the target audience is tech writers. Features include

- take screenshots and do screen recordings to check if they differs from a previous screenshot
  - can also be used for updating documentation's screenshots
- can generate test files using regular expressions
- has GHA support

An example of a user of Doc Detective is [RedPanda Console quick start](https://docs.redpanda.com/current/console/quickstart/).

### API documentation testing with AI user simulation

Presenter: Lisa Driukova, JetBrains

The talk was focusing on API documentation, and the challenges of getting feedback on API doc can be

- time constraints
- expertise of users (too skilled, not enough skilled)

The solution could be to use AI:

- test for gabs in documentation
- identify edge cases and unanswered questions
- reduce cognitive load of stakeholders

The presenter has created a PoC with a workflow starting with an OpenAPI spec. Currently, using AI is not useful for unstructured documentation.

### 9800 sandboxes and counting

Presenter: Jay Clifford, Grafana

The goals of deveveloper documentation are

- key source of truth for product
- enablement: from beginner to expert user

Grafana is using a sandbox based on [Killercoda](https://killercoda.com/). The advances include

- a disposable VM
- interactive docs
- experiment risk free
- accelate learning curve

Currently is it used for course material at Grafana. Killercode is using with markdown and JSON, and has engagement tracking build in.

## Building the next generation cloud native database

Presenter: Sunny Bains, PingCAP
The presenter used the talk to introduce the [TiKV](https://github.com/tikv/tikv), which is implemented in Rust and is utilizing the [Raft consensus algorithm](https://raft.github.io/). The next generation of databases must be able to scale up to 200 PB - and scale down when needed!
A cloud native database (TiDB serverless as an example)- in the presenter's opinion - must use

- S3: it is cheap to storage but can be expensive to access
- Integrate the database with the cloud providers' services
- Disaggregated storage
  - local disks or memory as write-through cache
  - data shared by row and column
- Raft logs as the only log
- spot instances to operate on immutable S3

## 14 years of systemd

Presenter: Lennart Poettering

The presenter's code (systemd) is used by major Linux distributions, and a few distributions have been created to use the presenter's code!

The title of the talk turned out to be inaccurate - it is 15 years ago systemd development was initiated.
Before systemd we had

- sysvinit (designed in 1983, first commit can be traced back to 1992)
- upstart (2006 - 2014) - used by Ubuntu
  - manual configuration
  - slow development
  - unfair contributor rules (copyright transfer)
- babykit evolved into systemd

Systemd is influenced by

- sysvinit and upstart
- Apple's launchd (from 2005)
- Solaris SMF (from 2005)
- UNIX?
  - it has a unified repository for kernel and user space
  - Linux is the opposite with its many distributions
  - systemd is heavily using `cgroup` which is close to the UNIX' philosophy that everything should be a file (or at least a directory)

Today, systemd is default for major Linux distributions:

- Fedora since 2011
- openSuse and Arch since 2012
- RHEL + SLES since 2014
- Debian + Ubuntu since 2015

The project has 6 core maintainers, and 60 persons with commit rights. It consists of about 150 binaries, and it is mostly written in C (690k SLOC). It relies heavily on `dlopen()` as a way to support weak dependencies.

When deciding if something belongs to systemd, the following criteria are considered:

- generic
- foundational (low-level)
- common
- future (no legacy)
- clean (don't cut corners)
- follow a common style

The project operates with a number of important concept. For example, a clear seperation of `/etc`, `/run`, and `/usr`. Hermetic `/usr` (`/usr` must contain everything needed to set up a minimal working system) is a cornerstone. Merging of configuration files from various locations should always work, and configuration should be declarative and not imperative. For the project, it is important to follow existing standards, and document behaviour accurately.
The future - according to the presenter and not all core maintainers - could include

- boot and system integrity (solved by major commercial operating systems) to lock down what you can run
- Pivot IPC - [varlink](https://varlink.org/) is an option
- C
  - Rust is considered as an alternative but dynamic linking in Rust is not ready for production usage
- moving from a package-based OS to an image-based OS
  - systemd already has [`mkosi`](https://github.com/systemd/mkosi)

## Forked communities: project re-licensing and community impact

Panel:

- Stephan Walli, Microsoft
- Dawn M. Foster, CHAOSS
- Ben Ford, Overlook InfraTech
- Brian Proffitt, Redhat

The panel discussion was focusing on a number of commercial open projects which have in the last years re-licensed to a non-open license: MongoDB, ElasticSearch, Redis, and Terraform.

The re-licensing has shown gaps in the (open source) business model, and it has typically abandoned the community around the project.

In the last decade, forking larger open source projects haven't been common, and often the code and projects have been merged back. Recent development is that forks happen more often.

Corporate diversity seems to make it less likely to re-license, and for projects with multiple companies participating, the project will be more healthy. And more healthy project, forking and re-licensing is less likely.

According to RedMonk, there is no financial benefit by re-licensing.

The panel agrees that cloud providers are in their rights to use open source software. But their scale seems to be the issue as they don't contribute back to the project.

## Databases in the AI trenches

Presenter: Bruce Momjian, EDB

With the introduction of ChatGPT in November 2022, AI moved from discriminative AI to generative AI (GenAI). Discriminative AI is used for classification, recommendation, prediction, and translation. Generative AI gives us human-like conversations.
The presenter tried to give a high-level introduction to how GenAI is implemented. From embedding vectors, vector search to transformers. The ultra-high dimensional vector spaces can consume very large data sets.
The presenter used PostgreSQL and OpenAI/ChatGPT to demonstrate how you can implement your own AI applications.

## Devroom: JavaScript

### JSR - open source package registry

Presenters: Leo Kettmier, Deno; Luca Casonato, Deno

JavaScript Registry (JSP) is a new alternative to NPM, and is a reaction to NPM's lack of openness and innovation. It can work with NPM packages, and it supports Deno, Bun, Node.js, and Cloudflare Workers.
TypeScript support is build in, and when you publish a package, TypeScript is transpiled to JavaScript by JSR to make it easy for NPM users to consume the package. Moreover, API documentation is extracted and published with the package.
To avoid type-squatting, all packages must be published within a scope.
JSR is currently setting up a governance board to ensure transparency in all decisions. In the near future, JSR will be transferred from Deno to a foundation (still unclear which one).

### Nobody asks "How is JavaScript?"

Presenter: Ujjwal Sharwa, Igalia

The talk was a walk-through of the standardization process around Java^H^H^H^HECMAScript. The technical committee ([TC39](https://github.com/tc39)) consists of

- delegates
  - implementors
  - companies
  - non-profit organizations
  - universities
- invited experts
  - subject-matter experts
  - community representatives
- editors and reviewers

All decisions are done in consensus, and each proposal goes through a number of stages:

- 0: Just an idea (over-simplified proposal), and many proposals will not go further.
- 1: A proposal, and time is devoted to to develop it. A demo and polyfills are developed, and a champion is elected to managing the proposal. It is not a solution yet.
- 2: Syntactic and semantic details are ironed out, and a formal specification is written. It is now a solution as APIs are completed.
- 2.7: Conformance tests are written which will help engine implementors. The [test262](https://github.com/tc39/test262) test suite is a good place to contribute.
- 3: Recommended for implementors.
- 4: Finished when two implementation are passing conformance tests.

We can expect ECMAScript 2025 in June!

### Privacy-first architecture: alternatives to GDPR popup and local-first

Presenter: Andrey Sitnik

The talk was an introduction to [local-first](https://localfirstweb.dev/) as a new paradigm in developing privacy-aware software. It stands in opposition to the current server-first (cloud) paradigm, and the local-only paradigm in the early days of computing.
Local-first is a spectrum as not all applications can satisfy the criteria in the [locat-first manifesto](https://www.inkandswitch.com/local-first/). The benefits include simplified server, cheap to scale up, no privacy issues, higher developer productivity and zero latency.
The technical side of local-first is to have a local/client-side database and persistence storage (can be challenging for browsers), and conflict resolution when synchronizing data. Often [CRDT](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type) are used (the presenter didn't mention [Operational Transformation](https://en.wikipedia.org/wiki/Operational_transformation)).

### Demystifying Temporal

Presenter: Aditi Singh, Igalia

`Temporal` is the replacement for JavaScript's `Date`, and it has started to be implemented in popular JavaScript engine (currently in stage 3). The features are

- time/date computations
- internationalization (including time zone and non-gregorian calendars)
- strongly typed
- immutable

The talk demonstrated how `Temporal` can be used, and solutions were compared to code using `Date`. `Temporal` seems to be a good advancement for JavaScript developers.

### EuroHPC FP: a Federated Platform for HPC Infrastructure in Europe, Built with Open Source Software

Presenter: Henrik Nortamo

The talk presented the work on unifying the HPC installations in Europe. Currently Europe has 9 active and 3 planned supercomputers, 7 announced AI factories and about 8 quantum computers in progress. A major challenges for users today is that they need to have separate accounts on each supercomputer or AI factory, they use. Moreover, using AI attract users with non-HPC background (read: Linux, C/C++/Fortran and command-line tools). EuroHPC wants to make it easier for researchers and companies to utilize the supercomputers and AI factories.

A federated platform (EFP) has been designed and is under development. We can expect it to be fully operational in Q1/2026. EFP will provide

- single sign-on
- centralized view of resources
- a software catalogue
- interactive web accees

The platform is built on open source software, including

- MyAccessID - secure shell, identity management
- Walder - allocation/job scheduler
- Grafana and OpenSearch - monitoring
- OpenOnDemand - Jupyter and remote desktop
- zammad - helpdesk
- Lexis and Apache Airflow - workflows

It is expected that later will be possible to integrate smaller regional/national installations with EFP.

## Running Kubernetes Workloads on HPC with HPK

Presenter: Antony Chazapis, Institute of Computer Science, FORTH

The presenter introduced his system to integrate Kubernetes workloads on classical supercomputers. The system is called HPK (High Performance Kubernetes). It creates ephemeral Kubernetes mini-clusters to run on cluster nodes allocated by [Slurm](https://slurm.schedmd.com/documentation.html).

## How we are defending Software Freedom against Apple at the EU's highest court

Presenter: Lucas Lasota, Free Software Foundation Europe

The presenter began his talk with talking about an awkward neighbor who

- eats 30 % of your pizza
- never leaves
- and controls who you can invite home

The awkward neighbor is a metafore for Apple and how they control iOS and iPadOS. In general, EU calls the awkward neighbor gateway in the Digital Market Act, and specific actions can be taken against gateways. The talk centered around how FSFE has pushed the case against Apple at EU's highest court.

The presenter argues that if we can talk about healthy digital ecosystems, mobile today is a digital plantation and a monoculture.
