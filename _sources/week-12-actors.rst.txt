.. -*- mode: rst -*-

Week 12: Actors and Message-Passing Concurrency
===============================================

.. admonition:: Quote 

   A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable. 

   **Leslie Lamport**

Useful Resources
----------------

* `Documentation for Akka Actors
  <https://doc.akka.io/docs/akka/current/actors.html>`_
* `Testing Akka actors
  <https://doc.akka.io/docs/akka/current/testing.html>`_
* `Code with examples
  <https://github.com/ysc4231/lectures-2024/tree/12-actors>`_,
  package ``actors``

Actor Terminology
-----------------

These are best thought in terms of software companies and employees exchanging emails within them.

* **Actor System** - hierarchical group of actors that share the same configuration. Responsible for creating new actors, locating them, and logging important events. Think the Company itself.

* **Actor Class** - a template that describes the state and the behaviour of the actor. Think designation within a company.

* **Actor Instance** - an entity that exists at runtime and is capable of sending an receiving messages. Actor Instance is an instance of an Actor Class. Think an employee.

* **A Message** - unit of communication between actors. Any object can be a message. Messages are sent and processed asynchronously. Think an e-mail.

* **The Mailbox** - part of the memory, associated with an actor instance that is used to buffer messages. Just like a regular e-mail mailbox.

* **Actor Reference** - an object that allows you to send messages to a specific addresse. Think e-mail address. 

* **Dispatcher** - a component that decides the priorities for actors to process the messages. Think company e-mail policy.

Code Commentary
---------------

A short summary of the files from the accompanying code is given
below, outlining the characteristic aspects of working with Scala
Actors. We suggest you explore the files in the order they appear in
the following list.

**Creating and Using Actors**

* ``HelloActor`` --- a simple actor that prints received messages into
  the terminal using standard log facilities.

* ``package object actors`` --- a package object with common
  definitions, such as, e.g., the actor system allowing to create new
  actors.

* ``ActorCreate`` --- creating a simple actor and interacting with it.

* ``DeafActor`` --- demonstration of processing unhandled messages.

* ``BadCountDownActor`` --- anti-pattern for behavioural change.

* ``CountdownActor`` --- an actor as a state-transition system.

* ``CountDownActorWithResponse`` --- an actor that responds at the end.

* ``SimpleActorTests`` --- testing actor systems.

* ``DictionaryActor`` --- a state-machine actor implementing a
  dictionary. This is meant as an exercise.

* ``DictionaryActorTests`` --- tests for ``DictionaryActor``.

**Actor Hierarchy and Life Cycle**

* ``ActorHierarchy`` --- demonstrate hierarchy of Akka actors.

* ``TalkToChildren`` --- Talking to children actors directly.

* ``CheckActor`` --- identifying actors by their paths in the system.

* ``LifecycleActor`` --- observing the lifecycle of actors.

**Actor Communication and Supervision**

* ``PingPong.scala`` --- example of the ask-pattern with a timeout.

* ``Router`` --- Example of a router actor and message forwarding.

* ``CommunicatingPoisonPill`` --- Sending a poison pill to the actor
  causing it to terminate.

* ``CommunicatingGracefulStop`` --- death watch and graceful stop.

* ``Supervision.scala`` --- actor supervision.

**Implementing Remote Systems**

* ``RemoteCommunication.scala`` --- Interaction between two remote
  systems of actors.
