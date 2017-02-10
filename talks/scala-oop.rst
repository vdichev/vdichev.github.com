Scala- OOP support
==================


:author: Vassil Dichev
:date: |date|

What is OOP anyway?
-------------------
      I invented the term Object-Oriented, and I can tell you I did not have C++ in mind — Alan Kay
    

Outside view
------------

.. class:: incremental

* Classes

* Singletons

* Abstract classes

* Traits

Extending and mixins
--------------------

.. sidebar:: \

  .. image:: images/Diamond_inheritance.png
      :class: scale
      :width: 200
      :height: 300
      :align: center

.. class:: incremental

* Extending classes or traits

  * extends

* Mixing in traits

  * with

Inside view
-----------

.. class:: incremental

* Fields

* Methods

* Uniform Access Principle

* Constructors

  * primary

  * auxiliary

Methods
-------

.. class:: incremental

* Named and default parameters

* Overloading

* Overriding

Visibility
----------

.. class:: incremental

* public (default)

* protected

* private

Discussion
----------

* Use inheritance wisely

* Avoid mutability

imports
-------

* on-demand

* selector

* renaming

Additional resources
--------------------

* `Ammonite shell <https://lihaoyi.github.io/Ammonite>`_

* `Scala IDE <http://scala-ide.org/download/sdk.html>`_

* `Scala Fiddle <http://www.scala-js-fiddle.com/>`_

* `API Docs <http://www.scala-lang.org/api/current/>`_

Homework
--------

* Write an object that extends a trait

* Do you think a trait can extend a class? What would that accomplish?

* What do you think happens when a method with default parameters conflicts an overloaded method?

* Can a val override a def? What about the reverse? Why?

* Define Java's package-private visibility using Scala's modifiers

.. |date| date:: %d.%m.%Y