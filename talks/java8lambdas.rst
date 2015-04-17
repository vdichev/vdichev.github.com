Java 8 Lambdas
==============


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

Who am I
--------

* Scala

  * SentimentMetrics

  * RememberTheMilk

* Java

  * Spring

  * J2EE

Java 8 lambdas history
----------------------

.. class:: incremental

* 2006- First closure proposal by Neal Gafter

* 2007- 3 closure proposals

* 2009

  * Sun bought by Oracle

  * Mark Rheinhold announces return of closures at Devoxx

  * JSR 335 starts

* 2010- Lambdas delayed for Java 8

* 2013- Java 8 delayed

Survey
------

.. image:: images/survey3.png
    :class: scale
    :width: 800
    :height: 400

Evolution of paradigms
----------------------

* GOTO → structured programming

* Manual memory management → Garbage collection

* Imperative programming → Functional programming

Functional programming
----------------------

* Correctness

* Compositionality

* Parallelization

Java before 1.4
---------------

.. code-block:: java

  int sum = 0;
  for (int i = 0;
       i < employees.length;
       i++) {
    sum += employees[i].getSalary();
  }

.. image:: images/chain.jpg
    :class: scale
    :width: 201
    :height: 278

Enhanced for loop
-----------------

.. code-block:: java

  int sum = 0;
  for (Employee employee: employees) {
    sum += employee.getSalary();
  }

Enhanced loop decompiled
------------------------

.. code-block:: java

  int sum = 0;
  for (Iterator<Employee> iter =
         employees.iterator();
       iter.hasNext();) {
    Employee employee = iter.next();
    sum += employee.getSalary();
  }

Internal/External Iteration
---------------------------

.. image:: images/internal_external_iteration.png
    :class: scale
    :width: 740
    :height: 512

.. Use cases

.. Callbacks

  * UI listeners

.. Parallel and concurrent processing

.. DSLs

Lambdas
-------

.. 

* Parameters

* arrow ->

* Body

.. code-block:: java

  (int x, int y) -> { return x + y; };
  (int x, int y) -> { x + y; };
  (x, y) -> x + y;
  x -> 2 * x;
  () -> out.println("hey")

Functional interfaces
---------------------

.. code-block:: java

  interface Runnable {
    void run();
  }
  interface Callable<V> {
    V call();
  }
  interface Comparator<T> {
    int compare(T o1, T o2);
  }
  interface FileFilter {
    boolean accept(File path);
  }
  interface ActionListener {
    void actionPerformed(ActionEvent e);
  }

Concurrent
----------

.. code-block:: java

  // Anonymous Runnable
  Runnable r1 = new Runnable(){
  
    @Override
    public void run(){
      out.println("Hello 1!");
    }
  };
  
  // Lambda Runnable
  Runnable r2 = () -> out.println("Hello 2!");
  //            ↓          ↓
  //    parameters        body

Method references
-----------------

.. code-block:: java

  Runnable r =
    () -> out.println("Hey!");
  Callable<Void> c =
    () -> out.println("Hey!");
  class Message {
    static void hey() {
      out.println("Hey");
    }
  }
  Runnable r = Message::hey;
  Callable<Void> c = Message::hey;

Method reference types
----------------------

* Static

* Instance

  .. code-block:: java

    (str, i) -> str.substring(i);
    String::substring

* Instance of specific object

  .. code-block:: java

    DateFormat format =
      new DateFormat.getDateInstance();
    (str) -> format.parse(str);
    format::parse

GUI
---

.. code-block:: java

  button.addActionListener(new ActionListener(){
    @Override
    public void actionPerformed(ActionEvent ae){
      out.println("Anon Class");
    }
  });
  
  button.addActionListener(
      e -> out.println("Lambda Listener"));
  //  ↓          ↓
  // parameters body

Variable capture
----------------

.. code-block:: java

  int sum = 0;
  employees.stream().
            forEach(e -> sum += e.getSalary());
  // COMPILER SAYS NO!

Common patterns
---------------

* Consumer- void result

* Supplier- no arguments

* Predicate- boolean result

* Function- generic function

* BiFunction- two arguments

* Higher-order functions- argument or result is a function

.. Restrictions

.. Can't assign across different functional interfaces

.. (effectively) final

Filter
------

.. image:: images/filter.png
    :class: scale
    :width: 640
    :height: 310

Map
---

.. image:: images/map.png
    :class: scale
    :width: 640
    :height: 305

Reduce
------

.. image:: images/reduce.png
    :class: scale
    :width: 640
    :height: 320

.. Using lambdas

.. Functional interfaces

.. Method references

Streams
-------

.. sidebar:: \

  .. image:: images/stream6.jpg
      :class: scale
      :width: 400
      :height: 300

* Lazy

  * Intermediate operations

  * Terminal- enforce strictness

* Traversible only once

* Short-circuiting

Loop with streams
-----------------

.. code-block:: java

  employees.stream().
            filter(e -> e.getAge() > 30).
            map(Employee::getSalary).
            reduce(Integer::sum)

Parallel streams
----------------

.. code-block:: java

  employees.parallelStream().
            filter(e -> e.getAge() > 30).
            map(Employee::getSalary).
            reduce(Integer::sum)

Intermediate methods
--------------------

* filter

* distrinct

* skip

* limit

* map

* flatMap

* sorted

Terminal
--------

* anyMatch, noneMatch, allMatch

* findAny, findFirst

* forEach

* collect

* reduce

* count

.. Compatibility with pre-Java-8 libraries

.. Implementations of Lambdas on the JVM

.. invokedynamic

Default methods
---------------

.. code-block:: java

  default void sort(Comparator<? super E> c){
    Collections.sort(this, c);
  }

Default methods resolution
--------------------------

* Classes always win

* More specific interface wins

* Disambiguate

  .. code-block:: java

    class implements B, A {
      void hello() {
        B.super.hello();
      }
    }

Scala
-----

.. code-block:: scala

  List(1, 2, 3).filter(_ % 2 == 0)
  List(1, 2, 3).map(_ * 2)
  List(1, 2, 3).reduce(_ + _)

Clojure
-------

.. code-block:: clojure

  (filter #(= (mod % 2) 0) '(1 2 3))
  (map #(* 2 %) '(1 2 3))
  (reduce + '(1 2 3))

Groovy
------

.. code-block:: groovy

  [1, 2, 3].findAll { it % 2 == 0 }
  [1, 2, 3].collect { it * 2}
  [1, 2, 3].inject { acc, val -> acc + val } 

Ruby/JRuby
----------

.. code-block:: ruby

  [1, 2, 3].select { |num| num.even? }
  [1, 2, 3].collect { |num| num * 2 }
  [1, 2, 3].inject(:+)

Python/Jython
-------------

.. code-block:: python

  list(filter(lambda x: x % 2 == 0, [1, 2, 3]))
  list(map(lambda x: x * 2, [1, 2, 3]))
  reduce(lambda x, y: x + y, [1, 2, 3])

JavaScript
----------

.. code-block:: javascript

  [1, 2, 3].filter(function (el) {
    return el % 2 == 0;
  });
  [1, 2, 3].map(function (el) {
    return 2 * el;
  });
  [1, 2, 3].reduce(function (prev, curr) {
    return prev + curr;
  });

Where to next?
--------------

.. image:: images/urma_cover150.jpg
    :class: scale
    :width: 300
    :height: 376

Evolution?
----------
      Every C# developer should really try #Scala. You won't look back. I promise.
    
      -- Erik Meijer
    