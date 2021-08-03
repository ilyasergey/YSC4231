.. -*- mode: rst -*-

Software Prerequisites
======================

We will be using `Scala <https://www.scala-lang.org/>`_ (version 2) as a main
programming language for this course.

Getting Scala
-------------

In your preparation for the first lecture, please install the following software artefacts (or make sure that you have them installed in your system):

* `Java SDK 1.11
  <https://www.oracle.com/sg/java/technologies/javase-jdk11-downloads.html>`_.
  You will need to make an Oracle account to download the latest version.
* `Scala Build Tool (sbt) <https://www.scala-sbt.org/download.html?_ga=2.57019370.1900758631.1565340428-2015161099.1565340323>`_
* `IntelliJ IDEA <https://www.jetbrains.com/idea/>`_. When you start IntelliJ for the first time, make sure to choose Scala plugin when IntelliJ IDEA suggests you to download featured plugins.
* `Scala plugin for IntelliJ IDEA <https://www.jetbrains.com/help/idea/discover-intellij-idea-for-scala.html>`_ (if not installed in the previous step)

All these components can be found at the `Scala 2 Download page <https://www.scala-lang.org/download/scala2.html>`_.

Working with Multiple Java Versions
-----------------------------------

If you want to maintain multiple versions of Java Development Kit on your
machine, consider installing the utility tool ``jenv`` (available `here
<https://www.jenv.be/>`_). Follow the instructions on the linked webpage to
switch between multiple versions and add already installed versions to ``jenv``
list.

Working with Version Control
----------------------------

The code from the lectures will be disseminated via `GitHub <https://github.com/>`_ using the ``git`` version control system. If you don't have a GitHub account yet, please, create one for yourself. ``git`` comes installed on most of Unix systems. It can be downloaded for Windows via `this link <https://git-scm.com/download/win>`_.

Make sure that you are comfortable with the ``git`` operations, such as ``clone``, ``pull``, ``add``, ``commit``, and ``push``. Some resources that might be helpful:

* `Signing up for a new GitHub account <https://help.github.com/en/articles/signing-up-for-a-new-github-account>`_
* `Basic git commands <https://www.hostinger.com/tutorials/basic-git-commands>`_
* `GitHub student pack <https://education.github.com/pack>`_

Checking your Setup
-------------------

The code appearing in the lectures will be collected in this `repository with examples <https://github.com/ysc4231/lectures-2021>`_.  In order to be able to access it, please, make sure to email your GitHub name to the instructor---this is necessary to grant you GitHub access for course-related repositories.

To check your Scala setup, clone this project from GitHub (via ``git@github.com:ysc4231/lectures-2021.git``). Next, try to execute the following two commands in the terminal from the root of your project (it will take a few minutes the first time you run it, as ``sbt`` needs to download all the dependencies)::

  sbt test

will run the tests in the project. You may also run::

  sbt

and then, from the ``sbt`` console::
  
  runMain basic.HelloWorld

This will execute a simple script printing (after dumping some rather verbose log information about software updates and compilation) the message ``Hello, World!`` to the output. 

You can now exit ``sbt`` console by typing::

  exit

Finally, you can try to open this project in IntelliJ IDEA via "File -> Open" and choosing the project folder. Click "OK" when asked about initial project settings.
