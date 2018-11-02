Scala- implicits and the typeclass pattern
==========================================


:author: Vassil Dichev
:date: |date|

Functions and data
------------------

  It is better to have 100 functions operate on one data structure than 10 functions on 10 data structures

  -- Alan Perlis

Functions and data abstraction
------------------------------

  It is better to have 100 functions operate on one **data abstraction** than 10 functions on 10 data structures.

  -- Rich Hickey (creator of Clojure)

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

Implicits
---------

* Not applied if code typechecks

* implicitNotFound for error messages

* can be disabled by hiding import or via style plugin

* -Xprint:typer option

* resolution rules

Implicit resolution rules
-------------------------

* current scope

* imports

* companion objects

* parameter arguments

* type parameters

* outer objects of nested types

* parent objects

Additional resources
--------------------

* `Ammonite shell <https://lihaoyi.github.io/Ammonite>`_

* `Scala IDE <http://scala-ide.org/download/sdk.html>`_

* `Scala Fiddle <http://www.scala-js-fiddle.com/>`_

* `Scastie <http://scastie.scala-lang.org/>`_

* `API Docs <http://www.scala-lang.org/api/current/>`_

.. |date| date:: %d.%m.%Y