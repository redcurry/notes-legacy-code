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

Chapter 11
----------

Effects
.......

* To understand how changing a method will affect
  the rest of the program, we need to create "effect sketches"
  (see simple example on p. 159)

* Make a list of all the things that can be changed
  after an object is created that would affect results
  returned by any of its methods

* For example, someone could add/remove elements of a list property
  or someone could change any of the items in that list

* Figure out the places were properties are modified
  after the object is created

Reasoning Forward
.................

* Using effect sketches, we can figure out what will change
  downstream if we make a change

* Remember to not count methods that don't change behavior
  when the item being looked at could change

* Look not only at changes within a class,
  but also changes to other classes

* Also look at superclasses and subclasses that may be affected

(Remaining sections)
....................

* A method may modify one of its parameters or a static variable,
  so consider these as effects as well

* In good code, there are clear rules (explicit or implicit)
  that constrain you whether something can be or should be changed;
  these rules make it easier to think about code

Chapter 20
----------

* Every class should have a single responsibility,
  and there should be only one reason to change it

* Find the responsibilities of a big class
  by grouping related methods together

* Ask yourself, "Why is this method here?" and
  "What is it doing for the class?"

* A class that has many private or protected methods
  may indicate that it has more than one responsibility

* Extract methods for decisions made (e.g., talking to a database)
  or hard-coded information; this can make grouping easier

* Find relationships between methods and instance variables;
  usually there is "lumping," which can be a sign of a group

* To find "lumps," draw circles for each variable and method,
  then draw a line if a method uses the variable,
  then notice any clustering, which may indicate
  separate responsibilities; but it may not,
  so try a different clustering

* Describe the key responsibility of a class;
  other responsibilities should be factored out into other classes

* Two ways to violate the single responsibility principle:
  (1) interface level or (2) implementation level

* For interface level, a class may appear to have many responsibilities
  when its interface has many methods

* For implementation level, a class really does all the things
  declared by its interface

* We care most about implementation level violation;
  interface level is not too bad because the class is a facade

* If we need to simplify at the interface level,
  the client could use some delegate classes directly

* One can use Interface Segregation to create interfaces
  for groupings in a class, so that clients only use
  the interface they need

* Then, to split up the large class, one can create an implementation
  of one of its interfaces, and pass the large class to the implementation;
  the large class does not need to have that interface anymore
  and the methods can be removed from it;
  essentially, you move certain behaviors out of the large class
  into a separate class, which uses the original class to implement
  the behaviors

* When modifying a class, that change may represent
  a new responsibility and may be best to put it in a separate class

* Read books on design patterns, read other people's code,
  and look at open-source projects

* When refactoring, start at the implementation level,
  then slowly move to interface level
