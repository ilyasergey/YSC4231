.. -*- mode: rst -*-

Week 13: Actors and Message-Passing Concurrency
===============================================

Useful Resources
----------------

* `Documentation for Akka Actors
  <https://doc.akka.io/docs/akka/current/actors.html>`_
* `Testing Akka actors
  <https://doc.akka.io/docs/akka/current/testing.html>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/12-actors>`_,
  package ``actors``

Code Commentary
---------------

A short summary of the files from the accompanying code is given
below, outlining the characteristic aspects of working with Scala
Actors. We suggest you explore the files in the order they appear in
the following list.

* ``HelloActor`` --- a simple actor that prints received messages into
  the terminal

* ``package object actors`` --- a package object with common
  definitions, such as, e.g., the actor system allowing to create new
  actors.

* ``ActorCreate`` --- creating a simple actor and interacting with it.

* ``DeafActor`` --- demonstration of processing unhandled messages.

* ``BadCountDownActor`` --- anti-pattern for behavioural change.

* ``CountdownActor`` --- an actor as a state-transition system

* ``CountDownActorWithResponse`` --- an actor that responds at the end

* ``SimpleActorTests`` --- testing actor systems

* ``ActorHierarchy`` --- demonstrate hierarchy of Akka actors

Homework
--------

* `Programming Assignment 7 <_static/resources/programming-07.pdf>`_
