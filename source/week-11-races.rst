.. -*- mode: rst -*-

Week 09: Data Race Detection in Practice
========================================

* `Lecture Slides <_static/resources/ysc4231-week-09-races.pdf>`_

In this mini research project you'll be working in groups of two. The
goal of this project is to get you exposed to the state-of-the-art
tools for finding concurrency bugs in large Java codebases.

You are not required to be proficient in Java in order to complete
this project, but you are expected to understand the meaning of Java's
``synchronized`` keyword and be able to follow the structure of class
definitions. Given your knowledge of Scala, figuring out those
relations should be trivial. 

Background: Data Races in Java
------------------------------

In the previous lectures of this module, we've been primarily
concerned with implementations of non-trivial concurrent data
structures and algorithms, most of which feature a form of "racing"
between threads. Such fenomena, called `race conditions` occur
frequently when multiple concurrent threads try to simultaneously
perform a certain operations (e.g., grab a lock).

However, if the threads are racing over a memory location that is not
synchronised (i.e., it is not implemented by means of
``AtomicInteger`` or a similar class, or isn't protected by a lock),
it almost certainly indicates a bug in the implementation. For instance,
consider the examples in the lectures, in which a counter has been
inconsistently incremented due to the missing locks. This situation is
commonly referred to as a `data race`.

According to Oracle's `official documentation
<https://docs.oracle.com/cd/E19205-01/820-0619/geojs/index.html>`_, a
**data race** in concurrent Java code occurs when:

* two or more threads in a single process access the same memory
  location (i.e., a mutable field of an object) concurrently, and
* at least one of the accesses is for writing, and
* the threads are not using any exclusive locks to control their
  accesses to that memory.

When these three conditions hold, the order of accesses is
non-deterministic, and the computation may give different results from
run to run depending on that order. Some data-races may be benign (for
example, when the memory access is used to implement locks via fields
marked as ``volatile``), but many data-races are bugs in the program. 

Unfortunately, both notions of `race conditions` and `data races` are
frequently confused. You might find `this blog post
<https://dzone.com/articles/race-condition-vs-data-race>`_ helpful to
disambiguate these definitions and acquire some extra intuition on
what should be considered data races. In practice, programmers very
rarely implement their own synchronisation mechanisms, and instead
rely on library constructions, such as ``ReentrantLock``. Therefore,
about 90% of the concurrent code written "in the wild" uses standard
synchronisation mechanisms, and most of the concurrency-related bugs
are, in fact, data races introduced because of a missing
synchronisation.

Luckily for the humanity, such data races often can be identified in
an automated way via tools for `static program analysis`. This project
is dedicated to interaction with one of such tools.

The Tool: Facebook Infer
------------------------

We will be using `Facebook Infer <https://fbinfer.com>`_ as a tool for
static data race detection in large Java projects. Infer provides a
large suite of analyses for Java code, but we will only need its data
race detector, known as **RacerD**. You can find the necessary
documentation on installing and using the relevant parts of Infer and
examples using `this link <https://fbinfer.com/docs/checker-racerd>`_.

As a part of this assignment, please, check out the following research
paper, which introduces pragmatics of Infer's RacerD component and
provides a number of examples. You don't have to understand all the
details of Section 5 or follow the specifics of the experiments, just
look for a general intuition on how the analysis reports data races.

* `RacerD: Compositional Static Race Detection
  <https://ilyasergey.net/papers/racerd-oopsla18.pdf>`_

You may also find it useful to watch the accompanying video of the
`conference talk <https://www.youtube.com/watch?v=1fnUTMMQ5y0>`_ on
RacerD.

Example of a Racy Java Class
----------------------------

As an example of a simple data race, consider the following Java code::

  public class Racy {
    public void foo(B b) {
      final A a = new A();
      synchronized (this) {
        b.haz(a);
        b.haha(42);
      }
    }
  }

  class B {
    A myA = new A();
    public synchronized void haz (A a) {
      myA = a;
    }

    protected void haha(int x){
      myA.f = x;
    }
  }

  class A { int f = 0; }

In order to compile this code to JVM's ``.class`` binary file, you
need to save it in the file ``Racy.java`` and then invoke the
following command from the terminal::

  javac Racy.java

The code should compile without errors. 

The class ``Racy`` can be potentially used as a library in a
multi-threaded environment (which is determined by the fat that it has
``synchronized`` modifiers in it), and, as such, it contains a data
race, manifested by some of involved objects' mutable fields being
potentially accessed without synchronisation.

To confirm that, let's delete the compiled ``.class`` file and re-run
the compilation of ``Racy.java`` with Infer/RacerD::

  infer --racerd-only -- javac Racy.java

The following is printed to the output::

 Found 1 issue

 Racy.java:19: error: THREAD_SAFETY_VIOLATION

   Read/Write race. Non-private method `void B.haha(int)` reads
   without synchronization from `this.B.myA`. Potentially races with
   write in method `B.haz(...)`.
   Reporting because another access to the same memory occurs on a
   background thread, although this access may not.

   17.   
   18.     protected void haha(int x){
   19. >     myA.f = x;
   20.     }
   21.   }

This indicates that a call of the method ``haha()`` may create a race,
when, e.g., invoked concurrently with the (correctly synchronised)
method ``haz()`` of the same object. 

The result of the analysis will be printed to the console and also
recorded in the locally created file ``infer-out/bugs.txt``.

**Question:** Can you suggest how we could fix this issue by
introducing more synchronisation?

The Task
--------

Your goal for in this assignment is to hunt down and explore data
races in large real-world Java projects. A list of some of such
projects is given below, but you may also find some on your own.

You may work on this project either individually or in teams of two.
By using Infer/RacerD you will have to locate **four (eight for a team
of two) distinct** data races in one or more large projects, explain
the reasons why the analyser considers them such, and provide a
tentative solution on how they could be fixed. If the races cannot be
fixed easily (e.g., by just declaring a Java method as
``synchronized``), outline your ideas on what prevents one from doing
so. The result of your project should a be PDF document that contains:

.. admonition:: Note
 
   If you work individually, you may only consider one project. In a
   team of two, you should consider at least **two different** projects.

* A short report on the chosen Java projects. For instance, which
  parts of the projects utilise concurrency, and why do you think it
  is beneficial there? 

* Descriptions of 4 (8 for the team of two) data races (possibly
  from multiple different projects), each complemented with a short story as
  described above. Some variations on what is reported are possible
  and are described below.

* If applicable, a quick enumeration of the technical issues
  encountered while working on this project (to help the future
  generations).

.. admonition:: 

   If you're using Linux or Windows/WSL and want to run RacerD
   natively, please, install `Version 0.17.0
   <https://github.com/facebook/infer/releases/tag/v0.17.0>`_ of the
   tool by compiling it from the sources as described in the
   `corresponding instructions
   <https://github.com/facebook/infer/blob/99464c01da5809e7159ed1a75ef10f60d34506a4/INSTALL.md>`_.
   Before running the build script, make sure to install all the
   dependencies via ``apt`` package manager, as listed, e.g., in `this
   file
   <https://github.com/facebook/infer/blob/99464c01da5809e7159ed1a75ef10f60d34506a4/docker/master/Dockerfile>`_.

Open-Source Java Projects with Concurrency
------------------------------------------

Below is a list of some real-world Java projects using concurrency.
Most of them contain data races. Feel free to pick one or more of them
to explore in our data race study.

* https://github.com/apache/tomcat
* https://github.com/ibr-cm/avrora
* https://github.com/aragozin/jvm-tools
* https://github.com/apache/xalan-j
* https://github.com/OpenHFT/Chronicle-Map
* https://github.com/ReactiveX/RxJava
* https://github.com/adammurdoch/native-platform
* https://github.com/aws/aws-sdk-java

The projects were chosen for the facts that they extensively use
Java's ``synchronized`` primitive and, occasionally, the
``@ThreadSafe`` annotations.

You are welcome to come up with your own case studies, as long as
those are reasonably large projects not implemented by yourself. That
said, it is also fine if your exploration will be limited to a subset
of the projects listed above.

Running RacerD on Custom Projects
---------------------------------

The suggested large projects can be built from scratch using one of
the following three build-systems for Java. Make sure that the
necessary build tool is installed and can be run from the command
line. In most of the cases it can be done simply by using the package
manager of your operating system (e.g., ``brew`` for Mac OS X). The
kind of build system used by a particular project is determined by a
`building descriptor file` (or simply `buildfile`) that can be located
in the project root folder:

* `Ant <https://ant.apache.org/manual/install.html>`_ (buildfile
  ``build.xml``) --- one of the oldest build systems for Java, which
  is rarely used nowadays. In order to build a project, you typically
  only need to run ``ant`` from the terminal. To remove all compiled
  files, run ``ant clean``.

* `Maven <https://maven.apache.org/install.html>`_ (buildfile
  ``pom.xml``) --- a more advanced build system, similar in spirit to
  Scala's SBT. To compile a project, run ``mvn compile``. To clean the
  project from the results of the compilation, run ``mvn clean``.

* `Gradle <https://gradle.org/install/>`_ (buildfile ``build.gradle``)
  --- a build system based on the Groovy programming language. To
  build, run ``./gradlew build`` from the project root. To clean, run
  ``./gradlew clean``.

Check the ``README`` files of the corresponding projects for specific
instructions.

To make Infer/RacerD analyse a custom project, you need to "attach" it
to the compilation process. To do so, make sure that you run it on a
project that has not been compiled yet (or whose compiled files have
been removed via, e.g., ``ant clean`` in the case of ``ant``). If you
don't ensure this, RacerD will most likely not report any results. To
run the analysis attached to a building process, run the following
command::

  infer --racerd-only -- <build-command>

where ``<build-command>`` should be the corresponding command for a
particular build system, for instance::

  infer --racerd-only -- ant

or::

  infer --racerd-only -- mvn compile

or::

  infer --racerd-only -- ./gradlew build

depending on the parrticular build system the project uses.

Notice that some projects might provide specific instructions on how
to build them, not following one of the patterns above. In this case,
you will need to provide the command line that is supposed to build
the project as a replacement of ``<build-command>`` in the template
above. If the compilation of the project fails, you still might be
able to partially analyse it if adding the flag ``--keep-going`` to
the command ``infer --racerd-only``::

  infer --racerd-only --keep-going -- <build-command>

Finally, you can also run Infer after the compilattion, by pointing it
correctly to the foldere with sources and the compiled
``.class``-files as follows::

  infer --racerd-only --sourcepath <path-to-java-files> --generated-classes <path-to-class-files>

As previously shown, all results of the analysis run are collected in
the file ``bugs.txt`` under the locally created folder ``infer-out``.

Tips and Tricks
---------------

Here are some hints and comments on how to approach this assignment.

* It is suggested that you team up with someone who uses a different
  OS than you (e.g., Mac OS and Linux) to cater for the situations
  when building a project or running Infer is impossible due to
  system-specific reasons. It is perfectly fine if just one of the
  teammates obtains the report, and they you split the workload on
  code triaging for bugs.

* If you run WSL or Linux, I suggest you install Infer version 0.17.0.
  It can be built from sources available as a `zip-archive
  <https://github.com/facebook/infer/releases/tag/v0.17.0>`_. Follow
  the `instructions on building it
  <https://github.com/facebook/infer/blob/99464c01da5809e7159ed1a75ef10f60d34506a4/INSTALL.md>`_
  and make sure to first install all the Linux dependencies via apt
  (can be found at the top of this `Dockerfile
  <https://github.com/facebook/infer/blob/99464c01da5809e7159ed1a75ef10f60d34506a4/docker/master/Dockerfile>`_).
  Before building Infer make sure that you have JDK 1.8 installed (in principle,
  1.11 should work too, but I haven't checked it).
  `Here is a link to
  <https://docs.datastax.com/en/jdk-install/doc/jdk-install/installOpenJdkDeb.html>`_
  some instructions on how to do that. Make sure that both your
  Java and Javac are of the correct version. You can switch them as described `here
  <https://dev.to/harsvnc/how-to-change-your-java-and-javac-version-on-ubuntu-linux-1omj>`_.

* Please, allocate sufficient time to install Infer and build some of
  the projects and be prepared to resolve the issues with missing
  libraries and/or dependencies. Solving those might take **much
  longer** than you'd expect!

* Your reported data race don't have all come from the same project:
  you may pick as many projects as necessary to describe in your
  report.

* You **don't** have to understand what `exactly` the analysed code
  does. It's perfectly fine if you explain an error in terms of
  fields/classes it affects, without explaining what purpose those
  classes serve. It is, in fact, quite frequent in large development
  to fix bugs in someone else's code without fully understanding what
  it does but just following some predefined strategies (nowadays some
  bugs can be even fixed automatically!).

* Beware that Infer/RacerD can give `false positives`, i.e., report
  some code as being racy, whereas in fact it is not. If you manage to
  identify such fragments (which is typically harder than confirming a
  race) and provide reasoning on why a certain report is a false
  positive, feel free to use it instead of one of the race report.
  That said, **at least one** of your reports should be about what you
  consider to be **true race** detected by the analyser.

* Related to the previous, some of the races reported by the tool can
  be `benign`, e.g., used for implementation of custom synchronisation
  mechanisms via atomic or ``volatile`` variable. If you manage to
  identify any properly describe one of those, feel free to use it in
  your report (instead of a proper data race report).

* Infer/RacerD is just another program, and it may contain bugs
  itself. Sometimes it might crash, in which case it is suggested you
  abandon a specific project that causes it to do so and try another
  one. Also, don't spend too much time on a project you can't compile.

* When looking for more projects on GitHub that have concurrency in
  them, it's a good strategy to check if they use ``synchronized``
  statements or ``@ThreadSafe`` annotations.

* Don't worry about confirming a data race reported by RacerD as a
  true one (in case if it's not). This is an exploratory project,
  aimed to give you experience with bug detection at scale. That said,
  you are expected to do your best when explaining the nature of the
  bugs. Just copying-pasting RacerD report won't do it.

* Don't worry if the legitimate data races you're describing are not
  so "interesting" and look like silly programming mistakes. Most of
  the real-life bugs are quite silly (and if they weren't we couldn't
  have nice automated tools that discover them so efficiently).

Further Reading
---------------

More about why data races might be harmful:

* `Are Data Races bad? (StackOverflow) <https://stackoverflow.com/questions/20374281/are-data-races-bad>`_
* `Position Paper: Nondeterminism is unavoidable, but data races are pure evil <https://www.hpl.hp.com/techreports/2012/HPL-2012-218.pdf>`_

If you are interested in the state of the art in the research on data
race detection, as well as on static analyses of production code, you
might also want to check the following research papers:

* The `Context and Selected Related Work` section of `RacerD documentation <https://fbinfer.com/docs/checker-racerd/#context-and-selected-related-work>`_
* `ThreadSanitizer – data race detection in practice <https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/35604.pdf>`_
* `FastTrack: Efficient and Precise Dynamic Race Detection <https://users.soe.ucsc.edu/~cormac/papers/pldi09.pdf>`_
* `Lessons from Building Static Analysis Tools at Google
  <https://ai.google/research/pubs/pub46576>`_
* `Scaling Static Analyses at Facebook <https://cacm.acm.org/magazines/2019/8/238344-scaling-static-analyses-at-facebook/fulltext>`_

