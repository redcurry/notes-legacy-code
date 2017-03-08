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
