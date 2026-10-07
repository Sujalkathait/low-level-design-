# 06 - Structural Design Patterns in Modern C++

Structural patterns are concerned with how classes and objects are composed to form larger, flexible structures while keeping the parts independent.

---

## 🏛️ The 7 Structural Patterns

| Pattern | Intent | Key C++ Mechanism |
|---|---|---|
| **Adapter** | Convert the interface of a class into another interface clients expect | Wrapper class holding adaptee instance or inheritance |
| **Bridge** | Decouple an abstraction from its implementation so that both can vary independently | PImpl idiom (`std::unique_ptr<Impl>`) |
| **Composite** | Compose objects into tree structures to represent part-whole hierarchies | Vector of `std::shared_ptr<Component>` / tree traversal |
| **Decorator** | Attach additional responsibilities to an object dynamically | Wrapper class implementing component interface and holding component pointer |
| **Facade** | Provide a unified, simplified high-level interface to a set of interfaces in a subsystem | Co-ordinating controller class |
| **Flyweight** | Use sharing to support large numbers of fine-grained objects efficiently | Factory cache with immutable shared state (`std::shared_ptr`) |
| **Proxy** | Provide a surrogate or placeholder for another object to control access to it | Smart pointers, virtual proxy, or access-control guard |

---

## 💡 Top Interview Selection: Decorator vs Adapter vs Facade

- **Adapter**: Changes an existing interface to match client expectations.
- **Decorator**: Enhances an interface without changing its signature.
- **Facade**: Simplifies and aggregates multiple complex subsystem interfaces.
