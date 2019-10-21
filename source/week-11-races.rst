.. -*- mode: rst -*-

Week 11: Data Race Detection in Practice
========================================


Background on Data Races in Java
--------------------------------

TODO

Resources:

* `Installing Facebook Infer <https://fbinfer.com/docs/getting-started.html>`_
* `RacerD Documentation <https://fbinfer.com/docs/racerd.html>`_
* TODO: Some papers

Example of a Racy Java Class
----------------------------

For instance, the following Java file containing three classes::

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
need to save it in the file ``Racy.java`` and then infoke the
following command from the terminal::

  javac Racy.java

The code should compile without error. 

Noe let's delete the compiled ``.class`` file and re-run the
compilation of ``Racy.java`` with Infer/RacerD::

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

Your goal for in this assignment is to hunt and explore data races in
large real-world programs written in Java. You can find a list of such
projects below, or find some others on your own.  

Working in groups of two, by using Infer/RacerD you will have to
locate **five distinct** data races in one or more large projects,
explain the reasons why the analyser considers them such, and provide
a tentative solution on how they could be fixed. If the races cannot
be fixed easily (e.g., just by wrapping a Java method to
``synchronized``), outline your ideas on what prevents one from doing
so. Submit your observations and explanations of the bugs in a PDF
document by the deadline.

Here are some hints and comments on this assignment.

* It is suggested that you team up with someone who uses a different
  OS than you (e.g., Mac OS and Linux) to cater for the situations
  when building a project or running Infer is impossible due to
  system-specific reasons. It is perfectly fine if just one of the
  teammates obtains the report, and they you split the workload on
  code triaging for bugs.

* Please, allocate sufficient time to install Infer and build some of
  the projects and be prepared to resolve the issues with missing
  libraries and/or dependencies. Solving those might take **much
  longer** than you'd expect!

* Your reported data race don't have all come from the same project:
  you may pick as many projects as necessary to describe in your
  report.

* Don't worry if the legitimate data races you're describing are not
  so "interesting" and look like silly programming mistakes. Most of
  the real-life bugs are quite silly (and if they weren't we couldn't
  have automated tools to discover them so efficiently).

* You **don't** have to understand what exactly the analysed code
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
  That said, **at least one** of your reports should be about a **true
  race** detected by the analyser.

* Infer is just another program. Sometimes it might crash, in which
  case it is suggested you abandon a specific project that causes it
  to do so and try another one. Also, don't spend to much time on a
  project you can't compile.

* When looking for more projects on GitHub that have concurrency in
  them, it's a good strategy to check if they use ``synchronized``
  statements or ``ThreadSafe`` annotations.

Open-Source Java Projects with Concurrency
------------------------------------------

Below is a list of some real-world Java projects using concurrency.
Most of them contain data races. Feel free to pick one or more of them
to explore for your assignment.

* https://github.com/OpenHFT/Chronicle-Map
* https://github.com/ibr-cm/avrora
* https://github.com/aragozin/jvm-tools
* https://github.com/apache/xalan-j
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
the following three systems for Java. Ensure that the necessary system
is first installed as command-line tool. In most of the cases it can
be done simply by using the package manager of your operating system
(e.g., ``brew`` for Mac OS X). The kind of build system used by a
particular project is determined by a `building descriptor file` (or
simply `buildfile`) that can be located in the project root folder:

* `**Ant** <https://ant.apache.org/manual/install.html>`_ (buildfile
  ``build.xml``) --- one of the oldest build systems for Java, which
  is rarely used nowadays. In order to build a project, you typically
  only need to run ``ant`` from the terminal. To remove all compiled
  files, run ``ant clean``.

* `**Maven** <https://maven.apache.org/install.html>`_ (buildfile
  ``pom.xml``) --- a more advanced build system, similar in spirit to
  Scala's SBT. To compile a project, run ``mvn compile``. To clean the
  project from the results of the compilation, run ``mvn clean``.

* `**Gradle** <https://gradle.org/install/>`_ (buildfile
  ``build.gradle``) --- to build, run ``./gradlew build`` from the
  project root. To clean, run ``./gradlew clean``.

Please, check the ``README`` files of the corresponding projects for
further instructions.

To make Infer/RacerD analyse a custom project, you need to "attach" it to
the building process. To do so, make sure that you run it on a project
that has not been compiled yet (or whose compiled files have been
removed via, e.g., ``ant clean`` in the case of ``ant``). If you don't
ensure this, RacerD will most likely not report any results. To run
the analysis attached to a building process, run the following
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
able to aprtially analyse it if adding the flag ``--kepp-going`` to
the command ``infer --racerd-only``::

  infer --racerd-only --keep-going -- <build-command>

Finally, you can also run Infer after the compilattion, by pointing it
correctly to the foldere with sources and the compiled
``.class``-files as follows::

  infer --racerd-only --sourcepath <path-to-java-files> --generated-classes <path-to-class-files>

As previously shown, all results of the analysis run are collected in
the file ``bugs.txt`` under the locally created folder ``infer-out``.

Additional Reading
------------------

TODO

