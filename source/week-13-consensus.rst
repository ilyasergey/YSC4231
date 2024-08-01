Week 13: Distributed Consensus, BFT; Wrap-Up
============================================

* `Code with examples
  <https://github.com/ysc4231/lectures-2024/tree/13-paxos>`_,
  package ``paxos``

Slides
------

* `Distributed Consensus <_static/resources/ysc4231-week-13-paxos.pdf>`_
* `Byzantine Fault Tolerance and Blockchains; Wrap-Up <_static/resources/ysc4231-week-13-byzantine.pdf>`_

Papers to Read
--------------

* `Paxos Made Simple <https://lamport.azurewebsites.net/pubs/paxos-simple.pdf>`_
* `Paxos Made Moderately Complex <http://www.cs.cornell.edu/courses/cs7412/2011sp/paxos.pdf>`_
* `Practical Byzantine Fault Tolerance <http://pmg.csail.mit.edu/papers/osdi99.pdf>`_
* `Mechanising Blockchain Consensus <https://ilyasergey.net/papers/toychain-cpp18.pdf>`_
* `A Concurrent Perspective on Smart Contracts <https://ilyasergey.net/papers/csc-wtsc17.pdf>`_

Code Commentary
---------------

**Implementation of Paxos Consensus**

* ``PaxosVocabulary`` --- messages used in the simple Paxos protocol

* ``SimplePaxos`` --- definitions of Paxos Acceptors, Proposers and Learners as Scala actors

* ``PaxosFactory`` --- utility class to create arbitrary instances of Paxos system

* ``PaxosTestUtilities`` --- basic suite to test our simple Paxos implementation

* ``SimplePaxosTests`` --- testing normal mode

* ``PaxosFailureTests`` --- testing Paxos with failures of acceptors

