Scala- useful typeclasses
=========================


:author: Vassil Dichev
:date: |date|

Goals
-----

* Read code

* Study laws

* Type-driven development

What can these functions do?
----------------------------

.. code-block:: scala

  def f1[A](l: List[A]): Int
  
  def f2[A](l: List[A]): List[A]

Typeclasses
-----------

* Semigroup

* Monoid

* Functor

* Monad

Scary names...
--------------

  Scary names like Semigroup, Monoid, Magma etc. were invented by lonesome mathematicians to describe simple things and intimidate other people, probably as an act of revenge for not being invited to parties.

  -- Andrey Skorikov

Semigroup
---------

.. code-block:: scala

  // Scalaz
  def append(a1: A, a2: => A): A
  
  // Cats
  def combine(x: A, y: A): A

Semigroup syntax
----------------

.. code-block:: scala

  // Scalaz
  def |+|(other: => F): F
  def mappend(other: => F): F
  def ⊹(other: => F): F
  
  // Cats
  def |+|(rhs: A): A
  def combine(rhs: A): A

Semigroup laws
--------------

.. code-block:: scala

  // associativity
  (x |+| y) |+| z == x |+| (y |+| z)

Monoid
------

.. code-block:: scala

  // Scalaz
  def zero: A
  
  // Cats
  def empty: A

Monoid laws
-----------

.. code-block:: scala

  // left identity
  Monoid[A].empty |+| x == x
  
  // right identity
  x |+| Monoid[A].empty == x

Task
----

* Write a function sum which takes (at least) a list of monoids and combines all of them. You can either implement the monoid typeclass yourself or import it from Cats by using an sbt project with this dependency:

  * `libraryDependencies += "org.typelevel" %% "cats" % "0.9.0"`

Functor
-------

.. code-block:: scala

  def map[A, B](fa: F[A])(f: A => B): F[B]

Functor syntax
--------------

.. code-block:: scala

  def map[B](f: A => B): F[B]

Functor laws
------------

.. code-block:: scala

  // identity
  (x map identity) == x
  
  // associativity
  (x map (f map g)) ==
    (x map f map g)

Monad
-----

.. code-block:: scala

  // Scalaz
  def point[A](a: => A): M[A]
  def bind[A, B](a: M[A], f: A => M[B]): M[B]
  
  // Cats
  def pure[A](x: A): F[A]
  def flatMap[A, B](fa: F[A])(f: A => F[B]): F[B]

Monad Laws
----------

.. code-block:: scala

  // left identity
  (Monad[F].pure(x) flatMap {f}) == f(x)
  
  // right identity
  (m flatMap {Monad[F].pure(_)}) == m
  
  // associativity
  (m flatMap f) flatMap g ==
    m flatMap { x => f(x) flatMap {g} }

Usage
-----

* Monoids- folds

* Functors- independent operations

* Monads- dependent operations

Additional resources
--------------------

* `Ammonite shell <https://lihaoyi.github.io/Ammonite>`_

* `Scala IDE <http://scala-ide.org/download/sdk.html>`_

* `Scala Fiddle <http://www.scala-js-fiddle.com/>`_

* `Scastie <http://scastie.scala-lang.org/>`_

* `API Docs <http://www.scala-lang.org/api/current/>`_

.. |date| date:: %d.%m.%Y