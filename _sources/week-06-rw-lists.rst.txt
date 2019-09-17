.. -*- mode: rst -*-

Week 06: Read-Write Locking and Linked Lists
============================================

Read-Write Locking
------------------

In many cases a shared resource can allow multiple threads that do not
modify it access it concurrently, but will require an exclusive access
for someone to make modifications. This pattern is known as
`Readers-Writers`:

* Only one writer can be modifying the resource exclusively
* Many readers can observe it concurrently without requiring mutual
  exclusion, as long as there is no write.

The structure allowing for such an access is called **Read-Write
Lock**. It can be implemented using monitors as follows::

 import java.util.concurrent.TimeUnit
 import java.util.concurrent.locks.{Lock, ReadWriteLock, ReentrantLock}

 /**
   * @author Maurice Herlihy, Ilya Sergey
   */
 class SimpleReadWriteLock extends ReadWriteLock {

   private var readers = 0
   private var writer = false
   private val myLock = new ReentrantLock
   private val myReadLock = new ReadLock
   private val myWriteLock = new WriteLock
   private var condition = myLock.newCondition

   def readLock: Lock = myReadLock

   def writeLock: Lock = myWriteLock

   class ReadLock extends Lock {
     def lock(): Unit = {
       myLock.lock()
       try {
         while (writer) try {
           condition.await()
         } catch {
           case e: InterruptedException =>
         }
         readers += 1
       } finally {
         myLock.unlock()
       }
     }

     def unlock(): Unit = {
       myLock.lock()
       try {
         readers -= 1
         if (readers == 0) {
           condition.signalAll()
         }
       } finally myLock.unlock()
     }
     // ...
   }

   protected class WriteLock extends Lock {
     def lock(): Unit = {
       myLock.lock()
       try {
         while (readers > 0) try {
           condition.await()
         } catch {
           case e: InterruptedException =>

         }
         writer = true
       } finally myLock.unlock()
     }

     def unlock(): Unit = {
       myLock.lock()
       try {
         writer = false
         condition.signalAll()
       } finally {
         myLock.unlock()
       }
     }
     // ...
   }
   // ...
 }

Notice that any reader using the instance of the ``ReadLock`` will be
blocked as long as a writer is present (which is indicated by a
boolean shared variable ``writer``). Once available, the reader lock
will admit multiple readers, so the writers will have to wait on a
writer lock until the ``condition`` is notified by ``ReadLock``'s
``unlock()``. A similar intuition is applied to the writer lock.
Notice that the ``condition`` does not distinguish between the roles
(readers/writers) --- it is used to notify all threads currently
waiting. In principle, the lock can be improved by using two different
condition variables.

The problem with the version of the Read-Write lock above is that if
readers keep coming, a writer will never have a chance to acquire the
lock. This can be fixed if, as soon as the writer acquires the writer
lock, it will be only waiting until `all readers currently holding
ReadLock` will exit. That is, no new readers will be allowed into the
critical section until writer gets an access. This can be implemented
as follows::

 class FIFOReadWriteLock extends ReadWriteLock {

   private var readers = 0
   private var writer = false
   private var readAcquires, readReleases: Int = 0
   private val myLock = new ReentrantLock
   private val myReadLock = new ReadLock
   private val myWriteLock = new WriteLock
   private var condition = myLock.newCondition

   def readLock: Lock = myReadLock

   def writeLock: Lock = myWriteLock

   class ReadLock extends Lock {
     def lock(): Unit = {
       myLock.lock()
       try {
         while (writer) try {
           condition.await()
         } catch {
           case e: InterruptedException =>
         }
         readAcquires += 1
       } finally {
         myLock.unlock()
       }
     }

     def unlock(): Unit = {
       myLock.lock()
       try {
         readReleases += 1
         if (readAcquires == readReleases) {
           condition.signalAll()
         }
       } finally myLock.unlock()
     }

     // ...
   }

   protected class WriteLock extends Lock {
     def lock(): Unit = {
       myLock.lock()
       try {
         while (readAcquires != readReleases) try {
           condition.await()
         } catch {
           case e: InterruptedException =>

         }
         writer = true
       } finally myLock.unlock()
     }

     def unlock(): Unit = {
       myLock.lock()
       try {
         writer = false
         condition.signalAll()
       } finally {
         myLock.unlock()
       }
     }

     // ...

   }

   // ...
 }

When Should We Use Monitors
---------------------------

Monitors (locks + conditional variables) are complementary to
spin-locks. An appropriate synchronisation mechanisms depends on the
use case:

* Spin-locks are good when the critical sections are small (in terms
  of execution time), thus the spinning time will likely be small too.
  The main "cost" of a spin-lock is the high usage of CPU cycles while
  spinning, as well as added contention overhead. Thus, spinning makes
  sense for a multiprocessor, if we expect a short waiting time.

* Monitors should be used for fine-grained management of access to a
  critical section, which is long. However, for small critical
  sections, waking up a thread requires `context switching` by a
  processor, which is also expensive. That is, waiting (blocking) is
  preferable if we expect to wait for a long time before getting the
  access to the critical section.

Other Synchronisation Mechanisms
--------------------------------

As of now, monitors (reentrant locks + condition variables) are one of
the most popular blocking synchronisation mechanisms. However, most of
the popular concurrent libraries (such as ``java.util.concurrent`` and
C's ``PThreads``) provide other synchronisation primitives. Those are
typically implemented as instructions by most of the common processors.

* **Semaphore** is similar to a lock that admits :math:`n \geq 1`
  threads. Once the capacity is reached, the new incoming threads are
  blocked. Semaphores were invented by Edsger Dijkstra (the same as in
  Dijkstra's algorithm) in 1963. An example of using a semaphore (in
  Java) can be found, e.g., by `this link
  <https://www.mkyong.com/java/java-thread-mutex-and-semaphore-example/>`_.

* **Mutex** is simply a semaphore with capacity 1. As such, it is
  equivalent to a lock.

Concurrent Lists, Part I
------------------------

* `Lecture Slides <_static/resources/ysc3248-week-06-lists-01.pdf>`_
* `Code with examples
  <https://github.com/ysc3248/ysc3248-examples/tree/06-lists>`_,
  package ``lists``

Homework
--------

* `Programming Assignment 3 <_static/resources/programming-03.pdf>`_
