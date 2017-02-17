Scala- using the type system
============================


:author: Vassil Dichev
:date: |date|

Using type system
-----------------

some still seem to equate "the ease of programming" with the ease of making undetected mistakes

-- Edsger Dijkstra

Algebraic Data Types
--------------------

* sealed traits

* Option

* Try/Either/Validation

Rules of thumb
--------------

* Make illegal states unrepresentable

* Transformations

Currying
--------

* Multiple parameter lists

* Implicits

  * conversions

  * parameters

Typeclass pattern
-----------------

.. class:: incremental

* Ad-hoc polymorphism

* Decouples interface implementation

* When classes not under our control

* When multiple implementations can exist

Additional resources
--------------------

* `Ammonite shell <https://lihaoyi.github.io/Ammonite>`_

* `Scala IDE <http://scala-ide.org/download/sdk.html>`_

* `Scala Fiddle <http://www.scala-js-fiddle.com/>`_

* `API Docs <http://www.scala-lang.org/api/current/>`_

Homework
--------

.. |date| date:: %d.%m.%Y