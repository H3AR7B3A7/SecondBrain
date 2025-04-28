# Spring Modulith

Spring Modulith is an opinionated toolkit built on top of Spring Boot that aims to simplify the development of well-structured and maintainable modular monolith applications. Instead of immediately jumping to a microservices architecture, which can introduce significant complexity, Spring Modulith allows you to build a single deployable unit that is logically divided into distinct modules based on business domains.

## Core Concepts and Features

- **Application Modules:** Spring Modulith enables you to define logical boundaries within your application based on business capabilities or domains. These modules are typically represented by top-level packages in your codebase (e.g., `com.example.order`, `com.example.customer`).
- **Module Encapsulation:** It enforces clear boundaries between these modules, primarily through package visibility rules. By default, a module can access the public content of other modules but cannot access their internal sub-packages, promoting loose coupling.
- **Dependency Management:** Spring Modulith helps manage dependencies between modules. It allows you to define explicit dependencies and can verify that modules adhere to these constraints, preventing unwanted coupling and cyclic dependencies.
- **Inter-Module Communication:**
    - **Direct Invocation (with caution):** While allowing direct calls between modules, Spring Modulith encourages mindful usage to avoid tight coupling.
    - **Application Events:** It provides a robust mechanism for asynchronous, event-driven communication between modules. This leverages Spring's Application Events with enhancements for transactional outbox patterns, ensuring reliable event delivery even in case of failures.
    - **Named Interfaces:** You can explicitly expose specific interfaces from a module for other modules to use, further defining clear contracts.
- **Testing Support:**
    - **Individual Module Testing:** Spring Modulith facilitates testing modules in isolation, allowing you to focus on the specific logic within a module without the need to spin up the entire application.
    - **Integration Testing:** It also supports integration testing of взаимодействующих modules, especially in the context of event-driven communication, providing abstractions to easily publish and verify event reception.
- **Observability:** It integrates with Spring Actuator to provide insights into the application's modular structure and inter-module communication at runtime. This includes a dedicated `/actuator/modulith` endpoint. It can also generate Micrometer spans for tracing inter-module interactions.
- **Documentation:** Spring Modulith can automatically generate documentation of your application's module structure and their relationships. It can produce diagrams (using PlantUML) in formats like UML or C4, providing a visual representation of your modular design.
- **Verification of Module Structure:** It offers tooling to verify the defined module boundaries and dependency rules during build or test phases, ensuring that the application adheres to its intended modular architecture.
- **Runtime Support:** It provides features like module initialization, allowing you to run specific code within a module during application startup, and handles the order of module initialization based on dependencies.
- **Externalized Events:** Spring Modulith simplifies the process of externalizing domain events to external systems like Kafka by providing annotations and infrastructure for automatic event serialization and publishing.
- **Time Awareness:** It introduces concepts like `TimeMachine` and `@TimeEvent` to handle temporal aspects within your domain in a more explicit and testable way.

## Benefits of Using Spring Modulith

- **Improved Maintainability:** Clear module boundaries and enforced encapsulation make it easier to understand, modify, and maintain different parts of the application independently.
- **Enhanced Testability:** The ability to test modules in isolation simplifies unit testing and makes integration tests more focused.
- **Better Organization:** It promotes a more organized and domain-driven structure for your codebase, making it easier for development teams to collaborate and understand the system.
- **Reduced Complexity Compared to Microservices:** For applications that don't yet require the full complexity of a distributed microservices architecture, Spring Modulith offers a way to achieve modularity within a simpler deployment model.
- **Gradual Migration to Microservices:** The well-defined module boundaries created with Spring Modulith can serve as a solid foundation for a future migration to microservices if the application's scale and complexity eventually necessitate it. You can potentially extract modules as independent services with less effort.
- **Cost-Effective:** By staying within a single deployment unit, you avoid the operational overhead associated with managing multiple services (e.g., inter-service communication, network configuration, distributed monitoring).
- **Faster Development Cycles (initially):** Setting up and deploying a modular monolith can be simpler and faster than setting up a distributed microservices environment from the start.

_In summary, Spring Modulith provides a powerful set of tools and conventions for building modular and maintainable Spring Boot applications within a monolithic deployment model. It helps bridge the gap between traditional monolithic architectures and the complexity of microservices, offering a balanced approach for many applications._

---

*Work in progress...*
