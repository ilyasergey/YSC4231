.. -*- mode: rst -*-

Midterm Project
===============

In this project we will be studying `thread pools
<https://en.wikipedia.org/wiki/Thread_pool>`_, a very useful
concurrent programming pattern that allows one to use a `fixed` number
of threads for executing concurrent tasks with unbounded parallelism.
In some way, implementing a thread pool is similar to implementing a
multiprocessor mechanism that allocates a particular CPU for a given
thread. In reality, we typically have much fewer CPUs than we have
threads running concurrently in the program, therefore some of the
threads are forced to share processors. Furthermore, many runtimes
(Java/Scala included) do not allow for an arbitrarily large number of
threads to be spawned at the same time (remember that in our examples
the numbers of threads were in tens, maybe, hundreds). Yet, it would
be undesirable for a programmer to worry about the allotted number of
threads that she is allowed to use at any moment. Thread pools provide
a convenient mechanism to lift this limitation by using a fixed number
of threads to execute an arbitrary number of "concurrent"
computational `tasks`.

Those of you who have completed the `midterm project for the latest
edition of YSC2229
<https://ilyasergey.net/YSC2229/YSC2229-midterm-tasks.html#an-array-based-memory-allocator>`_
might think of thread pools as of "resource allocators" for threads.
The only difference here is that instead of providing transparent
access to some (de-facto limited) memory space, thread pools provide
transparent access to a limited number of concurrent threads that can
execute in parallel.

This project will be structured as a sequence of problems, each next
building on the previous one. Not all problems will involve
concurrency, but all of them should be completed in order to get the
full project grade. Some of the posed problems are open-ended and
require you to experiment with your design. Your solutions for those
will be evaluated based on their performance, clarity, and elegance.

Your deliverables for this project must include:

* A link to a tagged GitHub release with the implementation based on the
  provided project template.
* A PDF file with the report describing your discoveries, experiments, design
  decisions, and related thoughts. The text below as well as some of the files
  in the provided project template will contain questions in comments. You are
  encouraged to elaborate on those in your narrative.

The link to the project template will be provided on Canvas. The template
contains many hints and specifications in the comments. Make sure to read and
understand them before starting with your implementations.

Problem 1 (Warm-Up)
-------------------

As you know, `Quicksort <https://en.wikipedia.org/wiki/Quicksort>`_ is
one of the best sorting algorithms used in practice. Let us start from
implementing a simple sequential version of Quicksort and making sure
that it works correctly. To do so, please, check and, when requested,
modify the following classes/objects/traits in the project:

* ``Sorting`` - a generic interface for in-place array sorting
  algorithms. The type of ``sort(...)`` method is ``Unit``, indicating
  that no new array is constructed.

* ``SimpleQuicksort`` - an implementation of a classical `in-place`
  quicksort algorithm for an array. 

* ``ArrayUtil`` contains a number of utility methods, useful for working with
  arrays and testing sorting algorithms. Make sure to implement those that have
  partially missing implementations. When working with it, do not remove the
  ``import Ordering.Implicits._`` line, as otherwise the ordering operators,
  such as ``<``, ``>`` etc will not be available for values of type ``T:
  Ordering``.

* ``SortingTests`` provides generic testing machinery for different
  array-sorting algorithms. Don't forget add some adequate checks for the sorted
  result to ensure that your algorithm does indeed produce a sorted version of
  its input array.

* ``SimpleQuicksortTests`` - a specific test suite for
  ``SimpleQuicksort``, which should be running without assertion
  failures once you implement the components listed above. Feel free
  to fiddle with the size of the array being sorted and examine the
  trends in performance.

Problem 2: Parallel Quicksort
------------------------------

A really nice property of Quicksort is that, due to its "divide-and-conquer"
nature, it is `naturally parallelisable`. That is, its recursive sub-calls,
performed after the partitioning step, work on `disjoint` sub-arrays. Therefore,
we can run those calls `concurrently` in different threads, spawned for each
such sub-call. hopefully, this will allow us to make some good use of our fancy
parallel processors. Indeed, we should be able to sort an array much faster as
now the work will be split between parallel threads changing its disjoint parts.
By the way, do we need any form of synchronisation between those threads and if
we do, how should ve do it (answer this in your report)?

In this problem, please, inspect and, when requested, change the following files
in the project template:

* ``ParallelQuicksort`` - implement ``sort()`` so it would create new threads
  for parallel sorting. Use ``start()`` and ``join()`` to control the lifetime
  of the children threads and synchronise them with the parent thread that
  spawned them.

* ``ParallelQuicksortTests`` - this test should succeed once you
  implement ``ParallelQuicksort``.

By running the tests, we can compare the performance of the two algorithms. What
are your thoughts about this? Can you explain the observed phenomena with regard
to the execution times?

Problem 3: Thread Pool
----------------------

Let us try a different strategy for adding concurrency into inherently
parallelisable tasks, such as Quicksort, by means of introducing a `thread
pool`. This is the largest sub-problem in the project, which will require you to
study and modify a number of provided files. The project template contains a
number of ready-to-use examples that will allow you to experiment with your
thread pool implementation.

The following classes files are of your interest:

* ``ThreadPool`` is the main class implementing the thread pool. Some parts of
  the implementation are already provided and are explained in the comments. The
  class instance takes as an argument the size of the pool, i.e., a number of
  "worker" threads that it will maintain so they will execute the
  client-supplied tasks.

The most interesting component of the ``ThreadPool`` implementation is the field
``taskQueue``. Notice that this is a mutable (linked) non-thread-safe queue from
the standard Scala library. It will contain some user-provided `tasks`, which
will be executed by the fixed number of "worker"-threads, maintained by the
pool. Notice that we take advantage of Scala's functional nature, representing
tasks as functions of type ``Unit => Unit`` (you can think of them as
`thunks`---"bottled" computations that will fire when applied to the unit value
``()``). The task queue can grow arbitrarily large, depending on the number of
tasks scheduled to execute by the threads in the pool.

The second important component is the array ``workers`` containing a fixed
number of threads that will be executed all those tasks. The main trick of a
thread pool is that threads are `not created` whenever a new concurrent
computation needs to be executed. Instead, we have a fixed array (the pool) of
constantly running threads that "pick up" tasks from the queue and execute them.
Whenever there are no tasks, the threads are "waiting" for something to be added
to the task queue. When a worker thread starts executing a task, it removes it
from the queue.

An auxiliary boolean array ``workInProgress`` is used to record, which of the
threads are currently executing some tasks. It will come useful to determine
whether all pending computations have been completed.

The exception ``ThreadPoolException`` is used to indicate invalid usage of the
of the thread pool. Feel free to throw it in the appropriate situations.

The inner class ``Worker`` implements a worker thread functionality. Its
functionality is structured in three parts:

1. Prelude: waiting for new tasks to be provided. This part requires
   synchronisation with the other worker threads and the client

2. Body: running some task. Does this part require synchronisation?
   Please, elaborate.

3. Epilogue: letting others know that you have completed this task,
   doing some bookkeeping and moving on to the next task. Do we need
   some synchronisation here?

The ``ThreadPool`` class provides three methods available to its clients.

* ``shutdown()`` is a method that terminates all worker threads in the pool.
  Typically, it is used by the client when there is no need in the pool, and all
  its threads can be put to rest. I suggest implementing this method using the
  ``interrupt()`` method of the thread class. Calling this method for a thread
  ``t`` that is blocked on a ``wait()`` method of some monitor makes ``t`` throw
  an ``InterruptedException`` and terminate its waiting and its execution. This
  exception can be caught and handled appropriately - a pattern known as
  `Graceful Shutdown` of a thread. The provided object
  ``InterruptThreadExample`` shows an example of using this functionality on a
  single thread.

* The method ``async(task: Unit => Unit)`` takes a task from the user and
  "schedules" it for an execution by some worker thread. Since there might be
  more tasks in the queue than workers, it is not guaranteed that the task will
  be executed immediately. Check the comments in the code and work out the way
  threads are made aware of the new tasks. Once you have this method
  implemented, try running the object ``AsyncExample`` in IntelliJ. As the
  result, you should see the output similar to the following one::

   Task 3
   Task 1
   Task 2
   Task 5
   Task 4
   Task 7
   Task 6
   Task 8
   Task 9
   Task 10
   About to shut down the pool.

   Process finished with exit code 0

  There will be also a small delay right after the line ``Task 10`` is printed.

* The method ``startAndWait(task: Unit => Unit): Unit`` is similar to
  ``async()`` in that it will also schedule a provided task for the execution by
  some of the worker threads. However, unlike ``async()`` it should `block` the
  caller thread until all activity in the thread pool ceases. That is, this
  method's intended use is to give raise to some bunch of concurrent tasks,
  enabled by the thread pool, and then wait for all those tasks (and also the
  tasks they might create) to complete. This way, the caller will be
  synchronised with all concurrent tasks executed by the thread pool. This is
  what we used to achieve via ``Thread.join()`` in the case of using native Java
  threads. Once implemented, you can experiment with using this method (in
  conjunction with ``async()`` and ``shutdown()``) by running the
  ``StartAndWaitExample`` object.

Problem 4: Pooled Quicksort
---------------------------

It is time to get back to our quicksort implementation and put the thread pool
to a good use. Inspect and modify the following files:

* ``PooledQuickSort`` is the object which should implement the quicksort via the
  thread pool. Just follow the comments in the file.

* ``PooledQuickSortTests`` - a test suite for ``PooledQuickSort``.

Now let us run the three versions of quicksort we have implemented. Are we happy
with the result delivered by ``PooledQuickSort``? What if we increase the array
size? Can you explain the performance phenomena when comparing the execution of
``PooledQuickSort`` to those of ``SimpleQuickSort`` and of
``ParallelQuickSort``?

.. admonition:: Hint

   If you find all your Quicksort implementation being very slow on large
   arrays, check how you generate those arrays used for benchmarking. Recall in
   the cases in which Quicksort doesn't perform great in terms of complexity.
   How about arrays with little diversity in theis elements (e.g., what if
   you're trying to quick-sort and array of ``10,000,000`` numbers ranging
   between ``1`` and ``10``)?

Problem 5: Hybrid Quicksort 
---------------------------

Finally, it's time to unleash your creativity and experiment with different
flavours of concurrent sorting to get the best of both worlds: single-threaded
and parallel:

* ``HybridQuickSort`` - implement your own quicksort-based sorting strategy in
  this object with the aim to fix the shortcomings of the previous three
  algorithms. Feel free to experiment with different heuristics and parameters.

* ``HybridQuickSortTests`` - use this file to test your hybrid sorting
  algorithm.

For the grand finale, let us check the absolute performance of the four sorting
algorithms. Use the file ``SortingBenchmarks`` to compare the implementations on
the arrays of the different size. The benchmark suite also includes
``ScalaSort`` -- a fine-tuned default Scala library implementation of array
sorting. Can you beat it in terms of performance? Use the benchmarks and drive
your experiments in the search of a better sorting algorithm that uses the full
potential of the parallel multiprocessors.

Make sure to document all your gotchas in your report.

Good luck!





