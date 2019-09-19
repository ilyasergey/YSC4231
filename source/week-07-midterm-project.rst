.. -*- mode: rst -*-

Week 07: Midterm Project: Thread Pools
======================================

In this project we will be studying `thread pools
<https://en.wikipedia.org/wiki/Thread_pool>`_, a very useful
concurrent programming that allows one to use a `fixed` number of
threads for executing concurrent tasks with unbounded parallelism. In
some way, implementing a thread pool is similar to implementing a
multiprocessor mechanism that allocates a particular CPU for a given
thread. In reality, we typically have much fewer CPUs than we have
threads running concurrently in the program, therefore some of the
threads are forced to share processors. Furthermore, many runtimes
(Java/Scala) included do not allow for an arbitrarily large number of
threads to be spawned at the same time (remember that in our examples
the numbers of threads were in tens, maybe hundreds). Yet, it would be
undesirable for a programmer to worry about the allotted number of
threads that she is allowed to use. Thread pools provide a convenient
mechanism to lift this limitation by using a fixed limited number of
threads to execute an arbitrary number of "parallel" computational
`tasks`. 

Those of you who have completed the midterm project for the latest
edition of `YSC2229
<https://ilyasergey.net/YSC2229/YSC2229-midterm-tasks.html#an-array-based-memory-allocator>`_
in might think of thread pools as of "memory allocators" for threads.
The only difference here is that instead of providing transparent
access to some (de-facto limited) space, thread pools provide
transparent access to a limited number of concurrent threads that can
execute in parallel.

This project will be structured as a sequence of problems, each next
building on the previous one. Not all problems will involve
concurrency, but all of them should be completed in order to get the
full project grade. Some of the posed problems are open-ended and
require you to experiment with your design. Your solutions for those
will be evaluated based on their performance, clarity, and elegance.

Your deliverables for this project must include:

* A link to a GitHub release with the implementation based on the
  provided project template.
* A PDF file with the report describing your discoveries, experiments,
  design decisions and related thoughts.

The link to the repository template will be provided on Canvas.

