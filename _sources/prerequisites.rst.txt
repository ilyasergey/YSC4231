.. -*- mode: rst -*-

Software Prerequisites
======================

We will use `Scala <https://www.scala-lang.org/>`_ as a main programming language for this course. 

Getting Scala
-------------

In your preparation for the first lecture, please install the following software artefacts (or make sure that you have them installed in your system):

* `Java SDK 1.8 <https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>`_
* `Scala Build Tool (sbt)<https://www.scala-sbt.org/download.html?_ga=2.57019370.1900758631.1565340428-2015161099.1565340323>`_
* `IntelliJ IDEA <https://www.jetbrains.com/idea/>`_. When you start IntelliJ for the first time, make sure to choose Scala plugin when IntelliJ IDEA suggests you to download featured plugins.
* `Scala plugin for IntelliJ IDEA <https://www.jetbrains.com/help/idea/discover-intellij-idea-for-scala.html>`_ (if not installed on the previous step)

All these components can be found at the `Scala Download page <https://www.scala-lang.org/download/>`_.

Working with Version Control
----------------------------

The code from the lectures will be disseminated via `GitHub <https://github.com/>`_ using the ``git`` version control system. If you don't have a GitHub account yet, please, create one for yourself. ``git`` comes installed on most of Unix systems. It can be downloaded for Windows via `this link <https://git-scm.com/download/win>`_.

Make sure that you are comfortable with the ``git`` operations, such as ``clone``, ``pull``, ``add``, ``commit``, and ``push``. Some resources that might be helpful:

* `Signing up for a new GitHub account <https://help.github.com/en/articles/signing-up-for-a-new-github-account>`_
* `Basic git commands <https://www.hostinger.com/tutorials/basic-git-commands>`_
* `GitHub student pack <https://education.github.com/pack>`_

Checking your Setup
-------------------

The code appearing in the lectures will be collected in tthis `repository with examples <https://github.com/ilyasergey/ysc3248-examples>`_. 

To check your Scala setup, clone this project from GitHub (via ``git clone git@github.com:ilyasergey/ysc3248-examples.git``). Next, try to execute the following two commands in the terminal from the root of your project (it will take a few minutes the first time you run it, as ``sbt`` needs to download all the dependencies)::

  sbt test

will run the tests in the project. The following line::

  sbt "runMain basic.HelloWorld"

will execute a simple script printing ``Hello, World!`` to the output.

Additionally, you can try to open this project in IntelliJ IDEA via ``File -> Open`` and choosing the project folder. Click "OK" when asked about initial project settings.





