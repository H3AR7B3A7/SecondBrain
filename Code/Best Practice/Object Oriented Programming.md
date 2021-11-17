# Object Oriented Programming (OOP)  
  
Four main principles of OOP:  
-  **Abstraction**: Hiding internals ensures simplicity.  
-  **Encapsulation**: Keeping internals private prevents modification.  
-  **Inheritance**: Inheriting attributes or functions avoids code duplication.  
-  **Polymorphism**: A single interface to entities of different types or the use of a single symbol to represent  
     multiple different types allows for different meaning or function depending on the instance.  

OOP helps programmers with [[Best Practice(s)]] like the DRY principle and modeling code to real world structures.

## Creating Objects  
  
### Static Factory Methods  
  
Advantages:  
- Methods have a name  
- Not required to make new object when invoked  
- Can return any subtype of the return type  
- The returned subtype can vary based on parameters  
- The implementation of the returned object doesn't need to exist yet when writing the code  
  
Drawbacks:  
- Classes without public or protected constructor can't be subclassed  
- They can be hard to find for programmers  
  
### Builder Pattern  
  
When facing a lot of parameters, a builder can be helpful for object creation.  
- Simulates named optional parameters  
- Well suited to class hierarchies  
- Good design choice over static factory when there are a lot of parameters  
  
Alternative drawbacks:  
- Telescoping constructors  
  - Hard to write client code  
  - Hard to read  
- Javabeans  
  - Allows inconsistency partway through construction  
  - Mandates mutability, requiring effort to ensure threat safety  
  
### Singleton  
  
*Making a class a singleton can make it difficult to test its clients.  
It is impossible to substitute a mock implementation for a singleton unless it implements an interface that serves as its type.*  
  
Options:  
- Private constructor  
- Enum (constructor is always private)  
 - Can't extend  
  - Can implement  
  
### Noninstantiability  
  
*While classes containing only static fields and static methods are frowned upon they do have their use.  
When we need them we should make the constructor private, so they can't be instantiated.*  
  
### Dependency Injection  
  
*Dependency Injection provides flexibility and testability.*  
  
Static utility classes and singletons are inappropriate for classes whose behavior is parametrized by an underlying resource.  
  
Dependency Injection can clutter up large projects, which can be eliminated using a DI framework, like Dagger, Juice or Spring.  
  
### Avoid Object Creation  
  
The string pool prevents unnecessary object creation for string objects. We should not use the 'new' keyword and instead just assign quoted text.  
  
We should try to avoid creating expensive objects where possible and prefer reusing them.  
  
We should also look out for object creation due to unintentional autoboxing.  
  
### Obsolete Object References  
  
*Nulling out object references should be the exception rather than the norm, but whenever a class manages its own memory,  
the programmer should be alert for memory leaks.*  
  
Another common source of memory leaks are caches. We can use weak hashmaps when if the desired lifetime of cache entries  
is determined by external references to the 'key'. Or by occasionally cleaning the cache using a background thread.  
  
A third common source of memory leaks are listeners and other callbacks.  
We should either deregister them explicitly or store only weak references to them by storing them as keys in a weak hashmap.  
  
### Avoid Finalizers and Cleaners  
  
The finalize method is deprecated for a reason. To protect non-final classes from finalizer attacks,  
write a final finalize method that does nothing.  
  
Resources that require termination should just implement AutoCloseable.  
  
### Try-With-Resources  
  
We should prefer try-with-resources over try-finally, apart from looking better when using multiple resources,  
it is the new and improved way to close resources.  
  
  
## Object Methods  
  
### Equals: General Contract  
  
Equals methods must adhere to the general contract:  
```  
- Reflexive  
- Symmetric  
- Transitive  
- Consistent  
- Never equal to null  
```  
  
They should also follow Liskov's substitution principle saying that:  
- Any important property of a type should hold for all its subtypes.  
  
*If we were to use inheritance instead of composition we would violate one or more of these rules.*  
  
### Hashcode & Equals  
  
HashCode methods must adhere to the general contract:  
```  
- Consistent  
- Two objects that are equal must have the same hashcode  
- Hash table performance is better if objects that are not equal have different hashCodes  
```  
  
*When caching hashCodes, make sure the objects are immutable!!!*  
  
### Override toString  
  
Providing a good toString implementation makes our class much more pleasant to use and makes systems using the class easier to debug.  
  
*When practical, the toString method should return all the interesting information contained in the object.*  
  
The format of the return value should match that of the static factory or constructor if specified.  
Provide programmatic access to the information in the value returned by the toString method.  
  
### Override Clone Judiciously  
  
Though the specification doesn't say it, in practice, a class implementing cloneable is expected to provide  
a properly functioning public clone method.   
  
Not absolute requirements:  
```  
- x.clone() != x returns true  
- x.clone().getClass == x.getClass() returns true  
- x.clone().equals(x) returns true  
```  
  
In practice, first call super.clone() and then handle any reference values to prevent shared mutable state.  
  
*Immutable classes should never provide a clone method. It only encourages wasteful copying.*  
  
The Cloneable architecture is incompatible with normal use of final fields referring to mutable objects.  
  
**A better approach to object copying is to provide a copy constructor or copy factory.**  
  
### Consider Implementing Comparable  
  
It indicates objects of this class have a natural order. Comparable should also adhere to the general contract:  
```  
- If this object precedes that; return negative value  
- If this object equals that; return zero  
- If this object proceeds that; return positive value
```  
  
Use of the relational operators < and > in compareTo methods is verbose, error-prone and no longer recommended.  
We should use the compare methods of the wrapper classes instead.  
  
We can also make use of a comparator and its construction methods. Chain them and then use the comparator in our compareTo method.  
  
  
## Classes and Interfaces  
  
### Minimize Accessibility  
  
### Accessor Methods  
  
### Minimize Mutability  
  
### Composition Over Inheritance  
  
### Design for - or Prohibit Inheritance  
  
  
  
---  
*Work in progress...*