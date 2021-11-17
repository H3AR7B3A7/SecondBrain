# Creational Design Patterns
Creational [[Design Patterns]] provide various object creation mechanisms, which increase flexibility and reuse of existing code.

## Singleton Pattern
The singleton pattern is a software design pattern that restricts the instantiation of a class to one "single" instance. This is useful when we need exactly one object to coordinate actions across the system. The term comes from the mathematical concept of a singleton. Critics consider the singleton to be an anti-pattern in that it is frequently used in scenarios where it is not beneficial, creating unnecessary restrictions in situations where we do not require a sole instance of a class, which constitutes a global state in the application.

### Different approaches: Pros and Cons
#### Eager Initialization
Pro:
-   Lower latency when using the singleton.
-   There is no need to synchronize the getInstance() method, meaning all threads will see the same instance, which requires no (expensive) locking.
-   The final keyword means that the instance cannot be redefined, ensuring that one (and only one) instance ever exists.

Con:
-   The JVM creates an instance even though the client application might not be using it. The application will take longer to boot.
-   Also, this method doesn't provide any options for exception handling.

#### Static Block Initialization

Pro:
-   Lower latency when using the singleton.
-   The final keyword means that the instance cannot be redefined, ensuring that one (and only one) instance ever exists.

Con:
-   The JVM creates an instance even though the client application might not be using it. The application will take longer to boot.
-   If multiple threads are inside the if loop at the same time, both threads will get a different instance of the singleton class.

#### Lazy Initialization
Pro:
-   Shorter boot time of application.

Con:
-   Higher latency when using the singleton.
-   If multiple threads are inside the if loop at the same time, both threads will get a different instance of the singleton class.

#### Thread Safe Lazy Initialization
Pro:
-   It is thread safe.
-   Shorter boot time of application.

Con:
-   It reduces the performance because of cost associated with the synchronized method, although we need it only for the first few threads who might create the separate instances.
-   Unfortunately, synchronized methods run much slower than ordinary asynchronous methods.

#### Double-Checked Locking
Pro:
-   It prevents the cost of calling a synchronized method everytime we need the singleton object.

Con:
-   It is synchronized for concurrent use and can still be slow.
-   Recognizing and reproducing failures can be difficult because of intermittent occurrence.

#### Bill Pugh's
Pro:
-   When the JVM loads the singleton class, it doesn't load the SingletonHelper class into memory. Only when someone calls the getInstance method, this class gets loaded and creates the Singleton class instance.
-   This is the most widely used approach for Singleton class as it doesn't require synchronization.
-   This solution is thread-safe without requiring special language constructs.

Con:
-   Just like all the previous patterns, it also can't handle reflection.

#### ENUM
Pro:
-   It is the only singleton that can handle reflection.
-   Very easy to read.

Con:
-   Can't inherit from a super class. However, enums can implement interfaces.

## Prototype Pattern
We use the prototype pattern when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects.  
We use this pattern to:

-   Avoid subclasses of an object creator in the client application, like the factory method pattern does.
-   Avoid the inherent cost of creating a new object in the standard way (e.g., using the 'new' keyword) when it is prohibitively expensive for a given application.

## (Abstract) Factory Pattern
The factory pattern uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method. This can either be specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes, rather than by calling a constructor.

## Builder Pattern
We use the builder pattern to provide a flexible solution to various object creation problems in object-oriented programming. The intent of the Builder design pattern is to separate the construction of a complex object from its representation.



---
#DesignPatterns