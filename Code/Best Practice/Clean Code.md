# Clean Code  
Clean code is all about [[Best Practice(s)]] for writing readable and easy to maintain code.

## Meaningful Names  
*Good*:  
- Intentionally revealing  
- Meaningful and distinct  
- Pronounceable  
- Searchable  
- Consistent  
- Understandable: Computer Science / Domain  
- In a meaningful context  
  
*Bad*:  
- Disinformation or false clues  
- Encoding  
- Need for mental mapping  
- Being cute  
- Puns  
- Gratuitous context  
  
**Classes**: nouns or noun phrase    
**Methods**: verbs or verb phrase  
  
  
## Functions  
They should:  
- Be small  
- Have minimal nesting  
- Do one thing / List things at just one level of abstraction  
  - Change state of object  
  - Return information on an object  
- Have structure if they are larger than desired  
   - Sections: declarations / initializations / sieve  
  
**Switch Statements** should:  
- Appear only once (in an abstract factory)  
- Create polymorphic objects  
- Be hidden behind an inheritance relationship  
  
**Arguments**:  
- Minimal number of arguments (Never more than three)  
- They need a good reason to exist  
   - A question about the argument  
   - Operations on an argument (Move function to argument object?)  
 - An event as argument  
- Avoid output arguments (Outputs should be in return statement)  
 - House the function in the object with the state change  
- Avoid flags (booleans)  
- Avoid side effects  
  
**Exceptions over Error Codes**  
  
*Error codes*:  
- Lead to deeply nested structures  
- Caller has to deal with it immediately  
- Need for rebuilding when adding new error code  
  
*Exceptions*:  
- Separate happy path from error processing  
- No need to rebuild: all derivative of exception.class  
  
**Try/Catch** blocks  
- Extract the bodies into functions  
  
  
## DRY  
*Don't Repeat Yourself.*  
  
A lot of evolution in languages and frameworks aims avoid repeating code:  
- Codd's forms  
- OOP  
- Aspect oriented programming  
- Component oriented programming  
- ...  
  
**Structural Programming Rules**:  
What Dijkstra said about code block or function:  
- One entry  
- One exit  
- No:  
  - break  
  - continue  
  - goto !!!  
  
**Now**:  
These rules are less important now we are able to use smaller functions.  
Breaks and continues can help in our expressions.  
  
**Method**:  
We start by writing a first draft and then improve our code to apply these good practices.  
  
  
## Comments  
*At best, comments are a necessary evil.*  
  
**GOOD Comments**:  
- Legal comments (copyright, ...)  
- Informative (Example format, return type ... What?)  
- Explanation of intent (Why?)  
- Clarification (Readability)  
- Warnings of consequence  
- TODO  
- Amplify (Draw attention)  
- Javadocs for public API  
  
**BAD Comments**:  
- Mumbling  
- Redundant  
- Mandated  
- Journal  
- Noise  
- Scary noise  
- Position markers  
- Closing braces  
- Attributions and bylines  
- Commented out code  
- HTML comments  
- Non-logical info  
- Too much info  
- Inobvious connection  
- Function headers  
- ...  
  
  
## Formatting  
Formatting tools:    
Consistently apply rules to help communicate the code  
  
*While functionality changes, readability usually continues to affect the maintainability.*  
  
- **Vertical**  
 - File / Class size  
      - Smaller = More easy to read  
  - Blank lines are viual cues  
  - Vertical density should indicate relations  
      
Locations  
- Local variables at the top of functions  
- Control values for loops in loop statements  
- Instance variables at top of class  
- Dependant functions should be vertically close  
  - Caller should be above the callee  
- Functions with conceptual affinity should be vertically close  
  
- **Horizontal**  
 - Keep lines short  
  - Closely related values should be horizontally close (like parameters in a function)  
 - A space can indicate 'less relation' compared to no space (like with an assignment)  
 - We can make precedence of operations more visual with spaces (doesn't work with formatting tool)  
  
*When you feel like a long list of declarations needs spacing in Java, you should probably split the class.*  
  
**Indentation**:    
Visualises the scope hierarchy.  
- Avoid breaking the rule on indentation even in compact structures  
- Mind dummy scopes (the semicolon after a one liner is easy to miss)  
  
***Teams should agree on a single style of formatting. Consistent gestures help readability a lot.***  
  
  
## Objects & Datastructutres  
Hiding implementation ≠ Layer of functions between the variables.  
  
**Objects**  
  
- Abstractions  
- Exposing functions  
  - Manipulating the essence of the object  
  - Not knowing the implementation  
  
**Data structures**  
- Exposing data  
- No meaningful functions  
  
**Procedural vs Visitor- or Dual-Dispatch Pattern**  
Sometimes you really do want simple data structures with procedures operating on them.  
(It is just a myth that "everything is an object".)  
  
  
### The Law of Demeter  
*(Modules shouldn't know about innards of the objects it manipulates.)*  
  
A method **f** of a class **C** should only call methods of these:  
- C  
- An object created by f  
- An object held in an instance variable of C  
  
The method should NOT invoke methods on objects that are returned by any of the allowed functions.  
("Talk to friends, not to strangers.")  
  
**Chained calls are generally sloppy programming and often rightfully called train wrecks.**  
  
These are in violation of Demeter only if the methods call for objects, but not when just accessing data structures. The difference often gets obscured by accessor functions.  
  
If they are objects we should ask ourselves what we need them for. We should make the initial object 'DO' something for us.  
This way we avoid having to know about the inners of the objects.  
  
  
### Data Transfer Objects  
Uses:  
- Communication with databases  
- Parsing from sockets  
- ...  
  
**Beans** are almost equivalent to this, but with accessor functions are 'quasi-encapsulated' without any real benefit.  
  
**Active records** are a special form of DTO, with navigational methods like *save* and *find*.  
  
None of these data structures should contain any business logic, which belongs in separate objects.  
  
  
## Error Handling  
*Error handling is important, but if it obscures logic, it's wrong.*  
  
It is cleaner to throw an exception in the callee than it is to use return codes in the caller.  
  
Starting with a Try-Catch-Finally statement will help us define a scope to which we can safely add logic using TDD.  
  
Checked exceptions violate the Open-Closed principle. A change in low level code can force many higher classes add exceptions to method signatures.  
This is why other languages don't have any, and we should use unchecked exceptions. They are only useful in critical libraries, not when writing applications.  
  
An exception should provide adequate context in a good error message to locate the error.  
  
  
### Defining Exceptions  
Classifications:  
- Source  
- Type  
  
How to catch them:  
- We should think about a 'common exception type' when we need to catch multiple exceptions.  
- Often a wrapper can help us catch and translate exceptions (of a 3d party API).  
  - Minimize dependencies  
  - Easy to swap out libraries later  
  - Easy to mock out 3d party calls in testing  
  - Not tied to 3d party API design  
  
One exception class is sufficient for an area of code, unless we want to catch one exception and allow another to pass through.  
  
  
### Defining Normal Flow  
Even better than handling an exception is making it part of the normal flow, by using something like the *Special Case Pattern*.  
The client code doesn't need to handle the exception if it is encapsulated in a special case object.  
  
  
### Don't Return Null  
Passing null to a method is even worse than returning null.  
  
Fixes:  
- Exception + handling  
- Assertions  
  
We'd still have a runtime error, and it is better to forbid passing null in the first place!  
  
  
## Boundaries  
We should keep clean boundaries between our software and foreign code.  
  
Conflicting interests:  
- Provider: broad applicability  
- User: focus on needs  
  
By wrapping we can make the code easier to read and harder to misuse. We can enforce design and business rules upon this wrapper.  
  
**Learning tests** can help us understand third party code.  
We shouldn't thoroughly test the third party API, but small tests similar to how we use that API can help differentiate problems   
in our own code from misunderstandings about the foreign code.  
  
We can handle yet unwritten code the same way. By temporarily creating the API we wish we had we can write concise code for it.  
We can then write a wrapper for the actual code when eventually the code is developed.  
  
  
## Unit Tests  
*If we let our tests rot, the production code will rot too.*  
  
Three laws of TDD:  
- You may not write production code until you have written a failing test.  
- You may not write more of a unit test than is sufficient to fail, and not compiling is failing.  
- You may not write more production code than is sufficient to pass the current failing test.  
  
*This way of working will generate A LOT of tests, which we need to manage and keep clean.*  
  
Our tests are just as important as production code. A mess in the testing suite will lead to loss of maintainability and eventually abandonment.  
Losing our tests is losing confidence to make changes to our code, not knowing if we introduced bugs when doing so.  
  
**Readability** is even more key in unit tests than in production code.  
- Avoid code repetition  
- Refactor out irrelevant details (Creating a 'Testing API')  
- Make 'BUILD-OPERATE-CHECK' structure visible  
- Prefer readability to efficiency (memory/CPU)  
- Keep tests small and clear  
- One assert per test (as a guideline)  
 - Test a single concept  
  
FIRST (Object Mentor Training Materials idea of writing clean tests)  
- Fast: They should run quickly  
- Independent: They should not depend on each other  
- Repeatable: They should be repeatable in any environment  
- Self-Validating: They should either pass or fail (no investigating)  
- Timely: They should be written right before production code  
  
  
## Classes
Order:  
- public static finals (constants)  
- private static variables  
- private instance variables  
- public functions  
  - private functions called by them right after  
  
We look for ways to maintain privacy (encapsulation), but will allow protected / package private variables or utility functions to be accessible by a test.  
  
Rules a clean class adheres to:  
- Small size (No 'god' classes)  
 - Single responsibility  
    - A description shouldn't require 'and/if/or' (concise name/description)  
 - If something prevents the class to be reusable, it probably doesn't belong  
  - Small number of instance variables  
    - Each method should operate on one or more of them (cohesion)  
 - Instance variables serving to keep a subset of methods small almost always means they belong in a new class  
    - Refactoring methods while keeping parameter lists small will generate more instance variables and thus possible new classes  
- Open-Closed Principle  
  - We use interfaces and abstract classes to isolate concrete details from changes in the code  
  
  
## Systems
Abstractions and modularity are key for components to work effectively.  
  
  
### Separating construction from use:
**Separation of main:**  
- Main:  
  - Consistent strategy for resolving major dependencies  
- Application  
  - Use interfaces that call on these dependencies  
  
**Dependency Injection:**  
  
*(The application of Inversion of Control to dependency management)*  
  
An authoritative mechanism, either a main routine or a special-purpose container, is responsible for resolving dependencies.  
  
The Spring framework provides the best known DI container for Java.  
  
  
### Scaling up:
*The architecture of software systems can grow incrementally **IF** proper separation of concerns is maintained.*  
  
In practice, sometimes fine-grained intersection of domains can tend to cut across the natural object boundaries.  
Aspect oriented programming is a general-purpose approach to restoring modularity for these cross-cutting concerns.  
  
Aspect-like mechanisms in Java:  
  
- **Java Proxies**:  
For simple situations like wrapping method calls in individual objects or classes.  
Dynamic proxies in JDK only work with interfaces. To proxy classes we need to use a byte-code manipulation library like CGLIB, ASM or Javassist.  
The code volume and complexity even for simple cases, makes it hard to keep code clean.  
  
- **Pure Java AOP Frameworks**:  
Spring AOP or JBoss AOP can handle most of the proxy boilerplate code. Even the outdated verbose wiring of beans using XML was preferable over the complexity of proxy and aspect logic.  
The application is almost completely decoupled from Spring and the tight-coupling problems are eliminated, making it easy to test and maintain.  
These frameworks are sufficient for +-90% of the cases.  
  
- **AspectJ Aspects**:  
An extension of Java that provides first-class support for aspects as modularity constructs.  
Tools and language constructs can be a drawback, but are largely mitigated by annotation-based aspects.  
  
The ability to write our application's domain logic using simple POJOs decoupled from the architecture helps us separate concerns.  
This separation of concerns allows for more agile development in absence of 'Big Design Up Front'.  
Thinking about design is good, but designing *everything* up front limits the ability to adapt to change.  
  
The agility provided by a POJO system with modularized concerns allows us to make optimal, just-in-time decisions,  
based on recent knowledge. The complexity of these decisions is also reduced.  
  
**Standards** make it easier to reuse ideas and components, recruit people with relevant experience, encapsulate good ideas,  
and write components together. However, the process of creating standards can sometimes take too long for industry to wait,  
and some standards lose touch with the real needs of the adopters they are intended to serve.  
  
  
### Domain Specific Languages
DSL can help code to better reflect a domain experts input. Used effectively, they can raise the abstraction level above code idioms and design patterns.  
  
They allow all levels of abstraction and all domains in the application to be expressed as POJOs, from high-level policy to low-level details.  
  
  
## Emergence
Kent Beck's four rules of **Simple Design**:  
- Runs all the tests  
- Contains no duplication  
- Expresses the intent of the programmer  
- Minimizes the number of classes and methods  
  
  
## Concurrency
Concurrency helps us decouple what gets done from when it gets done. It can improve the throughput and the structure of a program.  
The improvement in throughput is greatest when there is a lot of waiting involved (for example on web-sockets).  
  
Common misconceptions:  
- Concurrency is always faster  
- Design does not change when writing concurrent programs  
- Understanding concurrency issues is not important when working with a container such as Web or EJB container  
  
Facts:  
- Concurrency incurs some overhead, both in performance and writing additional code  
- Correct concurrency is complex, even for simple problems  
- Concurrency bugs aren't usually repeatable and are often ignored as one-offs instead of a defect  
- Concurrency often requires a fundamental change in design strategy  
  
  
### Concurrency Defense Principles
Principles for defending code from concurrency problems:  
- Single responsibility principle  
- Limiting the scope of data  
  - Encapsulation of shared data  
  - Limiting access to shared data  
- Use copies of data (preventing shared data)  
- Keep threads as independent as possible  
  
*Attempt to partition data into independent subsets that can be operated on by independent threads, possibly in different processors.*  
  
  
### Know Your Libraries
- java.util.concurrent  
- java.util.concurrent.atomic  
- java.util.concurrent.locks  
  
Some interesting subjects to know about:  
- Thread safe collections  
- Executor framework  
- Thread unsafe library classes  
- Use non-blocking solutions when possible  
- Reentrantlock  
- Semaphore  
- CountDownLatch  
  
  
### Know Your Execution Models
Problems:  
- Bound resources  
- Mutual exclusion  
- Starvation  
- Deadlock  
- Livelock  
  
Execution models:  
- Producer-Consumer  
  - Bound resource: queue  
    - Producers add tasks to queue and signal it is no longer empty  
    - Consumers read from the queue and signal it is no longer empty  
- Readers-Writers  
  - Preventing simultaneous reading and updating  
    - Finding balance to provide reasonable throughput and prevent starvation  
- Dining Philosophers  
  - Systems in which threads compete for resources need to be carefully designed to prevent issues  
    - Throughput  
    - Deadlock  
    - Livelock  
  
  
### Dependencies Between Synchronized Methods
*Avoid using more than one method on a shared object.*  
  
When we use more than one method on a shared object:  
- Client-Based Locking  
- Server-Based Locking  
- Adapted Server  
  
  
### Keep Synchronized Sections Small
*Keep critical sections few and small.*  
  
The locks in synchronized blocks create overhead and delays which need to be avoided.  
We want to keep these blocks small and concise when we need them.  
  
  
### Shut-Down Code
Writing graceful shut-down code is hard.  
  
Threads waiting for signals to continue that never come can lead to deadlock.  
Threads working in pairs might be unable to receive shut-down signals waiting for a signal of its partner.  
  
*Think about shut-down early and get it working early. It's going to take longer than you expect.  
Review existing algorithms, because this is probably harder than you think.*  
  
  
## Testing Threaded Code
Testing only minimizes risk for incorrect behaviour.  
  
*Write tests that have the potential to expose problems and run them frequently with different programmatic/system configurations and load.  
If tests ever fail, track down the failure. Don't ignore failure because tests pass on a second subsequent run.*  
  
- Treat spurious failures as candidate threading issues  
- Get non-threaded code to work first  
- Make threaded code pluggable  
  - One / several / varying number of threads  
  - Interacting with real objects / test doubles  
    - Force different orderings by using: object.wait(), .sleep(), .yield(), priority()  
 - Hand coded  
      - Automated: CGLIB, ASM, ... (Thread jiggling strategies)  
 - Varying number of iteration  
- Make threaded code tunable  
  - Time performance early under different configurations  
  - Consider allowing self-tuning in runtime  
- Run with more threads than processors  
- Run on different platforms  
- Instrument your code to try and force failures  
  
  
## Smells and Heuristics
Comments:  
- Inappropriate information  
- Obsolete comment  
- Redundant comment  
- Commented-out code  
  
Environment:  
- Build requiring multiple steps  
- Tests requiring multiple steps  
  
Functions:  
- Too many arguments  
- Output arguments  
- Flag arguments  
- Dead functions  
  
General:  
- Multiple languages in one source file  
- Obvious behaviour is unimplemented  
- Incorrect behaviour in the boundaries  
- Overridden safeties  
- Duplication  
- Code at wrong level of abstraction  
- Base classes depending on their derivatives  
- Too much information  
- Dead code  
- Vertical separation  
- Inconsistency  
- Clutter  
- Artificial coupling  
- Feature envy  
- Selector arguments  
- Obscured intent  
- Misplaced responsibility  
- Inappropriate static  
- Use explanatory variables  
- Function names should say what they do  
- Understand the algorithm  
- Make logical dependencies physical  
- Prefer polymorphism to if/else or switch/case  
- Follow standard conventions  
- Replace magic numbers with named constants  
- Be precise  
- Structure over convention  
- Encapsulate conditionals  
- Avoid negative conditionals  
- Functions should do one thing  
- Hidden temporal couplings  
- Don't be arbitrary  
- Encapsulate boundary conditions  
- Functions should descend only one level of abstraction  
- Keep configurable data at high levels  
- Avoid transitive navigation  
  
Java:  
- Avoid long import lists by using wildcards  
- Don't inherit constants  
- Prefer enums to constants  
  
Names:  
- Choose descriptive names  
- Choose names at the appropriate level of abstraction  
- Use standard nomenclature where possible  
- Unambiguous names  
- Use long names for long scopes  
- Avoid encodings  
- Names should describe side effects  
  
Tests:  
- Insufficient tests  
- Use a coverage tool  
- Don't skip trivial tests  
- An ignored test is a question about ambiguity  
- Test boundary conditions  
- Exhaustively test near bugs  
- Patterns of failure are revealing  
- Test coverage patterns can be revealing  
- Tests should be fast  
  
  
  
---  
#BestPractice 