.. -*- mode: rst -*-

Week 09: Asynchronous Computations and Futures
==============================================

Useful resources:

* `Documentation on Scala Futures and Promises
  <https://docs.scala-lang.org/overviews/core/futures.html>`_
* `Scala's for-comprehensions <https://docs.scala-lang.org/tour/for-comprehensions.html>`_
* Futures and Async: `Slides
  <https://speakerdeck.com/phaller/futures-and-async-when-to-use-which>`_
  and `Video <https://www.youtube.com/watch?v=TyuPdFDxkro>`_
* `Code with examples
  <https://github.com/ysc4231/lectures-2023/tree/09-futures>`_,
  package ``futures``

Summary of the Lecture
----------------------

A short summary of the files from the accompanying code is given below,
outlining the characteristic aspects of working with Java Futures, as well as
Scala Futures and Promises. It is recommended that the files are explored in the
order they appear in the following list:

**Java Futures**

* ``SortAndRead`` --- reading a user input after having performed a costly
  operation (array sorting). This examples demonstrates the need for
  parallelisation.

* ``SortAndRead2`` --- a better version of the previous program. Sorting is
  moved into a separate future. Introducing Java's thread pools and the class
  ``Future``.

* ``SortAndRead3`` --- even better implementation, in which the user input is
  also moved into a separate future.

**An Exercise on Java Futures**

* ``FutureSort`` --- an old friend, parallel quick-sort, now re-implemented with
  Java futures. An interesting question is why some of the offered thread pools,
  e.g., ``Executors.newFixedThreadPool(4)`` make it deadlock?

**Scala Futures**

* ``FutureDataType`` --- a first example of using Scala's futures, its
  ``isCompleted`` method and the implicit execution context
  (``ExecutionContext.Implicits.global``).

* ``FuturesCallbacks`` --- demonstration of processing results of the futures
  asynchronously via callbacks (using ``foreach`` method).

* ``FutureExceptions`` --- treatment of exceptions in futures, via
  ``onComplete`` method and pattern matching on the result class: ``Success`` or
  ``Failure``.

* ``AwaitExample`` --- an example showing the use of ``Await.result`` method to
  wait for a future to complete or fail otherwise.

**Composing Scala Futures**

* ``Options`` --- a quick practice on building combinators for the ``Option``
  type. Serves as an introduction to similar future combinators introduced next.

* ``ComposingFutures`` --- an example of composing two futures running
  asynchronously, via the explicit ``flatMap`` combinator (or using the ``for``
  notation). Check: what changes in the execution if the futures are inlined
  under the ``for`` comprehension?

* ``BlacklistedFiles`` --- a large example involving composing futures in the
  implementation of ``getAllBlacklisted``. Multiple ways to query the result are
  possible.

* ``ScalaFuturesTests`` --- shows how to test futures.

**Scala Promises**

* ``ProducerConsumer`` --- implementation of a producer-consumer with a
  promise, which serves as a single-assignment mailbox.

* ``ProducerConsumer2`` --- demonstration of ``isCompleted`` method of
  promises.

* ``ProducerConsumer3`` --- failing the promise and recovering after an
  exception in the future using the ``recover`` method.
