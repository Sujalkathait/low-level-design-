# 13 - Clean Code & Engineering Craftsmanship

Writing clean code is about communicating intent clearly to other developers and interviewers. Code should read like well-crafted prose.

---

## 💎 Core Principles of Clean C++

### 1. Intent-Revealing Names
- Avoid generic names (`data`, `temp`, `manager`, `process`).
- Use precise domain terminology (`SpotAllocationStrategy`, `TicketExpirationTimer`).

### 2. Method Size and Focus
- Keep methods under 20-25 lines.
- Each function should do **one thing well**.
- Command-Query Separation (CQS): Functions should either modify state or return a value, not both unexpectedly.

### 3. Modern Idiomatic C++
- Avoid raw pointers for ownership; use `std::unique_ptr` and `std::shared_ptr`.
- Pass read-only parameters by `std::string_view`, `std::span`, or `const T&`.
- Mark non-mutating member functions as `const`.
- Mark single-argument constructors as `explicit` to prevent unintended implicit conversions.
- Use `[[nodiscard]]` for functions where ignoring return values leads to bugs (e.g. `acquireLock()`, `validate()`).

---

## 🚫 Common Code Smells to Avoid

- **Magic Numbers**: Replace hardcoded values with `constexpr` constants or scoped enums (`enum class`).
- **Feature Envy**: Methods that use data from another class more than their own.
- **Deep Nesting**: Use guard clauses and early returns instead of 4+ levels of `if-else` indentation.
- **Global Mutable State**: Avoid global variables and unbounded singletons.
