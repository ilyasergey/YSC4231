Week 13: Distributed Consensus
==============================

Paxos Conseunsus
----------------

* `Lecture Slides <_static/resources/ysc3248-week-14-paxos.pdf>`_
* `Paxos Made Simple
  <https://lamport.azurewebsites.net/pubs/paxos-simple.pdf>`_
* `Paxos Made Moderately Complex <http://www.cs.cornell.edu/courses/cs7412/2011sp/paxos.pdf>`_
* `Code with examples
  <https://github.com/ysc3248/lectures-2020/tree/13-paxos>`_,
  package ``paxos``

Code Commentary
---------------

**Implementation of Paxos Consensus**

* ``PaxosVocabulary`` --- messages used in the simple Paxos protocol

* ``SimplePaxos`` --- definitions of Paxos Acceptors, Proposers and Learners as Scala actors

* ``PaxosFactory`` --- utility class to create arbitrary instances of Paxos system

* ``PaxosTestUtilities`` --- basic suite to test our simple Paxos implementation

* ``SimplePaxosTests`` --- testing normal mode

* ``PaxosFailureTests`` --- testing Paxos with failures of acceptors

Byzantine Fault-Tolerance
-------------------------

* `Lecture Slides <_static/resources/ysc3248-week-14-byzantine.pdf>`_
* `Practical Byzantine Fault Tolerance <http://pmg.csail.mit.edu/papers/osdi99.pdf>`_
* `Mechanising Blockchain Consensus <https://ilyasergey.net/papers/toychain-cpp18.pdf>`_
* `A Concurrent Perspective on Smart Contracts <https://ilyasergey.net/papers/csc-wtsc17.pdf>`_
