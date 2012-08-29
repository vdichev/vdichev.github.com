Scala for Java developers
=========================



:author: Vassil Dichev
:date: |date|

.. header::

  .. image:: images/java2days.png
    :class: scale
    :height: 73
    :width: 259

.. footer:: 2011 Java2Days Conference | 3-4 November, Sofia, Bulgaria | www.java2days.com

.. |date| date:: %d.%m.%Y

Stairway to Scala
-----------------

.. class:: incremental

* J2EE / Spring

* Python/Ruby

* Apache ESME and Lift open-source projects

* Remember The Milk

Java releases
-------------

* JDK 1.0 (January 23, 1996)

* JDK 1.1 (February 19, 1997)

* J2SE 1.2 (December 8, 1998)

* J2SE 1.3 (May 8, 2000)

* J2SE 1.4 (February 6, 2002)

* J2SE 5.0 (September 30, 2004)

* Java SE 6 (December 11, 2006)

* Java SE 7 (July 28, 2011)

* Java SE 8 (2013?)

Next?
-----

.. class:: huge center

  Java 9 is already released. It's called Scala

Meet Martin Odersky
-------------------

.. sidebar:: \ 

  .. image:: images/martin_odersky.jpg
    :class: scale
    :width: 166
    :height: 256
    :align: center

.. en.wikipedia.org > Wiki > File:Mark Odersky photo by Linda Poeng

* Java generics

* javac compiler

* Fusing FP and OOP together

  * Pizza

  * Scala

* Founder of Typesafe

Why learn Scala?
----------------

.. class:: incremental

* Fun

* Productive

* Educational

* Influential

Quotes
------

.. 

  If I were to pick a language to use today other than Java, it would be Scala
  
  -- James Gosling

.. 

  [...] if someone had shown me the Programming in Scala book [...] I'd probably have never created Groovy.
  
  -- James Strachan

.. 

  If you need to use Java, you should be using Scala.
  
  -- Gilad Bracha

Scala is
--------

.. class:: incremental

* Object-oriented

* Functional

* Static typing

* JVM

Dynamic?
--------

.. class:: incremental

* no type annotations

* REPL

* Duck typing

.. Things you can go without

.. semicolons

.. public

.. final

.. return

.. dot

.. parentheses

Java 5
------

.. class:: incremental

* Generics

* Enhanced for loop

* Autoboxing/unboxing

* Enums

* Annotations

* Static imports

Generics
--------

* Java

  .. code-block:: java

    Map<Integer,String> digits =
        new HashMap<Integer,String>();
    digits.put(Integer(1), "one");
    digits.put(Integer(2), "two");

* Scala

  .. code-block:: scala

    // val means "public final"
    val digits = Map(1 -> "one", 2 -> "two")
    // no semicolons

For Loop
--------

* Java

  .. code-block:: java

    for (Map.Entry<Integer,String> entry:
         digits.entrySet()) {
        System.out.println(entry.getKey()
                  + ": " + entry.getValue());
    }

* Scala

  .. code-block:: scala

    for ((key, value) <- digits)
      println(key + ": " +  value)

Autoboxing
----------

* Java

  .. code-block:: java

    digits.put(1, "one");

* Scala

  .. code-block:: scala

    // no primitive types!
    1.to(3)
    // equivalent to
    1 to 3

Enums
-----

* Java

  .. code-block:: java

    enum Color { RED, GREEN, BLUE}
    switch (c) {
        case RED: ...
        case GREEN: ...
    }

Sealed traits
-------------

* Scala

  .. code-block:: scala

    sealed trait Color
    object Red extends Color
    object Green extends Color
    object Blue extends Color
    color match {
      case Red => ...
      case Green => ...
      // compiler warning- Blue
    }

Annotations
-----------

* Java

  .. code-block:: java

    @Column(name ="user",
            nullable = false,
            updatable = false)

* Scala

  .. code-block:: scala

    @Column(name ="user",
            nullable = false,
            updatable = false)
    val duke = new Mascot(name = "Duke",
                           age = 15)

Annotations
-----------

* Java

  .. code-block:: java

    @Override public String toString() {
        return "test";
    }

* Scala

  .. code-block:: scala

    // don't need return statement
    override def toString = "hey"

Static imports
--------------

* Java

  .. code-block:: java

    import static java.lang.System.out
    out.println("hey")

* Scala

  .. code-block:: scala

    import java.lang.System.out._
    import java.sql.{Date=>SqlDate}
    import duke._
    println("name: " + name + ", age: " + age)

Java 7
------

.. class:: incremental

* Strings in switch

* Type inference

* Automatic resource management (ARM)

* Multi-catch

Type inference
--------------

* Java

  .. code-block:: java

    Map<> digits = new HashMap<Integer,String>();

* Scala

  .. code-block:: scala

    val conference = "Java2Days"
    val num = 42
    val digits = Map(1 -> "one", 2 -> "two")

Strings in switch
-----------------

* Java

  .. code-block:: java

    switch s {
      case "one": out.println(1)
    }

* Scala

  .. code-block:: scala

    myVar match {
      case 1 => "int 1"
      case "one" => "string one"
      case s: String => "string: " + s
      case Array(1, _*) =>
        "array starting with 1"
      case _ => 
    }

Multi-catch
-----------

* Java

  .. code-block:: java

    try {...
    } catch (ConnectException |
        SocketException ex) {

* Scala

  .. code-block:: scala

    try {...} catch {
      case net: SocketException |
                 ConnectException => ...
      case e: Exception => e.printStackTrace
    }

Automatic resource management
-----------------------------

* Java

  .. code-block:: java

    try (BufferedReader br =
         new BufferedReader(new FileReader(path)) {
        return br.readLine();
    }

* Scala

  .. code-block:: scala

    using(new BufferedReader(
            new FileReader("file.txt"))) {
      f => println(f.readLine)
    }

Implementing ARM
----------------

.. code-block:: scala

  def using[T<:{def close()}]
          (resource: T)
          (block: T => Unit) {
    try {
      block(resource)
    } finally {
      if (resource != null) resource.close()
    }
  }

Java 8- lambda expressions
--------------------------

* Java

  .. code-block:: java

    x -> x + 1
    (int x) -> x + 1

* Scala

  .. code-block:: scala

    (x: Int) => x + 1
    x => x + 1
    _ + 1
    (1 +)

Consistency
-----------

* Pattern matching

  .. code-block:: scala

    entry match {
      case (key, value) => println(key, value)
    }
    val (key, value) = getEntry
    for ((key, value) <- digits)
      println(key + ": " +  value)

* No primitives

* Arrays are collections

Is Scala the next Java?
-----------------------

.. class:: huge center incremental

  No

.. class:: incremental

* Different patterns

* Java's not going anytime soon

* Age of polyglotism- best tool for the job

Change in thinking
------------------

* Scala is fun(ctional)

  .. code-block:: scala

    for (i <- 1 to 100 if i % 2 == 0
    ) yield (i * 3)

* Scala is parallel

  .. code-block:: scala

    for (i <- (1 to 100).par if i % 2 == 0
    ) yield i * 3

Learning Scala
--------------

.. class:: borderless

.. list-table::

  * 

    * 

      .. image:: images/BeginningScala.gif
        :class: scale
        :align: center
        :width: 86
        :height: 114

    * Beginning Scala

    * 

      * David Pollak

  * 

    * 

      .. image:: images/ProgrammingInScala.gif
        :class: scale
        :align: center
        :width: 91
        :height: 118

    * Programming in Scala

    * 

      * Martin Odersky

      * Bill Venners

      * Lex Spoon

  * 

    * 

      .. image:: images/ProgrammingScala.gif
        :class: scale
        :align: center
        :width: 90
        :height: 117

    * Programming Scala

    * 

      * Alex Payne

      * Dean Wampler

Using Scala
-----------

* Testing

  * Behaviour-driven development (specs)

* Concurrency library

  * Akka

* Distributed software

  * Akka

* RESTful APIs

  * Unfiltered