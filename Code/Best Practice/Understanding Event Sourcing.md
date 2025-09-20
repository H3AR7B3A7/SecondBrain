# Event Sourcing

Summary: Understanding Event Sourcing, by Martin Dilger

## Part I: Foundations

### Chapter 1: Why You Should Care

Event Sourcing stores facts as they happen chronologically rather than just current state. Instead of updating a customer record, you store events like "Customer Created," "Address Changed," "Upgraded to Premium." This preserves the dimension of time - you know not just what the current state is, but how it came to be. This historical data enables insights impossible with traditional CRUD systems (like analyzing purchase patterns after moving). The key principle: "Not losing information" - you keep data readily available because you don't know what might be useful later.

### Chapter 2: Event Sourcing - What Is It?

The chapter opens with a charming example of children naturally discovering Event Sourcing through a toy sale, using price tags as events to track sales. Core concepts include:

- **Events**: Immutable facts about what happened (past tense)
- **Event Streams**: Chronological sequences of events for entities
- **Event Store**: Specialized database for append-only event storage
- **Projections**: Different views built from events (reports, UI views, etc.)

Common misconceptions debunked:

- Complexity: Actually simpler than evolving rigid schemas
- Performance: Properly designed streams handle thousands of events in milliseconds
- Coupling: Not inherent to Event Sourcing but an architectural choice
- Not the same as Event Streaming (Kafka)
- No special tools required (can use PostgreSQL)

### Chapter 3: Planning Systems Using Event Modeling

Event Modeling is a visual technique for planning systems on a timeline. Core elements:

- **Events** (orange): Facts that happened
- **Commands** (blue): Instructions to the system
- **Read Models** (green): Queries for stored data
- **Screens**: UI mockups for clarity

Four main patterns:

1. **State Change**: Command → Event (writing data)
2. **State View**: Event → Read Model (reading data)
3. **Automation**: Background processes triggered by events
4. **Translation**: Converting external events to internal format

The "Information Completeness Check" ensures all data in Read Models traces back to source events, preventing assumptions about data availability.

### Chapter 4: CQRS, Concurrency, Eventual Consistency

**CQRS** (Command Query Responsibility Segregation) separates write operations from read operations, often using different models and databases. This enables optimization - reads happen more frequently and can use denormalized, cached data.

**Consistency** challenges arise when multiple systems need updates. Solutions include:

- Same transaction updates (simple but coupled)
- Eventual consistency (updates propagate with small delays)

**Concurrency** is handled through optimistic locking on event streams - you can only append events if no others were added since you last read.

### Chapter 5: Internal Versus External Data

Critical distinction between internal domain events (can change freely) and external integration events (stable contracts with other systems). Key principles:

- Internal events capture state changes within a bounded context
- External events are versioned contracts between systems
- Translations shield internal domain from external changes
- Avoid letting external systems read internal events directly (creates coupling)

### Chapter 6: The Anatomy of an Event-Sourced Application

Building blocks explained:

- **Command Handlers**: Process commands, validate rules
- **Aggregates**: Enforce business invariants, ensure consistency
- **Event Sourcing Handlers**: Rebuild aggregate state from events
- **Projectors**: Update read models from events
- **Query Handlers**: Retrieve data from projections

The flow: Command → Command Handler → Aggregate → Event → Projectors → Read Models → Query Handlers

### Chapter 7: Event Streaming, Event Sourcing and Stream Design

Event Streaming (Kafka) is about moving data between systems in real-time. Event Sourcing is about storing state changes. They're fundamentally different:

- Streaming: Infinite streams, millions of events/second, technical focus
- Sourcing: Finite streams (10-100 events typically), business meaning

Stream design strategies:

- Keep streams short using "Closing the Books" pattern
- Use swimlanes in Event Modeling to define boundaries
- Summary events to partition long streams
- Snapshots as last resort for performance

### Chapter 8: Domain Driven Design

DDD concepts relevant to Event Sourcing:

- **Ubiquitous Language**: Common vocabulary between business and IT
- **Bounded Contexts**: Clear boundaries where terms have specific meaning
- **Aggregates**: Clusters ensuring transactional consistency
    - Root entity as entry point
    - Enforces invariants
    - Transaction boundary

Event Modeling naturally supports DDD by forcing clear language and boundaries.

### Chapter 9: Handling Transactions in Distributed Systems Using Sagas

Sagas manage data consistency across services without distributed transactions. Two approaches:

1. **Orchestration**: Central coordinator manages the process
2. **Choreography**: Services react to events independently

Challenges include handling partial failures and compensating transactions. The author prefers the simpler "Processor-TODO-List" pattern over complex Saga implementations.

### Chapter 10: Vertical Slicing

Vertical Slice Architecture organizes code by features rather than layers. Each slice contains all layers (UI, API, domain, persistence) for one feature. Benefits:

- Minimizes coupling between features
- Changes typically affect only one slice
- Scales development (developers work independently)
- Natural fit with Event Modeling

Trade-offs include some code duplication and need for tooling to enforce boundaries.

## Part II: Modeling the System

### Chapter 11: Brainstorming

Starting an e-commerce cart system. Initial requirements gathered through collaborative Event Modeling session using sticky notes. Process:

1. Write events in past tense (what happened)
2. No wrong answers initially
3. Arrange chronologically
4. Read as a story to validate

The Project Paradox: Most critical decisions made when least is known about the system.

### Chapter 12: Modeling Use Cases with Wireframes

Wireframes aren't about perfect UX but ensuring data flow clarity. Working backwards:

- From screens, identify needed data
- From Read Models, trace to source events
- From events, define triggering commands

The "backwards thinking" focuses on solutions rather than problems, leading to simpler implementations.

### Chapter 13: Given/When/Then Scenarios

Business rules captured as executable specifications:

- **Given**: System state (events)
- **When**: Action (command)
- **Then**: Expected outcome (events or errors)

Example: "GIVEN 3 items in cart, WHEN adding another item, THEN expect error (max 3 items allowed)"

These scenarios placed under slices provide complete behavioral documentation.

### Chapter 14: Clear Cart

Modeling the clear cart functionality reveals missing concepts like cart session identifier (aggregateId). Information Completeness Check forces explicit data flow - every attribute must have a source. Read Models can aggregate data from multiple event types.

### Chapter 15: Submit Cart

Cart submission involves internal processing and external communication. Pattern:

1. Submit Cart command → Cart Submitted event (internal)
2. Automation reads submitted cart data
3. Publish Cart command → External Cart Published event

Separation of internal/external events prevents coupling and provides stable integration contracts.

### Chapter 16: Inventory Changed

External inventory changes translated to internal events. Business rules:

- Can't add out-of-stock items
- Don't remove existing out-of-stock items from cart
- Can't submit cart with out-of-stock items

Translation Pattern shields internal domain from external system changes, acting as Anti-Corruption Layer.

### Chapter 17: Price Changed

Complex automation: when price changes, affected items must be archived in all active carts. Process:

1. External price change notification
2. Translation to internal event
3. Read Model tracks which carts contain which products
4. Automation archives affected items

Demonstrates power of event-based systems for complex business rules.

### Chapter 18: Structuring an Event Model

Practical extensions for complex models:

- Chapters/sub-chapters for logical grouping
- Multiple models per board
- Alternative flows for error cases
- Model context annotations

These aren't official Event Modeling notations but practical tools for managing complexity.

## Part III: From Zero to Running Software

### Chapter 19: Technology Stack

Implementation uses:

- Kotlin (JVM language)
- Spring Framework & Spring Modulith
- Axon Framework (CQRS/Event Sourcing)
- PostgreSQL
- Test Containers

Vertical Slice Architecture with packages mirroring Event Model slices.

### Chapter 20: Brief Introduction to Axon

Axon Framework provides:

- Event Store abstraction
- Aggregates with lifecycle management
- Command/Event Handlers
- Event Processors (Subscribing vs Streaming/Tracking)
- Query abstraction

Key distinction: Subscribing processors are synchronous, Streaming processors are eventually consistent.

### Chapter 21: Implementing the First Slice - "Add Item"

Test-first approach using Given/When/Then from Event Model. Implementation:

1. Generate test from GWT scenario
2. Implement Command Handler on Aggregate
3. Apply events using AggregateLifecycle
4. Event Sourcing Handlers rebuild state

Key insight: Command Handlers validate and apply events but don't change aggregate state directly - that happens in Event Sourcing Handlers.

### Chapter 22: State View Slices Using Live Projections

Live Projections calculate views from events in real-time for each request. Implementation:

1. Load events from Event Store
2. Apply events to build projection
3. Return via Query Handler

Benefits: No eventual consistency, always latest state. Trade-off: More CPU usage per request.

### Chapter 23: Remove-Item and Clear-Cart

Critical distinction reinforced: Command Handlers only validate and decide; Event Sourcing Handlers change state. This separation ensures aggregates are always in valid state since validation happened during command processing.

### Chapter 24: Apache Kafka Integration and Translations

External events (from Kafka) translated to internal commands/events:

1. Kafka Listener receives external event
2. Issues internal command
3. Command Handler creates internal event

Translation slices shield domain from infrastructure, with external events hidden in internal packages.

### Chapter 25: Database Projection for Inventories

Database projections for complex queries or multiple streams:

1. JPA entities for persistence
2. Projectors with @EventHandler update tables
3. Query Handlers abstract data access

Error handling options: ignore, stop processing, or Dead Letter Queue.

### Chapter 26: Implementing Automations

Price change automation demonstrates complex background processing:

1. Build "Carts with Products" Read Model
2. React to price changes
3. Issue commands for affected carts

Handling eventual consistency: subscribing processors, in-memory cache, or accept delays.

### Chapter 27: Submitting the Cart

Dual-write problem when publishing to Kafka and Event Store. Solutions:

- Transactional Outbox Pattern
- Synchronized transactions
- Explicit error modeling (Cart Publication Failed event)

### Chapter 28: Handling Breaking Changes

Upcasters transform old event versions to new ones during deserialization. Process:

1. Add @Revision annotation for new version
2. Implement SingleEventUpcaster
3. Transform JSON representation

Event replays rebuild projections with new fields. Mark side-effect handlers with @DisallowReplay.

## Part IV: Implementation Patterns

### Chapter 30: Database Projected Read Model

Projects events to database tables optimized for queries. Not normalized, one table per use case. Implementation: Entity, Repository, Projector, Query Handler.

### Chapter 31: Live Model

Calculates projections from events on each request. Best for single streams with limited events. No eventual consistency but higher CPU usage.

### Chapter 32: Partially Synchronous Projection

Combines database projection with in-memory cache of recent events to eliminate eventual consistency gaps while maintaining performance.

### Chapter 33: Logic Read Model

Calculations in Read Models acceptable if based only on existing events without side effects.

### Chapter 34: Snapshots

Technical optimization to reduce events processed. Store aggregate state periodically. Alternative: business-driven stream partitioning ("Closing the Books").

### Chapter 35: Processor-TODO-List Pattern

Automations as todo lists calculated from system state:

1. Read Model provides tasks
2. Processor executes commands
3. Events update todo list

Simpler alternative to complex Saga orchestration.

### Chapter 36: Reservation Pattern

Ensures consistency for limited resources across aggregates. Two approaches:

1. Database with unique constraints
2. Dedicated reservation aggregates

## Part V: The Missing Chapters

### Chapter 38: Handling Metadata

Metadata provides context (correlation IDs, user IDs, timestamps). Implementation via CorrelationDataProviders automatically attaches metadata to all messages for traceability.

### Chapter 39: Handling Security

Security as cross-cutting concern:

- Model business roles, not technical permissions
- Use metadata for authorization
- @Secured annotations on handlers
- Separate domain from infrastructure

### Chapter 40: GDPR - Handling Sensitive Data

Approaches for GDPR compliance:

1. **Crypto-shredding**: Encrypt PII with per-user keys, delete keys for erasure
2. **Forgettable Payloads**: Store PII separately, reference in events

Key principle: Data minimalism - only store what's essential.

### Chapter 41: Handling the UI

Managing eventual consistency in UIs:

1. **Fenced Polling**: Track projection versions, poll until updated
2. **Server-Sent Events**: Real-time notifications via subscriptions

Key insight: Return aggregate version after commands, enabling clients to know when projections are current.

## Conclusion

The book provides a complete journey from Event Sourcing theory through practical implementation. Core themes throughout:

- Focus on information flow, not technology
- Model behavior, not structure
- Embrace eventual consistency
- Use patterns repeatedly
- Keep slices independent
- Test behavior, not implementation

The author emphasizes this isn't about perfect architecture but finding what works through iterative improvement while maintaining flexibility through Event Sourcing's inherent capabilities.