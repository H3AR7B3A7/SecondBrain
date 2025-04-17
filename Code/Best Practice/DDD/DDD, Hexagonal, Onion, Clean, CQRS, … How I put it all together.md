# DDD, Hexagonal, Onion, Clean, CQRS, … How I put it all together

[link](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/)

The author combines various software architectural patterns such as DDD (Domain-Driven Design), Hexagonal, Onion, Clean, and CQRS to create what he calls "Explicit Architecture". It aims to provide a structured approach to software design, emphasizing clear separation of concerns and maintainability.

## Key concepts discussed in the article:

- **Ports and Adapters:** This architecture explicitly separates the application's internal code from external code. It identifies three fundamental blocks: user interface code, application core (business logic), and infrastructure code (connecting to tools like databases).
- **Application Core:** The most important part of the system, containing the business logic. It should be independent of the user interface and infrastructure.
- **Tools:** External resources used by the application, such as database engines, search engines, web servers, and CLI consoles.
- **Adapters:** Code units that connect tools to the application core. Primary (Driving) Adapters tell the application to do something, while Secondary (Driven) Adapters are told by the application to do something.
- **Ports:** Specifications defining how tools interact with the application core. They are typically interfaces that belong within the business logic.
- **Inversion of Control:** The principle where dependencies point towards the application core, making it independent of specific tools or adapters.

## Organization of the Application Core, drawing from Onion Architecture and DDD:

- **Application Layer:** Contains use cases and application services, defining business processes. It also includes Ports & Adapters interfaces.
- **Domain Layer:** Contains the domain logic, independent of business processes. It includes Domain Services and the Domain Model.
- **Domain Services:** Handle domain logic that involves multiple entities.
- **Domain Model:** The core, containing business objects (Entities, Value Objects, Enums) and Domain Events.

## Importance of component-based architecture:

- **Components:** Coarse-grained segregation of code based on sub-domains or bounded contexts (e.g., Authentication, Billing).
- **Decoupling:** Components should be loosely coupled, using techniques like Dependency Injection and avoiding direct knowledge of other components.
- **Communication:** Components can interact through events, shared kernels, or eventual consistency.

## Explicit Architecture, combines these patterns to create a system where:

- The application core is at the center, independent of external tools and UIs.
- Layers organize the business logic, with dependencies pointing inwards.
- Components provide a higher-level structure based on domain concepts.
- Clear boundaries and interfaces (Ports) define interactions between different parts of the system.

_While these patterns provide a good foundation, the specific implementation should always be tailored to the application's needs and context._

---

*Work in progress...*
