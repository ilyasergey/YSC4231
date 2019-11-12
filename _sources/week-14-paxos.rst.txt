Week 14: Distributed Consensus
==============================

Useful Resources
----------------

* `Lecture Slides <_static/resources/ysc3248-week-14-paxos.pdf>`_
* `Paxos Made Simple
  <https://lamport.azurewebsites.net/pubs/paxos-simple.pdf>`_
* `Paxos Made Moderately Complex <http://www.cs.cornell.edu/courses/cs7412/2011sp/paxos.pdf>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/13-paxos>`_,
  package ``paxos``

Code Commentary
---------------

* ``PaxosVocabulary`` --- messages used in the simple Paxos protocol

* ``SimplePaxos`` --- definitions of Paxos Acceptors, Proposers and Learners as Scala actors

* ``PaxosFactory`` --- utility class to create arbitrary instances of Paxos system

* ``PaxosTestUtilities`` --- basic suite to test our simple Paxos implementation

* ``SimplePaxosTests`` --- testing normal mode

* ``PaxosFailureTests`` --- testing Paxos with failures of acceptors
