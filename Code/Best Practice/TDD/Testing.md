# Testing

Testing is a [[Best Practice(s)]] for any project, especially when intended for production.

## Unit Tests
Unit tests are automated tests that check a small, isolated piece of code (a "unit"), such as a function or a method. They are the foundation of a solid testing strategy.

**Benefits of Unit Tests:**
- **Fast Feedback:** They run very quickly, providing immediate feedback on whether a change has broken something.
- **Easier Debugging:** When a unit test fails, it points to a specific piece of code, making it easier to find and fix the bug.
- **Living Documentation:** Unit tests can serve as documentation for the code, showing how it is intended to be used.

### Red / Green Refactoring
This is the core cycle of Test-Driven Development (TDD).
1.  **Red:** Write a failing test for a new feature or a bug fix. The test should fail because the code to make it pass has not been written yet.
2.  **Green:** Write the simplest possible code to make the test pass.
3.  **Refactor:** Improve the code you just wrote without changing its behavior. The tests should still pass after refactoring.

## Integration Tests
Integration tests verify that different parts of the application work together correctly. For example, an integration test might check if the application can successfully connect to the database and retrieve data.

## Smoke Tests
Smoke tests are a small set of tests that are run to verify that the most critical functionalities of the application are working. They are usually run after a new build to quickly check if the application is stable enough for further testing.

## Penetration Testing
Also known as "pen testing", this is a simulated cyber attack against your computer system to check for exploitable vulnerabilities. It is a crucial practice for ensuring the security of your application.

---

## More Testing Practices

### Test-Driven Development (TDD)
TDD is a software development process where you write tests *before* you write the code. The process is:
1.  Write a failing test.
2.  Write the code to make the test pass.
3.  Refactor the code.

This approach leads to better code design and higher test coverage.

### Behavior-Driven Development (BDD)
BDD is an extension of TDD that focuses on the behavior of the application from the user's perspective. BDD tests are written in a natural language format (like Gherkin) that can be understood by non-technical stakeholders.

**Example of a BDD scenario (using Gherkin syntax):**
'''gherkin
Feature: User login
  Scenario: Successful login
    Given I am on the login page
    When I enter my username and password
    And I click the "Login" button
    Then I should be redirected to my dashboard
'''

### End-to-End Testing
End-to-end (E2E) tests simulate a real user's workflow from start to finish. They test the entire application, from the user interface to the backend services and databases. E2E tests are slow and can be brittle, but they are essential for ensuring that the application works as a whole.

### Property-Based Testing
Instead of writing tests for specific inputs and outputs, property-based tests check that your code holds true for a wide range of automatically generated inputs. This can help you find edge cases that you might not have thought of.

### Fuzz Testing
Fuzz testing (or fuzzing) is an automated software testing technique that involves providing invalid, unexpected, or random data as inputs to a computer program. The program is then monitored for exceptions such as crashes, failing built-in code assertions, or potential memory leaks.

### Mutation Testing
Mutation testing is a technique used to evaluate the quality of your tests. It involves making small, random changes ("mutations") to your source code and then running your tests. If your tests fail, it means they are effective at catching bugs. If they pass, it means your tests are not good enough and need to be improved.

### Contract Testing
Contract testing is a technique for testing the interactions between different services in a a microservices architecture. It ensures that each service adheres to a shared understanding (a "contract") of how they should communicate with each other.

### Performance Testing
Performance testing is a non-functional testing technique that measures the speed, responsiveness, and stability of a computer, network, software program, or device under a workload.
- **Load Testing:** Simulates a specific number of concurrent users to see how the system behaves.
- **Stress Testing:** Pushes the system beyond its limits to see how it fails.
- **Soak Testing:** Keeps the system under a significant load for an extended period to check for issues like memory leaks.

### Usability Testing
Usability testing is a technique used in user-centered interaction design to evaluate a product by testing it on users. This can be seen as an irreplaceable usability practice, since it gives direct input on how real users use the system.

---
#Testing 