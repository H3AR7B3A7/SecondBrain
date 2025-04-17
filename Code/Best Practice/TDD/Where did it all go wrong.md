# Where did it all go wrong

 [link](https://www.youtube.com/watch?v=EZ05e7EMOLM)

## The Problem

- Expensive to own test suites
- Breaking heavily mocked tests (/ nothing under test but mocks)
- Slow ATDD suites
- Devs start ignoring red results
- Devs don't want to write them: value return unknown
- Kent Beck <> David Heinemeier Hansson <> Martin Fowler

## TDD Rebooted

- Avoid testing implementation details, test behaviors
- The trigger for a test is implementing a requirement
	- Focusing on methods is hard to maintain, doesn't capture behavior
- Test the public API of the module, not the http API
	- The system under test are the exports from a module - its 'facade', not a class
	- No tests for implementation details - these change
- Use a Given When Then model
- Red, green, refactor - The key is the refactoring step!
- (Behavior) Driven Development

## Red-Green-Refactor

- RED: Write a failing test
- Green: solve the problem quick and dirty
- The key is the refactoring step!
	- No new tests

## Clean code When

To remove code smells

### Refactoring to Patterns 

Shouldn't break tests

## Ports and adapters

- Ports: The door / Facade / Point of entrance
- Adapters: Http, GUI, 

## Gears

Use/write, but delete tests to reach implementation

## ATDD

### Behavior Driven Development

## Mocks

- Don't use them to isolate classes, or confirm implementation details
- Tests that initialize the IOC container are a horror

## Summary

- The reason to test is a new behavior, not a method on a class
- Write dirty code to get green, then refactor
- No new test for refactoring internals and privates (method, class)
- Both Develop and Accept against tests written on a port
- Add integration tests for coverage of ports to adapters
- Add system tests for end-to-end confidence
- Don't mock internals, privates, or adapters

---


