.. -*- mode: rst -*-

Week 12: Splitters and Combiners for Parallel Collections
=========================================================

Useful Resources
----------------

* `Documentation for Scala Parallel Collections
  <https://docs.scala-lang.org/overviews/parallel-collections/overview.html>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/11-parallel>`_,
  package ``parallel``

Code Commentary
---------------
A short summary of the files from the accompanying code is given
below, outlining the characteristic aspects of working with Scala
Parallel Collections. We suggest you explore the files in the order
they appear in the following list.

* ``ParNonCommutativeOperator`` --- exploting the effects of
  commutativity in parallel collections.

* ``ParNonAssociativeOperator`` --- exploting the influence of
  operation associativity when processing parallel collections.

* ``ConcurrentCollectionsWrong`` and ``ConcurrentCollectionsGood`` ---
  exploring interactions between parallel and concurrent collections.

* ``ParString`` --- implementation of a parallel immutable string

* ``ParStringSplitter`` --- Recursive splitter for parallel strings

* ``ParStringSplitterTests`` --- Testing parallel string splitter

* ``ParStringSplitterBenchmarks`` --- benchmarks for splitters

* ``ParStringCombiner`` --- two-phase combiner for parallel strings

* ``ParStringCombinerTests`` --- Testing parallel string combiner

* ``ParStringCombinerBenchmarks`` --- benchmarks for combiners

Homework
--------

* `Programming Assignment 6 <_static/resources/programming-06.pdf>`_
