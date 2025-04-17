# Structural Design Patterns
Structural [[Design Patterns]] explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

## Adapter Pattern
We use the adapter pattern (also known as wrapper, an alternative naming shared with the decorator pattern) to allow the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code. An example is an adapter that converts the interface of a Document Object Model of an XML document into a tree structure that can be displayed.

## Bridge Pattern
We use the bridge pattern to "decouple an abstraction from its implementation so that the two can vary independently". The bridge uses encapsulation, aggregation, and can use inheritance to separate responsibilities into different classes.

## Composite Pattern
We use the composite pattern to describe a group of objects that are treated the same way as a single instance of the same type of object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies. Implementing the composite pattern lets clients treat individual objects and compositions uniformly.

## Decorator Pattern
We use the decorator pattern to allow behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern. Decorator use can be more efficient than subclassing, because an object's behavior can be augmented without instantiating an entirely new object.

## Facade Pattern
The facade pattern serves as a front-facing interface masking more complex underlying or structural code.  
A facade can:

-   Improve the readability and usability of a software library by masking interaction with more complex components behind a single (and often simplified) API
-   Provide a context-specific interface to more generic functionality (complete with context-specific input validation)
-   Serve as a launching point for a broader refactor of monolithic or tightly-coupled systems in favor of more loosely-coupled code

Developers often use the facade pattern when a system is very complex or difficult to understand because the system has many interdependent classes or because its source code is unavailable. This pattern hides the complexities of the larger system and provides a simpler interface to the client. It typically involves a single wrapper class containing a set of members required by the client. These members access the system on behalf of the facade client and hide the implementation details.

## Flyweight Pattern
A flyweight is an object that minimizes memory usage by sharing as much data as possible with other similar objects. It is a way to use objects in large numbers when a simple repeated representation would use an unacceptable amount of memory. Often some parts of the object state can be shared. The flyweight object holds the objects in an external data structure and passes them when they are needed.

A classic example usage of the flyweight pattern is the data structures for graphical representation of characters in a word processor. For each character in a document, it might be desirable to have a glyph object containing its font outline, font metrics, and other formatting data, but this would amount to hundreds or thousands of bytes for each character. Instead, for every character there might be a reference to a flyweight glyph object shared by every instance of the same character in the document. Only the position of each character in the document would need to be stored internally.

## Proxy Pattern
A proxy is a class functioning as an interface to something else. The proxy could interface to anything: a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate. In short, a proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy, extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before invoking operations on the real object. For the client, usage of a proxy object is similar to using the real object, because both implement the same interface.


---

*Work in progress...*
