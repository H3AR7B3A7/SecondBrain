# Behavioral Design Patterns
Behavioral [[Design Patterns]] are concerned with algorithms and the assignment of responsibilities between objects.

## Chain Of Responsibility Pattern
The chain-of-responsibility pattern consists of a source of command objects, and a series of processing objects. Each processing object contains logic that defines the types of command objects that it can handle. The rest it will pass to the next processing object in the chain. A mechanism also exists for adding new processing objects to the end of this chain.

In a variation of the standard chain-of-responsibility model, some handlers may act as dispatchers, capable of sending commands out in a variety of directions, forming a tree of responsibility. In some cases, this can occur recursively, with processing objects calling higher-up processing objects with commands that attempt to solve some smaller part of the problem. When this is the case, recursion continues until the handler finishes processing the command, or the entire tree has been explored. For example, an XML interpreter might work in this manner.

This pattern promotes the idea of loose coupling.

The chain-of-responsibility pattern is structurally nearly identical to the decorator pattern. The difference is that for the decorator, all classes handle the request, while for the chain of responsibility, exactly one of the classes in the chain handles the request. This is a strict definition of the Responsibility concept in the GoF book. However, many implementations (such as loggers, or UI event handling, or servlet filters, etc.) allow several elements in the chain to take responsibility.

## Command Pattern
In the command pattern, we use an object to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

Four terms always associated with the command pattern are command, receiver, invoker and client. A command object knows about the receiver and invokes its method. We store values for parameters of the receiver method in the command. We store the receiver object to execute these methods in the command object by aggregation. The receiver then does the work when we call the execute-method in command. An invoker object knows how to execute a command, and optionally does bookkeeping about the command execution. The invoker does not know anything about a concrete command, it knows only about the command interface. A client object holds the invoker object(s), command objects and receiver objects. The client decides which receiver objects it assigns to the command objects, and which commands it assigns to the invoker. The client decides which commands to execute at which points. To execute a command, it passes the command object to the invoker object.

Using command objects makes it easier to construct general components that need to delegate, sequence or execute method calls at a time of their choosing without the need to know the class of the method or the method parameters. Using an invoker object allows bookkeeping about command executions to be conveniently performed, as well as implementing different modes for commands, which are managed by the invoker object, without the need for the client to be aware of the existence of bookkeeping or modes.

The central ideas of this design pattern closely mirror the semantics of first-class functions and higher-order functions in functional programming languages. Specifically, the invoker object is a higher-order function of which the command object is a first-class argument.

## Interpreter Pattern
We use the interpreter pattern to specify how to evaluate sentences in a language. The basic idea is to have a class for each symbol (terminal or non-terminal) in a specialized computer language. The syntax tree of a sentence in the language is an instance of the composite pattern and is used to evaluate (interpret) the sentence for a client.

## Iterator Pattern
In the iterator pattern, an iterator is used to traverse a container and access the container's elements. The iterator pattern decouples algorithms from containers. In some cases, algorithms are necessarily container-specific and thus cannot be decoupled.

For example, the hypothetical algorithm SearchForElement can be implemented generally using a specified type of iterator rather than implementing it as a container-specific algorithm. This allows SearchForElement to be used on any container that supports the required type of iterator.

## Mediator Pattern
The mediator pattern defines an object that encapsulates how a set of objects interact. With the mediator pattern, we encapsulate communication between objects within a mediator object. Objects no longer communicate directly with each other, but instead communicate through the mediator. This reduces the dependencies between communicating objects, thereby reducing coupling.

## Memento Pattern
The memento pattern provides the ability to restore an object to its previous state (undo via a rollback). We implement it with three objects: the originator, a caretaker and a memento. The originator is some object that has an internal state. The caretaker is going to do something to the originator, but wants to be able to undo the change. The caretaker first asks the originator for a memento object. Then it does whatever operation (or sequence of operations) it was going to do. To roll back to the state before the operations, it returns the memento object to the originator. The memento object itself is an opaque object (one which the caretaker cannot, or should not, change). When using this pattern, care should be taken if the originator may change other objects or resources. The memento pattern operates on a single object.

## Null Object Pattern
A null object is an object with no referenced value or with defined neutral ("null") behavior. The null object design pattern describes the uses of such objects and their behavior (or lack thereof). It can be regarded as a special case of the State pattern and the Strategy pattern.

## Observer Pattern
In the observer pattern, an object named the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods. It is mainly used for implementing distributed event handling systems, in "event driven" software.

## State Pattern
The state pattern allows an object to alter its behavior when its internal state changes. This pattern is close to the concept of finite-state machines. It can be interpreted as a strategy pattern, which is able to switch a strategy through invocations of methods defined in the pattern's interface.

## Strategy Pattern
The strategy pattern enables selecting an algorithm at runtime. Instead of implementing a single algorithm directly, code receives run-time instructions as to which in a family of algorithms to use. For instance, a class performing validation on incoming data may use the strategy pattern to select a validation algorithm depending on the type of data, the source of the data, user choice, or other discriminating factors. We don't know these factors until run-time and may require radically different validation to be performed. Other validating objects may use the validation algorithms (strategies) encapsulated separately from the validating object, in different areas of the system (or even different systems) without code duplication.

## Template Pattern
The template method is a method in a superclass, usually an abstract superclass, and defines the skeleton of an operation in terms of a number of high-level steps. These steps are themselves implemented by additional helper methods in the same class as the template method. The helper methods may be either abstract methods, requiring subclasses to provide concrete implementations, or hook methods, which have empty bodies in the superclass. Subclasses can (but are not required to) customize the operation by overriding the hook methods. The intent of the template method is to define the overall structure of the operation, while allowing subclasses to refine, or redefine, certain steps.

## Visitor Pattern
The visitor design pattern is a way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existing object structures without modifying the structures. It is one way to follow the open/closed principle. In essence, the visitor allows adding new virtual functions to a family of classes, without modifying the classes. Instead, a visitor class is created that implements all the appropriate specializations of the virtual function. The visitor takes the instance reference as input, and implements the goal through double dispatch.