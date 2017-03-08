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
