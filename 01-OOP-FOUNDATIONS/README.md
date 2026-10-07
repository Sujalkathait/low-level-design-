# 01 - Object-Oriented Programming (OOP) Foundations & Modern C++ Mechanics

Mastering Low-Level Design (LLD) starts with deep fluency in Object-Oriented Programming (OOP) fundamentals and understanding the underlying C++ object model, memory layout, and Modern C++ language mechanics.

---

## 🎯 Core Themes in This Module

1. **Object Model & Memory Layout**: Class blueprint vs runtime object instantiation, struct/class memory padding, alignment, and vtable pointer (`vptr`) overhead.
2. **Strict Encapsulation**: Enforcing domain invariants with `private`, `protected`, and `public` access boundaries.
3. **Object Lifecycle & Resource Ownership**: Deterministic resource management (RAII), copy/move semantics, Rule of 0/3/5, and smart pointer ownership.
4. **Polymorphic Dispatch**: Compile-time (templates, overloading, CRTP) vs runtime (virtual functions, pure virtual interfaces, dynamic dispatch).
5. **Object Relationships**: Composition (HAS-A strong), Aggregation (HAS-A weak), Association (USES-A), and Inheritance (IS-A).

---

## 📋 Comprehensive Topic Roadmap

### Part 1: OOP Foundations (25 Topics)

| # | Topic | Status | Focus & Description |
|:---:|---|:---:|---|
| **01** | [Class & Objects](01-Class-and-Objects/) | ✅ Ready | Class definition, object instantiation, memory allocation, encapsulation. |
| **02** | [Access Modifiers](02-Access-Modifiers/) | ✅ Ready | `public`, `protected`, and `private` scoping and access rules. |
| **03** | Encapsulation & Data Hiding | ⏳ Planned | Invariant preservation, getters/setters, protecting internal state. |
| **04** | Constructors & Initialization | ⏳ Planned | Default, parameterized, explicit, and member initializer lists. |
| **05** | Destructors & Cleanup | ⏳ Planned | Deterministic cleanup, stack unwinding, virtual destructors. |
| **06** | Copy Constructors | ⏳ Planned | Deep vs shallow copying, preventing double-free errors. |
| **07** | Copy Assignment Operator | ⏳ Planned | Copy-and-swap idiom, self-assignment guards, exception safety. |
| **08** | Inheritance Fundamentals | ⏳ Planned | Code reuse, base class subobjects, IS-A modeling in C++. |
| **09** | Single Inheritance | ⏳ Planned | Base/derived construction order and member resolution. |
| **10** | Multilevel Inheritance | ⏳ Planned | Hierarchy depth, fragility of deep base classes. |
| **11** | Multiple Inheritance | ⏳ Planned | Mixin classes, the diamond problem, and `virtual` base inheritance. |
| **12** | Hierarchical Inheritance | ⏳ Planned | Branching class structures and shared parent interfaces. |
| **13** | Virtual Functions & Vtables | ⏳ Planned | Dynamic dispatch, vptr mechanics, memory overhead, vtable layout. |
| **14** | Pure Virtual Functions | ⏳ Planned | Abstract contracts, enforcing derived class implementation. |
| **15** | Abstract Classes | ⏳ Planned | Incomplete base classes, interface segregation in C++. |
| **16** | Compile-Time Polymorphism | ⏳ Planned | Function overloading, templates, and CRTP (zero-cost dispatch). |
| **17** | Runtime Polymorphism | ⏳ Planned | Base pointers/references invoking overridden virtual functions. |
| **18** | Function Overloading | ⏳ Planned | Signature differentiation, `const` overloading, name mangling. |
| **19** | Operator Overloading | ⏳ Planned | Custom operators (`<<`, `==`, `[]`), canonical idioms. |
| **20** | Composition | ⏳ Planned | Strong HAS-A relationship (part-whole with identical lifecycles). |
| **21** | Aggregation | ⏳ Planned | Weak HAS-A relationship (independent lifecycles, shared pointers). |
| **22** | Association | ⏳ Planned | Peer-to-peer relationships between decoupled entities. |
| **23** | Dependency | ⏳ Planned | Transient USES-A relationship, method parameter coupling. |
| **24** | IS-A vs HAS-A | ⏳ Planned | Decision framework: when to inherit vs when to compose. |
| **25** | Composition vs Inheritance | ⏳ Planned | Preferring composition for flexibility, testability, and decoupling. |

### Part 2: Modern C++ Language Mechanics (Integrated)

| Topic | Modern C++ Feature | Architectural Implication in LLD |
|---|---|---|
| **RAII** | Scope-bound resource management | Guarantee zero leaks without manual `delete` or cleanup calls. |
| **Smart Pointers** | `std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr` | Express explicit ownership semantics; eliminate dangling pointers and cycles. |
| **Move Semantics** | Rvalue references (`&&`), `std::move`, `std::forward` | Zero-copy resource transfers for containers, strings, and heavy objects. |
| **Rule of 0 / 3 / 5** | Special member function generation rules | Rule of 0: let smart pointers manage resources; Rule of 5 for custom wrappers. |
| **Const-Correctness** | `const`, `const&`, `std::string_view`, `std::span` | Guarantee read-only immutability, thread-safe concurrent reads. |
| **Type Safety** | `enum class`, strong typedefs, `std::byte` | Prevent silent implicit numeric conversions and type confusion bugs. |

---

## 🚀 Building & Running Foundation Targets

```bash
# Configure and build all foundation executables
cmake -B build -G Ninja
cmake --build build

# Run targets
./build/bin/lld_01_class_and_objects
./build/bin/lld_02_access_modifiers
```
