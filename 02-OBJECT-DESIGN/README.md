# 02 - Object Design Principles & Advanced Lifecycle

Object design is the discipline of decomposing systems into cohesive, loosely coupled objects with clearly defined responsibilities, clean encapsulation boundaries, and explicit ownership lifecycles.

---

## 🎯 Core Themes in This Module

1. **Responsibility Assignment**: Establishing high cohesion, avoiding god classes, and adhering to Single Responsibility.
2. **Coupling Minimization**: Maintaining loose coupling, programming to interfaces, and eliminating circular dependencies.
3. **Behavioral Boundaries**: Enforcing the Law of Demeter and the "Tell, Don't Ask" principle.
4. **Domain Modeling**: Distinguishing Entities (identity-based) from Value Objects (value-based) and Service Objects.
5. **Advanced Lifecycle & Ownership**: Shared vs exclusive ownership, dependency injection (Constructor, Method), and immutability.

---

## 📋 Comprehensive Topic Roadmap

### Part 1: Core Object Design Principles (25 Topics)

| # | Topic | Focus & Architectural Value |
|:---:|---|---|
| **01** | **Identifying Objects** | Extracting natural domain nouns and boundaries from specifications. |
| **02** | **Identifying Responsibilities** | Defining what an object knows, does, and decides. |
| **03** | **Assigning Responsibilities** | Distributing responsibilities using GRASP patterns (Information Expert, Controller). |
| **04** | **Encapsulation Boundaries** | Shielding internal implementation details from external callers. |
| **05** | **Cohesion Fundamentals** | Measuring how closely related class operations and data members are. |
| **06** | **Coupling Fundamentals** | Measuring the degree of dependency between components. |
| **07** | **High Cohesion** | Designing focused classes with a single clear purpose. |
| **08** | **Low Coupling** | Minimizing knowledge between modules to prevent ripple effects during changes. |
| **09** | **Information Hiding** | Exposing contracts while concealing data representation. |
| **10** | **Programming to Interfaces** | Depending on abstract classes/interfaces rather than concrete classes. |
| **11** | **Dependency Management** | Managing directed dependencies; ensuring stability in core domain models. |
| **12** | **Separation of Concerns** | Isolating business logic, persistence, presentation, and external APIs. |
| **13** | **Composition Over Inheritance** | Favoring dynamic object assembly over static compile-time class hierarchies. |
| **14** | **Tell, Don't Ask** | Instructing objects to perform operations rather than asking for internal state. |
| **15** | **Law of Demeter** | Enforcing the principle of least knowledge (only talk to immediate friends). |
| **16** | **Immutability** | Designing thread-safe, side-effect-free objects whose state cannot change post-construction. |
| **17** | **Domain Modeling** | Translating business requirements into expressive domain structures. |
| **18** | **Entity vs Value Object** | Entities have persistent identities (ID); Value Objects are defined purely by their attributes. |
| **19** | **Service Objects** | Stateless orchestrators for operations spanning multiple domain entities. |
| **20** | **Repository Concept** | Mediating between domain entities and data mapping/persistence layers. |
| **21** | **Manager Classes** | When managers are appropriate vs when they degenerate into God Objects. |
| **22** | **Avoiding God Objects** | Refactoring bloated classes that know or do too much. |
| **23** | **Avoiding Anemic Domain Models** | Preventing classes that are mere bags of getters/setters without business behavior. |
| **24** | **Eliminating Tight Coupling** | Decoupling classes using abstract interfaces, callbacks, and events. |
| **25** | **Resolving Circular Dependencies** | Breaking cycles using forward declarations, mediator interfaces, or event buses. |

### Part 2: Advanced Object Design & Lifecycle (Integrated)

| Topic | Key Concept | Implementation Strategy in C++ |
|---|---|---|
| **Immutable vs Mutable Objects** | State permanence after creation | Const member variables, factory creation functions, no mutators. |
| **Object Ownership Models** | Exclusive vs Shared vs Weak | `std::unique_ptr` (exclusive), `std::shared_ptr` (shared), `std::weak_ptr` (non-owning observer). |
| **Dependency Lifetime** | Lifetime coordination | Ensuring dependent services do not outlive their injected dependencies. |
| **Dependency Injection (DI)** | Inversion of control | Constructor injection (`explicit Service(std::shared_ptr<IRepository>)`). |
| **Pluggable Architecture** | Dynamic extensibility | Registering component factories into a service locator or plugin manager. |
