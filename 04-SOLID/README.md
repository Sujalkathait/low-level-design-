# 04 - SOLID Principles in Modern C++

The SOLID principles are the bedrock of maintainable, extensible object-oriented systems.

---

## 🏛️ The Five Principles

| Acronym | Principle | Core Essence in C++ | Anti-Pattern to Avoid |
|:---:|---|---|---|
| **S** | **Single Responsibility (SRP)** | A class should have one, and only one, reason to change. | God Class / Monster Manager |
| **O** | **Open/Closed (OCP)** | Software entities should be open for extension, but closed for modification. | Massive `switch`/`if-else` type inspections |
| **L** | **Liskov Substitution (LSP)** | Subtypes must be substitutable for their base types without altering correctness. | Throwing `NotSupportedException` in derived classes |
| **I** | **Interface Segregation (ISP)** | Clients should not be forced to depend upon interfaces they do not use. | Fat Interfaces with 20+ unrelated methods |
| **D** | **Dependency Inversion (DIP)** | High-level modules should not depend on low-level modules; both should depend on abstractions. | Direct instantiation via `new ConcreteService()` |

---

## ⚡ C++ Specific Idioms for SOLID

- **SRP**: Separate domain logic from persistence, serialization, and presentation.
- **OCP**: Use abstract strategy interfaces (`std::unique_ptr<IStrategy>`) or `std::function` callbacks.
- **LSP**: Adhere strictly to preconditions (derived class cannot strengthen them) and postconditions (derived class cannot weaken them).
- **ISP**: Split large abstract base classes into lightweight mixins or pure interfaces (e.g. `IReadable`, `IWritable`).
- **DIP**: Pass interfaces via constructor dependency injection (`std::shared_ptr<IRepository>` or reference wrappers).
