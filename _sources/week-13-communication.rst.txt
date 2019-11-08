.. -*- mode: rst -*-

Week 13: Communication between Actors
=====================================

Useful Resources
----------------

* `Documentation for Akka Actors
  <https://doc.akka.io/docs/akka/current/actors.html>`_
* `Orders of message delivery <https://doc.akka.io/docs/akka/current/general/message-delivery-reliability.html>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/12-actors>`_,
  package ``actors``

Code Commentary
---------------

* ``DictionaryActor`` --- a state-machine actor implementing a
  dictionary

* ``DictionaryActorTests`` --- tests for ``DictionaryActor``

* ``LifecycleActor`` --- observing the lifecycle of actors

* ``CommunicatingPoisonPill`` --- Sending a poison pill to the actor

* ``Supervision.scala`` --- actor supervision

* ``CheckActor`` --- identifying actors by their paths in the system

* ``TalkToChildren`` --- warm-up, talking to actors directly

* ``PingPong.scala`` --- example of the ask-pattern with a timeout

* ``CommunicatingGracefulStop`` --- death watch and graceful stop

* ``RemoteCommunication.scala`` --- Interaction between two remote
  systems of actors.
