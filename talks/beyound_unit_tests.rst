Beyound unit testing
====================


:author: Vassil Dichev
:date: |date|

.. footer:: Questers

.. 

  .. header::

    .. image:: images/questers.png
        :class: scale
        :height: 93
        :width: 192

.. |date| date:: %d.%m.%Y

What this talk is about
-----------------------

.. class:: incremental

* Personal account

* Behaviour-driven development

* Property-based/generative testing

What this talk is *not* about
-----------------------------

.. class:: incremental

* Integration/functional/UI testing

* Test processes (test-first)

* Who writes the tests

* Mocks

What we do
----------

* SentimentMetrics

  .. class:: incremental

  * Check what people are saying on social networks about our customers

  * Submit keyword search rules to providers

  * Get back tweets/messages via streaming API

Unit tests
----------

.. list-table::

  * 

    * F

    * Fast

  * 

    * I

    * Isolated

  * 

    * R

    * Repeatable

  * 

    * S

    * Self-verifying

  * 

    * T

    * Timely

Benefits
--------

.. class:: incremental

* Quality assurance

* Documentation

* Design

Drawbacks
---------
      Testing shows the presence, not the absence of bugs
    
      -- Edsger Dijkstra
    

Traps
-----

.. class:: incremental

* Tests can become brittle

* We may forget certain tests

* Tests may become big/unreadable

BDD
---

* Behaviour-driven development

  .. class:: incremental

  * Introduced by Dan North

  * Where to start

  * What (not) to test

  * How much to test

  * How to call the tests

  * Why are tests failing

BDD
---

.. class:: incremental

* Test method names should be sentences

* A simple sentence template keeps test methods focused

* An expressive test name is helpful when a test fails

Types of BDD tests
------------------

* User stories

  * Given

  * When

  * Then

* Specs

Tools
-----

* JBehave

* specs/ScalaTest

JBehave
-------

.. code-block:: java

  @Given("a $width by $height game")
  public void gameIsRunning(int width, int height) {
      game = new Game(width, height);
      renderer = new StringRenderer();
      game.setObserver(renderer);
  }
  @When("I toggle the cell at ($column, $row)")
  public void toggleCellAt(int column, int row) {
      game.toggleCellAt(column, row);
  }
  @Then("the grid should look like $grid")
  public void theGridShouldLookLike(String grid) {
      assertThat(renderer.asString(), equalTo(grid));
  }

Rules
-----

* terms

* OR

* AND

* negation

specs
-----

.. code-block:: scala

  "simple deMorgan -(a or b)" in {
    deMorgan(Neg(Disjunction("A", "B")))
      must beEqualTo(Conjunction(Neg("A"), Neg("B"))
    )
  }
  "simple distributive law (a and (b or c))" in {
    val expr = Conjunction("A",
                           Disjunction("B", "C"))
    distribute(expr) must beEqualTo(
      Disjunction(Conjunction("A", "B"),
                  Conjunction("A", "C"))
    )
  }

Specs report
------------

.. code-block:: text

  Expression generator should
  + separate disjunctions with OR
  + separate conjunctions with space
  + prefix negation with '-'
  + consider proximity distance
  + surround group with parentheses
  + phrase with spaces should be quoted
  + phrase with punctuation or symbols should be
    quoted
  + case sensitivity (^) or wildcard(*) should be
    stripped

Advantages
----------

.. sidebar:: \

  .. image:: images/stay_prepared.jpg
      :class: scale
      :width: 385
      :height: 460

.. class:: incremental

* Readable specification

* Communication

* Drives process via acceptance criteria

* Behaviour from outside (black-box testing)

* Short tests

Effectiveness
-------------
      ...software testing alone has limited effectiveness -- the average defect detection rate is only 25 percent for unit testing, 35 percent for function testing, and 45 percent for integration testing...
      -- Steve McConnel
    

.. Understanding the specification

I like...
---------
      I like tests, especially when someone else has written them.
    

Parameterized tests
-------------------

* @RunWith

* @Parameters

JUnit theories
--------------

* @DataPoint

* @DataPoints

* @Theory

* @ParametersSuppliedBy

JUnit theories
--------------

.. code-block:: java

  @DataPoints
  public static int[] integers() {
    return new int[]{
      0, -1, -10, -1234567,1, 10, 1234567,
      Integer.MAX_VALUE, Integer.MIN_VALUE};}
  
  @Theory
  public void absIsNonNegative(Integer a) {
    assertTrue(abs(a) >= 0);
  }

Property-based/generative
-------------------------

.. sidebar:: \

  .. image:: images/magnifying-glass.jpg
      :class: scale
      :width: 400
      :height: 300

.. class:: incremental

* Generates input

* Calls function/method

* Checks if postconditions hold for output

* Skips if preconditions don't apply

* Shrinks the data to obtain minimal failing result

Frameworks
----------

* QuickCheck

* junit-quickcheck

* jcheck

* quickcheck for Java

* ScalaCheck

.. Similar practices

.. Test generation

.. Fuzz testing

.. Randomized testing

Splitting rules
---------------

.. code-block:: scala

  property("no chunk with more than 10 rules") =
  forAll { (rule: Rule) =>
    Split.tree(rule, None, 10).right forall {
      rs =>
      rs forall (numClauses(_) = 10)
    }
  }
  property("split chunks should be identical to
    normalized ones") =
  forAll { (rule: Rule) =>
    Split.tree(flatten(simplify(rule))).right forall {
      splitRules =>
      Normalize(Disjunction(splitRules: _*)) ==
        simplify(Normalize(rule))
    }
  }

ScalaCheck report
-----------------

.. code-block:: text

  + Normalizer.valid structure:
    OK, passed 100 tests.
  + Normalizer.no chunk with more than 10 rules:
    OK, passed 100 tests.
  + Normalizer.no chunk with more than 1024 size:
    OK, passed 100 tests.
  + Normalizer.split chunks should be identical
      to normalized ones:
    OK, passed 100 tests.
  + Normalizer.split rules are flattened and trimmed
      of single-clause connectives:
    OK, passed 100 tests.

Tradeoffs
---------

.. list-table::

  * 

    * Non-deterministic

    * But checks new input sets every time

  * 

    * Can be slow

    * Is extensive

  * 

    * Need to think

    * You have a detailed spec

  * 

    * You don't have specific tests

    * It's harder to get implementation-dependent

Appropriate for
---------------

.. class:: incremental

* Lots of different input

* Combinatiorial explosion of inputs

* Easy way to specify general properties

* No rampant side effects

Patterns
--------

.. class:: incremental

* Testing inverses

* Testing analogous functions

.. Use cases

.. Volvo

  .. 

.. What doesn't work

.. Copying the implementation

Functional programming
----------------------

* Referential transparency (no side effects)

* Immutability

* Parallelism

.. Images

.. Lense