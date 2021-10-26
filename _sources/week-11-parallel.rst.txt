.. -*- mode: rst -*-

Week 11: Data-Parallel Collections
==================================

Useful Resources
----------------

* `Documentation for Scala Parallel Collections
  <https://docs.scala-lang.org/overviews/parallel-collections/overview.html>`_
* `Splitters and Combiners
  <https://docs.scala-lang.org/overviews/parallel-collections/architecture.html>`_
* `Creating Custom Parallel Collections <https://docs.scala-lang.org/overviews/parallel-collections/custom-parallel-collections.html>`_
* `Code with examples
  <https://github.com/ysc4231/lectures-2021/tree/11-parallel>`_,
  package ``parallel``

Code Commentary
---------------
A short summary of the files from the accompanying code is given
below, outlining the characteristic aspects of working with Scala
Parallel Collections. We suggest you explore the files in the order
they appear in the following list.

**Measuring Performance**

* ``package object parallel`` --- a package object defining common
  functions used for benchmarking. ``warmedTimed`` is used to take
  advantage of JIT-based speed-up.

* ``ParDemoTimed`` --- showcasing a simple parallel collection
  example. Notice the oddities with timing parallel vs. sequential
  execution.

* ``ParDemoWarmed`` --- the same as before, but now with warmed-up
  times, hence a better comparison.

**Basic Usage of Parallel Collections**

* ``ParConfig`` --- controlling the level of parallelism for a
  collection.

* ``GoodParallelism`` --- showcasing an operation that allows for good
  parallelism.

* ``BadParallelism`` --- a case of a bad parallel speed-up (or the
  lack thereof) due to introduced contention in the operation applied
  to a collection.

**Caveats of Using Parallel Collections**

* ``NonParallelizableCollections`` --- comparing the inherent
  parallelism in different collections.

* ``NonParallelizableOperations`` --- analysing parallelism allowed by
  certain operations.

* ``ParSideEffectsIncorrect`` and ``ParSideEffectsCorrect`` ---
  parallel processing in the presence of side effects.

* ``ParNonCommutativeOperator`` --- exploiting the effects of
  commutativity in parallel collections. ``ArrayBuffer`` preserves the
  ordering of elements, while Scala's set does not.

* ``ParNonAssociativeOperator`` --- exploiting the influence of
  operation associativity when processing parallel collections.

* ``ConcurrentCollectionsWrong`` and ``ConcurrentCollectionsGood`` ---
  exploring interactions between parallel and concurrent collections.
  In the bad case, a sequential collection is used in a parallel
  setting, which leads to an error.

**Parallel Splitters and Combiners**

* ``ParString`` --- implementation of a parallel immutable string

* ``ParStringSplitter`` --- Recursive splitter for parallel strings

* ``ParStringSplitterTests`` --- Testing parallel string splitter

* ``ParStringSplitterBenchmarks`` --- benchmarks for string splitters

* ``ParStringCombiner`` --- two-phase combiner for parallel strings

* ``ParStringCombinerTests`` --- Testing parallel string combiner

* ``ParStringCombinerBenchmarks`` --- benchmarks for combiners

