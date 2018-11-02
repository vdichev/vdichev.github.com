Scala- ADTs and pattern matching
================================


:author: Vassil Dichev
:date: |date|

Using type system
-----------------

  some still seem to equate "the ease of programming" with the ease of making undetected mistakes

  -- Edsger Dijkstra

case classes
------------

* getters

* setters

* toString

* equals

* hashCode

pattern matching
----------------

.. class:: incremental

* wildcards

* constants

* variable

* constructor

* sequence

* tuple

* variable binding

* guards

pattern matching usage
----------------------

* match

* variable assignment

* for expressions

* try / catch

Exercise
--------

* Implement tail-recursive filter and map using pattern matching

Algebraic Data Types
--------------------

* sealed traits

* Product types

  * has-a relationship

* Sum types

  * is-a relationship

Rules of thumb
--------------

* Make illegal states unrepresentable

* Transformations

Replacing null
--------------

* Problems of null

  * Can be a subtype of everything!

  * Is a subtype of everything!

* Option

  * Some(value)

  * None

* Option+

  * Try

  * Either

  * Validation

Exercise
--------

.. code-block:: scala

  option match {
   case None => {}
   case Some(x) => foo(x)
  }

.. class:: incremental

* **Type**: Unit

* option.foreach(foo(_))

Exercise
--------

.. code-block:: scala

  option match {
   case None => Nil
   case Some(x) => x :: Nil
  }

.. class:: incremental

* **Type**: List

* option.toList

Exercise
--------

.. code-block:: scala

  option match {
   case None => false
   case Some(_) => true
  }

.. class:: incremental

* **Type**: Boolean

* option.isDefined

Exercise
--------

.. code-block:: scala

  option match {
   case None => true
   case Some(_) => false
  }

.. class:: incremental

* **Type**: Boolean

* option.isEmpty

Exercise
--------

.. code-block:: scala

  option match {
   case None => None
   case Some(x) => foo(x)
  }

.. class:: incremental

* **Type**: Option

* option.flatMap(foo(_))

Exercise
--------

.. code-block:: scala

  option match {
   case None => None
   case Some(x) => x
  }

.. class:: incremental

* **Type**: Option

* option.flatten

Exercise
--------

.. code-block:: scala

  option match {
   case None => None
   case Some(x) => Some(foo(x))
  }

.. class:: incremental

* **Type**: Option

* option.map(foo(_))

Exercise
--------

.. code-block:: scala

  option match {
   case None => true
   case Some(x) => foo(x)
  }

.. class:: incremental

* **Type**: Boolean

* option.forall(foo(_))

Exercise
--------

.. code-block:: scala

  option match {
   case None => false
   case Some(x) => foo(x)
  }

.. class:: incremental

* **Type**: Boolean

* option.exists(foo(_))

Exercise
--------

.. code-block:: scala

  option match {
   case None => foo
   case Some(x) => Some(x)
  }

.. class:: incremental

* **Type**: Option

* option.orElse(foo)

Exercise
--------

.. code-block:: scala

  option match {
   case None => foo
   case Some(x) => x
  }

.. class:: incremental

* **Type**: type of foo/x

* option.getOrElse(foo)

Additional resources
--------------------

* `Ammonite shell <https://lihaoyi.github.io/Ammonite>`_

* `Scala IDE <http://scala-ide.org/download/sdk.html>`_

* `Scala Fiddle <http://www.scala-js-fiddle.com/>`_

* `Scastie <http://scastie.scala-lang.org/>`_

* `API Docs <http://www.scala-lang.org/api/current/>`_

.. |date| date:: %d.%m.%Y