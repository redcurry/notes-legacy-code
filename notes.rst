Working Effectively with Legacy Code
====================================

Sprout Method and Sprout Class
------------------------------

* Do not make extensive changes to existing code,
  but try to put new code in a new method or class

* Use a class when the new code adds a responsibility

* Unit test the new class as it's developed

Wrap Method
-----------

* Just because two pieces of code must happen at the same time
  doesn't mean they should be coupled together

* When new code must happen before or after existing code,
  put the new code in a new method, then rename the existing method,
  and then create a new method (called like the old method) that calls
  the old method and the new method (before or after)

* Alternatively, create a new method that calls the old code
  and the new code, leaving the old method intact

Wrap Class
----------

* Use the decorator pattern to add functionality, but use sparingly

* Another way is to create a class that accepts the original class,
  then a method in the new class calls the original class's method,
  and then calls the new functionality (in a new method)

Chapter 7
---------

* Break up software into small, well-named, understandable pieces

* You should be able to compile every class or module in your system
  separately from the others and in its own test harness

* The first step in breaking a dependency is to try to instantiate
  the class (or classes in a cluster) in question in a test harness

* Look at everything that depends on the class(es) in question
  (used outside of the cluster of classes),
  then extract an interface for the class(es) and use those instead
  (Dependency Inversion)

* Move the class(es) to a new library

Chapter 8
---------

* Steps in TDD:

  1. Write a failing test
  2. Get it to compile
  3. Make it pass
  4. Remove duplication (or refactor)
  5. Repeat

* One way to quickly test and implement a new feature
  is to derive from the original class and override
  the method with the functionality of interest

* Then, refactor the classes to get rid of the inheritance,
  which can be problematic if used a lot

* According to the Liskov Substitution Principle (LSP),
  objects of subclasses should be substitutable for objects
  of their superclasses

* To help follow LSP, do not override concrete methods
  (those that already contain code); instead, override abstract methods

Chapter 9
---------

Constructors
............

* For constructor with many parameters, you can
  replace with an interface (create one, if necessary),
  or pass null

  - Me: But passing null may fail if ctor checks for it

* If the constructor of a class instantiates an object
  (a hidden dependency), you can create a new constructor
  that takes an instance of the dependency (or an interface),
  and have the original constructor call that with a new object.
  Your test code can call the new constructor with a fake,
  while the production code continues to call the original ctor.

* Another solution is to let the constructor create the object,
  but then replace it by creating a new method that replaces it

Singletons
..........

* When working with a singleton, you can add a static method
  to the singleton that allows you to replace the instance

* However, this requires that the singleton constructor be public

* If you can't make the constructor public,
  you can derive from it and override the heavy methods
  (e.g., those that access a database)

* If a new singleton's instance is needed between tests,
  you can add a "reset" method to the singleton,
  which sets the instance to null

* One can also replace the singleton with an interface,
  and update all uses of the singleton with the interface

Parameters
..........

* "Extract interface" works most of the time
  to replace concrete parameters, but it's problematic
  when the parameter class inherits from a parent class

* Solution is to create the interface
  and include the parent class's methods,
  and have the parameter class implement it
  by calling its parent's method (see p. 132)

* Another option is to subclass the parameter class
  and replace the heavy method with something else

Chapter 10
----------

* If a method doesn't use instance data,
  it can be turned into a static method for testing

* If a method is too long, it can be extracted to a class

* If a method is private and needs to be tested,
  move to a new class and make the method(s) public,
  then the original class can create an instance of it

* Never depend directly on libraries that are outside of our control

* When there's a method parameter we can't change,
  we can replace it with an interface and pass a wrapper
  (in the test, we pass a fake wrapper)

* A method should be a command or a query, not both
