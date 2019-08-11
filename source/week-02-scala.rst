.. -*- mode: rst -*-

Week 02: Scala Primer
=====================

This lecture is an introduction to Scala programming language. It is
intentionally brief, as all the YSC3248 attendies are assumed to have
familiarity with either OCaml or Java (or both). Therefore, this
tutorial provides a quick overview of Scala's object-oriented and
functional features

The accompanying code for this lecture is available in `this
repository <https://github.com/ysc3248/scala-primer>`_, which also
serves as a template for `Week 2 homework assignment
<_static/resources/programming-01.pdf>`_.

If unsure about some of the feature, you are encouraged to take a look
at one of multiple Scala tutorials available online. The following are
the recommended ones:

* `All about Scala <http://allaboutscala.com/#scala-introduction>`_
* `Scala for Java programmers <https://docs.scala-lang.org/tutorials/scala-for-java-programmers.html>`_

Using IntelliJ IDEA
-------------------

We will be using IntelliJ IDEA as an Integrated Development
Environment (IDE) for programming in Scala. It will allow us to manage
large multi-file projects with multiple executables and automated
tests. The following link provides instructions on getting IntelliJ
and creating a simple Scala project in it:

* `Getting Started with Scala in IntelliJ IDEA <https://docs.scala-lang.org/getting-started/intellij-track/getting-started-with-scala-in-intellij.html>`_

You can also open the `accompanying project
<https://github.com/ysc3248/scala-primer>`_ from IntelliJ via `File`
-> `Open` dialogue. 

IntelliJ IDEA provides a convenient way to build projects, navigate to
files and definitions, and refactor them consistently. You are
encouraged to `this tutorial
<http://allaboutscala.com/tutorials/chapter-1-getting-familiar-intellij-ide/scala-tutorial-first-hello-world-application/>`_
to master the following aspects of using IntelliJ for managing Scala
projects:

* Creating new files
* Using code completion
* Building and rebuilding the project
* Navigating to definitions and files (see the menu Navigate)
* Creating runtim configurations

Use this `key binding reference
<https://resources.jetbrains.com/storage/products/intellij-idea/docs/IntelliJIDEA_ReferenceCard.pdf>`_
for your convenience. Alternatively, just remember how to invoke the
`Find Action` dialogue (Ctrl + Shift + A or Command + Shit + A,
depending on the system) and type in your query to get a hint.

The following simple executable is implemented in the file
``SquareOf5.scala`` (use IntelliJ navigation to locate it!)::

 object SquareOf5 extends App {
   def square(x: Int) = x * x
   val s = square(5)
   println(s"Result $s")
 }

To run it in the IDE, right-click on ``SquareOf5`` in the editor (or
on the file in the navigator tree pane on the left of the editor) and
choose `Run 'SquareOf5'`. Alternatively, you can click on the green
triangle next to the object definition. The result of executing the
program will appear in the execution pane at the bottom of the screen.

An alternative way to define an executable ``object`` is via the
``main`` method. For instance, it can be done as follows::

 object SquareOf6 {
   def main(args: Array[String]): Unit = {
     val s = SquareOf5.square(6)
     println(s"Result $s")
   }  
 }

Here, the executable object ``SquareOf6`` uses the function ``square``
defined within the object ``SquareOf5``.

Using SBT
---------

Scala Build Tool is a build system used to manage dependencies and
compile Scala projects, similar to OCaml's ``dune`` and ``opam``. The
tutorial on obtaining and running ``sbt`` is available:

* `Getting Started with Scala and SBT on the Command Line <https://docs.scala-lang.org/getting-started/sbt-track/getting-started-with-scala-and-sbt-on-the-command-line.html>`_

You can try executing ``sbt test`` from the root of the primer
project. This will compile it and automatically run all the tests in
the project.

Object-Oriented Elements of Scala
---------------------------------

Scala inherits many object-oriented features from languages such as
C++ and Java. That said, it's object-oriented model can still be
understand in terms of OCaml abstractions. Definitions of functions
and data types in Scala can be placed in either of the module-like
environments:

`Objects` are similar to OCaml's first-order modules. They may contain
data type definitions, functions and mutable references.
Each object is unique, hence all values in it are global. Examples
of objects are shown above. Objects are the "final" units of any
Scala project: all executable code is run starting from some
object's ``main`` method (or is an object is defined as ``extends App``)
as demonstrated above.

`Classes` are "factories" of objects. Similarly, they may contain
definitions of functions (called `methods` in Scala), as well as
data types. However, each class can be used to create multiple
`instances`, each having its own state (including mutable variables,
called `fields`). For instance, the following class features one
mutable field ``greeting`` and three methods::

  class Printer(val initial: String) {
    private var greeting = initial

    def printMessage(): Unit = println(greeting + "!")

    def printNumber(x: Int): Unit = {
      println("Number: " + x)
    }

    def setGreeting(s: String) = {
      greeting = s
    }
  }

It takes a value of type ``String``, which can be then used within the
body of the class. For instance, it is used to initialise a mutable
field ``greeting``. It can be later changed via a method
``setGreeting`` by passing a new ``String`` value. The class can be
then `instantiated` and used as follows::

 object UsePrinter {
   def main(args: Array[String]): Unit = {
     val printer = new Printer("Hello")
     printer.printMessage()
     printer.printNumber(42)
   }
 }

`Traits` in Scala are used as "templates" containing some data
types, fields, and methods, which can be used to "mix-in" to classes
and objects that are create later. Traits cannot be instantiated or
executed: they should be considered as "dictionaries" of definitions
to be used by classes and objects. The following example shows a
trait, a class that extends it, and an object that uses the
resulting class::

  trait Logging {
    // Signature of a method to be defined later 
    def log(s: String): Unit

    def warn(s: String) = log("WARN: " + s)

    def error(s: String) = log("ERROR: " + s)
  }


  // A class that mixes in Logging's functionality
  class PrintLogging extends Logging {
    def log(s: String) = println(s)
  }

  object UseLogging extends App {
    val logger = new PrintLogging
    logger.warn("Hmm...")
  }

  One class and object can extend multiple traits. In addition, an
  object and a class can extend precisely one class. 

More details on object-oriented model of Scala can be found in the
following tutorials:

* `Scala Classes and Objects
  <https://www.tutorialspoint.com/scala/scala_classes_objects>`_
* `Scala Traits <https://www.tutorialspoint.com/scala/scala_traits.htm>`_

Classes, objects and traits in Scala are located under a source root
in a hierarchy of folders that correspond to `packages`. Packages are
declared at the beginning of each file and should mimic the folder
hierarchy (), for instance::

  package runners.squares

is a package ascribed to ``SquareOf5`` and ``SquareOf6`` objects that
are located in a folder ``runners/squares`` under the source root of a
project.

Classes and traits in scala can be `polymorphic`, i.e., taking type
parameters. For instance, the following class corresponds to OCaml's
polymorphic ``pair`` data type with `immutable` fields ``first`` and
``second`` or arbitrary types ``P`` and ``Q``::

 class Pair[P, Q](val first: P, val second: Q)

 object UsePair extends App {
   val p = new Pair("abc", 42)
   println(p.first)
   println(p.second)
 }

Functional Elements of Scala
----------------------------

Scala allows to define classes in a way that they could be used in a
pattern matching, similar to OCaml's data types. For this, they need
to be defined using the keyword ``case``. The typical pattern is to
define a trait that corresponds to the "abstract data type" and a
number of case classes that extend it. For instance, this is how the
familiar option type is implemented in Scala (ignore the ``+`` in
front of the type parameter for now)::

 trait Option[+T]

 case class Some[T](elem: T) extends Option[T]

 case object None extends Option[Nothing]

Notice that ``None`` is defined as an object, since it doesn't take
any parameters, and hence should only exist as a single instance. This
is how case classes are used in pattern matching::

 object PrintOption {

   def printOption(o: Option[String]): Unit = {
     o match {
       case Some(e) => 
         println("Some: " + e) 
       case None => 
         println("Nothing!")
     }
   }

   def main(args: Array[String]): Unit = {
     val s = Some("Hello")
     printOption(s)
   } 
 }

Scala has support for first-class functions-as-values. The following
code snippet declares a lambda-expressions for multiplying a number by
two::

  val twice: Int => Int = (x: Int) => x * 2

Notice that it is ascribed the type ``Int => Int``. However, the compiler can
infer this type automatically cased on the argument type of ``x``,
hence we can shorten the definition and write in one of the two
following ways::

  val twice = (x: Int) => x * 2

or::

  val twice: Int => Int = x => x * 2

First-class functions allow manipulating blocks of code as if they
were first-class values. For instance, the following example uses
`lazy` (by-name) parameter to declare a run-twice method, which runs
the specified block of code ``body`` twice::

  def runTwice(body: =>Unit): Unit = {
    body
    body
  }

  // This will print Hello twice.
  runTwice ({
    println("Hello!")
  })

Scala provides ``for``-expressions as a convenient way to travers and
transform collections. For instance, the following loop prints all
elements of a list ``ls``::

    val ls = List(1, 2, 3, 4)
    for (e <- ls) {
      println(e)
    }

The standard functions on collections, such as ``map``, ``foldLeft``,
``filter`` etc. are all available as methods of the corresponding data
types. For instance, the following code prints the list that is
obtained by multiplying all elements of ``ls`` by 3::

  println(ls.map(x => x * 3))

Notice that the parameter type of ``x`` of the function passed to
``map`` is inferred from the type of ``map`` itself and does not have
to be declared explicitly.

Scala features both immutable (purely functional) and mutable
collections. All collections mix-in the functionality from the
``Seq[T]`` trait of generic collections of elements of type ``T``.
Concrete collections can be created and manipulated as follows::

  val messages : Seq[String] = Seq("Hello", "World", "!")
  val messageMap : Map[Int, String] = Map(1 -> "Hello", 2 -> "World", 3 -> "!")
  
  // Convert all elements of `messages` to strings (which they already are), 
  // concatenate with the " " as a separator and print the result:
  println(messages.mkString(" "))
  
  //Create a new map by adding a key-value pair (4 -> "Yay") to messageMap
  println(messageMap + (4 -> "Yay"))

We recommend to use IntelliJ auto-completion to discover available
methods for different data types. The following tutorial provides a
great overview of Scala collections:

* `Scala Collections <https://www.tutorialspoint.com/scala/scala_collections>`_

Imperative elements of Scala
----------------------------

Scala allows one to use arrays in the same way one uses them in OCaml
and Java. The code below shows some examples of creating using arrays::

 object ArrayExample {

   var index = 0
   val nextIndex = () => {
     val tmp = index
     index = index + 1
     tmp
   }

   def main(args: Array[String]): Unit = {

     // Create an array of booleans of size 5
     val arr1 = new Array[Boolean](5)

     // Print all elements of the array
     for (i <- 0 to arr1.length - 1) {
       println(arr1(i))
     }

     // Create an array of size 5 filled by repeating the computation
     // passed as a second parameter
     val arr2 = Array.fill(5)({ nextIndex() * nextIndex() })

     // Print all elements of this array
     for (i <- arr2.indices) {
       println(arr2(i))
     }     
   }
 }

The following reference provides a brief guide on using
arrays in conjunction with other Scala collections:

* `Scala arrays
  <https://docs.scala-lang.org/overviews/collections/arrays.html>`_

Working with Threads in Scala
-----------------------------

TODO: Examples

TODO: Difference between run and start

Writing Automated Tests in Scala
--------------------------------

TODO

Homework
--------

* `Programming Assignment 1 <_static/resources/programming-01.pdf>`_
