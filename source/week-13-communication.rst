.. -*- mode: rst -*-

Week 13: Communication between Actors
=====================================

Useful Resources
----------------

* `Documentation for Akka Actors
  <https://doc.akka.io/docs/akka/current/actors.html>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/12-actors>`_,
  package ``actors``

Code Commentary
---------------

* ``TalkToChildren`` --- warm-up, talking to actors directly

* ``LifecycleActor`` --- observing the lifecycle of actors

* ``PingPong.scala`` --- example of the ask-pattern with a timeout

* ``CommunicatingPoisonPill`` --- Sending a poison pill to the actor

* ``CommunicatingGracefulStop`` --- death watch and graceful stop

* ``RemoteCommunication.scala`` --- Interaction between two remote
  systems of actors.
