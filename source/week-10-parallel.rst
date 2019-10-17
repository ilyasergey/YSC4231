.. -*- mode: rst -*-

Week 10: Futures and Promises
=============================

Useful resources:

* `Documentation for Scala Parallel Collections
  <https://docs.scala-lang.org/overviews/parallel-collections/overview.html>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/11-parallel>`_,
  package ``parallel``

Summary of the Lecture
----------------------

A short summary of the files from the accompanying code is given
below, outlining the characteristic aspects of working with Scala
Parallel Collections. We suggest you explore the files in the order
they appear in the following list

**Using Scala Parallel Collections**

* ``package object parallel`` --- a package object defining common
  functions used for benchmarking. ``warmedTimed`` is used to take
  advantage of JIT-based speed-up.

* ``ParDemoTimed`` --- showcasing a simple parallel collection
  example. Notice the oddities with timing parallel vs. sequential
  execution.

* ``ParDemoWarmed`` --- the same as before, but now with warmed-up
  times, hence a better comparison.

* ``ParConfig`` --- controlling the level of parallelism for a
  collection.

* ``GoodParallelism`` --- showcasing an operation that allows for good
  parallelism.

* ``BadParallelism`` --- a case of a bad parallel speed-up (or the
  lack thereof) due to introduced contention in the operation applied
  to a collection.

* ``NonParallelizableCollections`` --- comparing the inherent
  parallelism in different collections.

* ``NonParallelizableOperations`` --- analysing parallelism allowed by
  certain operations.

* ``ParSideEffectsIncorrect`` and ``ParSideEffectsCorrect`` ---
  parallel processing in the presence of side effects.

* ``ParNonCommutativeOperator`` --- exploting the effects of
  commutativity in parallel collections.

* ``ParNonAssociativeOperator`` --- exploting the influence of
  operation associativity when processing parallel collections.

* ``ConcurrentCollectionsWrong`` and ``ConcurrentCollectionsGood`` ---
  exploring interactions between parallel and concurrent collections.

**Implementing Scala Parallel Collections**

Coming soon!

Homework
--------

Coming soon!
