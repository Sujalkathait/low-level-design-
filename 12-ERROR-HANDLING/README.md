# 12 - Error Handling & Exception Safety

Robust Low-Level Design accounts for failure modes gracefully. In C++, choosing the right error reporting mechanism determines code readability, performance, and exception safety guarantees.

---

## 🛡️ The 4 Levels of Exception Safety Guarantees

1. **Nothrow (noexcept) Guarantee**:
   - The function will never throw or propagate exceptions.
   - Required for: Move constructors, move assignments, swap functions, destructors.
2. **Strong Exception Guarantee (Commit-or-Rollback)**:
   - If an exception occurs, the system state remains exactly as it was before the call.
   - Implemented via: Copy-and-swap idiom, transactional mutations.
3. **Basic Exception Guarantee**:
   - If an exception occurs, no memory is leaked and objects remain in a valid, destructible state.
   - Implemented via: RAII smart pointers (`std::unique_ptr`, `std::shared_ptr`).
4. **No Guarantee**:
   - Resource leaks or undefined behavior occur upon exception. (Forbidden in production code).

---

## ⚖️ Modern C++ Failure Modeling Strategies

| Mechanism | Standard | Best For | Trade-offs |
|---|---|---|---|
| **Exceptions (`throw`/`catch`)** | C++98+ | Exceptional, non-recoverable operational failures | Stack unwinding overhead, hard to trace in low-latency systems |
| **`std::optional<T>`** | C++17 | Queries that may validly return nothing (e.g., cache lookup) | Cannot explain *why* lookup failed |
| **`std::expected<T, E>`** | C++23 | Recoverable domain errors (e.g., validation, parsing) | Zero-overhead, explicit functional error checking |
| **Result Status Codes** | Custom | High-frequency trading, real-time audio | Requires disciplined caller checks |
