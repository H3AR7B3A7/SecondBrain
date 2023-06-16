# Java

## Access Levels
|  | Class | Package | Subclass (same pkg) | Subclass (diff pkg) | World |
| - | - | - | - | - | - |
| public | &check; | &check; | &check; | &check; | &check; |
| protected | &check; | &check; | &check; | &check; |  |
| package-private | &check; | &check; | &check; |  |  |
| private | &check; |  |  |  |  |

## Keywords
static
final
sealed
abstract
default

## Method Overloading

- different signature (parameters)

_Exceptions:_
- varargs = array
- generics erasure

## Method Overriding

- same signature
- more or equal accessibility
- no new or broader checked exceptions
- same or subtype of return value

## Method Hiding

- same signature
- static
- more or equal accessibility
- no new or broader checked exceptions
- same or subtype of return value

## Interface

### Interface Methods

Interface methods are by default public & abstract.

- abstract (can't be private)
- static (must have a body)
- default (can't be private)
- private / private static (must have a body)

_Cant't have final or protected methods._

### Interface Variables

Interface variables are by default static & final.

- static
- final

_Interface variables NEED to be initialized._

## Abstract Class

### Abstract Class Methods

- abstract methods (can't be static)
- non-abstract methods

_Can have final & protected methods._

### Abstract Class Variables

Abstract classes can have instance variables, but can't be instantiated.

## Interface vs Abstract Class

An **abstract class** allows you to create functionality that subclasses can implement or override. The use of final methods can ensure functionality in classes that extend the abstract class.

An **interface** only allows you to define functionality, not implement it. Default methods can provide default functionality to classes that implement the interface, but these can always be overridden.

And whereas a class can extend only one abstract class, it can take advantage of multiple interfaces.

## Multiple Inheritance

When inherited methods of different classes / interfaces collide there are some rules that determine the behavior.

- superclass > interface default

When both a class is extended and and an interface is implemented the method of the class will define the behavior.

- subtype interface > supertype interface

When an interface extends another, the method of the interface extending (the subtype) will define the behavior.
  
- 2 interfaces: the method needs to be implemented

## Errors

- Throwable
	- Error (unchecked)
	- Exception (checked)
		- Runtime Exception (unchecked)

---
#ComputerLanguage #Java