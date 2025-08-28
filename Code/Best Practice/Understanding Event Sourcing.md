## Part I: Foundations

### Chapter 1: Why You Should Care

- Traditional CRUD systems flatten data and lose historical context.
    
- Event Sourcing preserves the full timeline of changes, enabling better insights, traceability, and flexibility.
    
- It aligns with how businesses think—tracking what happened, not just what is.
    

### Chapter 2: What Is Event Sourcing?

- Uses a toy sales stand analogy to explain events, projections, and event stores.
    
- Events are immutable facts; projections turn them into usable views.
    
- Introduces key components: event streams, projections, and event stores.
    

### Chapter 3: Planning Systems Using Event Modeling

- Event Modeling is a visual planning technique that aligns technical and non-technical stakeholders.
    
- Systems are modeled as timelines of user interactions and system responses.
    
- Encourages modeling behavior over static data.
    

### Chapter 4: CQRS, Concurrency, and Consistency

- Explains Command Query Responsibility Segregation (CQRS): separating write and read models.
    
- Discusses eventual consistency and how to handle concurrent updates using aggregates and event streams.
    

### Chapter 5: Internal vs External Data

- Differentiates internal events (used within a service) from external/integration events (shared across services).
    
- Advocates for clear boundaries to avoid tight coupling and maintain service autonomy.
    

### Chapter 6: Anatomy of an Event-Sourced Application

- Breaks down components: commands, events, aggregates, projections, and event handlers.
    
- Shows how these interact to form a robust, scalable system.
    

### Chapter 7: Event Streaming vs Event Sourcing

- Clarifies the distinction: Event Streaming (e.g., Kafka) is about real-time data flow; Event Sourcing is about storing meaningful business events.
    
- Warns against using streaming tools like Kafka as event stores.
    

### Chapter 8: Domain-Driven Design

- Connects Event Sourcing with DDD principles like bounded contexts and ubiquitous language.
    
- Emphasizes modeling behavior and aligning software with business processes.
    

### Chapter 9: Handling Transactions with Sagas

- Introduces Sagas to manage long-running, distributed transactions.
    
- Sagas coordinate multiple services through events and compensating actions.
    

### Chapter 10: Vertical Slicing

- Advocates for building features slice-by-slice (end-to-end) rather than layer-by-layer.
    
- Improves delivery speed, clarity, and testability.
    

## 🎨 Part II: Modeling the System

### Chapter 11: Brainstorming

- Collaborative ideation techniques to gather requirements and align stakeholders.
    

### Chapter 12: Modeling Use Cases with Wireframes

- Uses UI wireframes to visualize user interactions and system behavior.
    

### Chapter 13: Given/When/Then Scenarios

- Applies Gherkin syntax to define behavior-driven development (BDD) scenarios.
    

### Chapters 14–17: Use Cases

- **Clear Cart**, **Submit Cart**, **Inventory Changed**, **Price Changed**: each modeled with events, commands, and projections.
    
- Demonstrates how to translate business behavior into event-driven architecture.
    

### Chapter 18: Structuring an Event Model

- Shows how to organize events, commands, and views into a coherent model.
    
- Encourages modularity and clarity in system design.
    

## 🚀 Part III: From Zero to Running Software

### Chapter 19: Technology Stack

- Overview of tools and frameworks (Java, Spring Boot, Axon).
    

### Chapter 20: Introduction to Axon

- Axon simplifies Event Sourcing and CQRS implementation.
    
- Offers built-in support for aggregates, event stores, and projections.
    

### Chapters 21–27: Implementing Features

- Step-by-step implementation of features like Add Item, Remove Item, Clear Cart, Submit Cart.
    
- Covers projections, automations, and integrations (e.g., with Kafka).
    
- Demonstrates how to build live views and database projections.
    

### Chapter 28: Handling Breaking Changes

- Strategies for versioning events and evolving schemas safely.
    
- Emphasizes backward compatibility and event immutability.
    

## 🧠 Part IV: Implementation Patterns

### Chapter 29: Introduction to Patterns

- Introduces reusable patterns for event-sourced systems.
    

### Chapters 30–36: Patterns

- **Database Projected Read Model**: builds views from events into relational tables.
    
- **Live Model**: real-time projections for UI.
    
- **Partially Synchronous Projection**: hybrid approach for performance.
    
- **Logic Read Model**: embeds business logic in projections.
    
- **Snapshots**: optimize performance by storing intermediate states.
    
- **Processor-TODO-List**: tracks pending actions from events.
    
- **Reservation Pattern**: handles resource locking and availability.
    

## 🔒 Part V: The Missing Chapters

### Chapter 37: Why the Missing Chapter?

- Reflects on overlooked topics in Event Sourcing literature.
    

### Chapters 38–41: Practical Concerns

- **Metadata**: enriches events with context (who, when, where).
    
- **Security**: ensures safe handling of sensitive data.
    
- **GDPR**: strategies for compliance in immutable systems.
    
- **UI Design**: building interfaces for event-driven systems.
    

## 🧭 Final Chapter: Where to Go from Here?

- Encourages readers to apply the concepts, iterate, and contribute to the community.
    
- Offers guidance for evolving systems and scaling teams.