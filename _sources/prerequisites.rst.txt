.. -*- mode: rst -*-

Software Prerequisites
======================

We will be using `Scala <https://www.scala-lang.org/>`_ (Version 2) as
a main programming language for this course.

The setup outlined below has been tested on Windows 11 and macOS (for
both Intel and Apple silicon chips). If you experience issues at any
stage of the setup, please refer to the **Troubleshooting** section
below.

Getting Scala and IntelliJ
--------------------------

In your preparation for the first lecture, please install the following software artefacts (or make sure that you have them installed in your system):

* `Oracle Java SDK 11 <https://www.oracle.com/sg/java/technologies/javase/jdk11-archive-downloads.html>`_.
  You will need to make an Oracle account to download the latest version.
* `Scala Build Tool (sbt) <https://www.scala-sbt.org/download.html3>`_
* `IntelliJ IDEA <https://www.jetbrains.com/idea/>`_. When you start IntelliJ for the first time, make sure to choose Scala plugin when IntelliJ IDEA suggests you to download featured plugins.
* `Scala plugin for IntelliJ IDEA <https://www.jetbrains.com/help/idea/discover-intellij-idea-for-scala.html>`_ (if not installed in the previous step)

..
   All these components can be found at the `Scala 2 Download page  <https://www.scala-lang.org/download/scala2.html>`_.

This setup has been last checked with ``sbt`` version 1.6.2 and
IntelliJ IDEA 2022.1.3.

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

The code appearing in the lectures will be collected in this `repository with examples <https://github.com/ysc4231/lectures-2022>`_.  In order to be able to access it, please, make sure to email your GitHub name to the instructor---this is necessary to grant you GitHub access for course-related repositories.

To check your Scala setup, clone this project from GitHub (via ``git@github.com:ysc4231/lectures-2022.git``). Next, try to execute the following two commands in the terminal from the root of your project (it will take a few minutes the first time you run it, as ``sbt`` needs to download all the dependencies)::

  sbt test

will run the tests in the project. You may also run::

  sbt

and then, from the ``sbt`` console::
  
  runMain basic.HelloWorld

This will execute a simple script printing (after dumping some rather verbose log information about software updates and compilation) the message ``Hello, World!`` to the output. 

You can now exit ``sbt`` console by typing::

  exit

Finally, you can try to open this project in IntelliJ IDEA via "File -> Open" and choosing the project folder. Click "OK" when asked about initial project settings.

Troubleshooting
---------------

1. **Problem**: I am trying to open the project in IntelliJ IDEA for
   the first time, and, while importing it via ``sbt``, it fails with
   an error::

    Extracting structure failed: Build status: Error
    sbt task failed, see log for details

   This problem has been detected on macOS.

   **Solution**: Close the project (via ``File -> Close Project``),
   then follow the instructions `here
   <https://www.jetbrains.com/help/idea/bsp-support.html>`_ to import
   the project using BSP instead of SBT. The instructions there are
   given for macOS; on Windows, the first action dialogue shortcut is
   ``Ctrl+Shift+A``.

2. **Problem**: Opening the project for the first time in IntelliJ
   fails with a pop-up notification::

     sbt import cancelled: Cannot run program

   This problem has been observed on Windows 11.

   **Solution** Open ``File -> Project Structure``, category ``Project Settings -> Project``
   and sekect a Java SDK (e.g. OpenJDK version 11.0.5 or similar one)
   from what's already installed at your system.
