# Other Good Design Practices

## Static Factory Method
A static factory method is a public static method on the object that returns a new instance of the object. These type of methods share the same benefits as the traditional factory method design pattern. This is especially useful for value objects that don't have a separate interface and implementation class.

Pro:
-   They have names.
-   They are not required to create a new object each time they’re invoked.
-   They can return an object of any subtype of their return type.
-   The class of the returned object can vary from call to call as a function of the input parameters.
-   The returned object need not exist when writing the class containing the method.

Con:
-   Classes without public or protected constructors can't be subclassed.
-   Harder to find for programmers, so it will require some naming conventions.

## Dependency Injection
Dependency injection is a technique in which an object receives other objects that it depends on. We call these other objects dependencies. In the typical "using" relationship we call the receiving object a client, and the passed (that is, "injected") object a service.

## Avoiding Object Creation
We should consider reusing an expensive object to avoid creating it multiple times. This can drastically improve performance. Likewise, we should avoid unnecessary boxing of primitives in repetitive operations to avoid repeated creation of their wrapper variants.

## Cleaning Objects
The Garbage Collector removes an Object that has been created during the program execution automatically after use. When an object not referenced by any thread and when JVM determines that this object can't be accessed, then it can be eligible for garbage collection.

Finalize() is an object method, which is automatically called by the garbage collector before it attempts to remove the object from the heap. In Java 9, finalize() has been deprecated. A new class java.lang.ref.CleaningObjects was added to garbage collection management. An object of CleaningObjects class gets notified automatically when an object becomes eligible for garbage collection. An object that is being garbage collected needs to be registered with the cleaner object by using the register() method.

Usually the use of a cleaner is unnecessary. We only use it in specific situations, for example when we want to make sure sensitive information doesn't stay in memory.

## Composition
There is no way to extend an instantiable class and add a value component while preserving the equals contract. For this reason we should favor composition over inheritance. Instead of inheriting from an object we can add it as a private field. We can provide a public 'view' method to return the field to compare the object with instances of its member type.

## Caching
We can cache a value when the cost of computing it is significant, to prevent repeating the computation.

## Reflection
Reflection is not so much a code structure, but rather a Java API. Because it is mentioned a couple of times in this repository there is an example of it too. It is used to examine or modify the behavior of methods, classes, interfaces at runtime. The required classes for reflection are provided under java.lang.reflect package. Reflection gives us information about the class to which an object belongs and also the methods of that class which can be executed by using the object. We can use it to invoke methods at runtime irrespective of the access specifier used with them.

## MVC - Pattern
The MVC pattern is commonly used for developing user interfaces that divides the related program logic into three interconnected elements. This is done to separate internal representations of information from the way information is presented to and accepted from the user. It usually consists of several other design patterns. At a minimum the MVC pattern uses Observer pattern which is a Behavioral pattern. There are some more design patterns used by MVC. Sometimes the patterns it uses may depend on the particular implementation too.