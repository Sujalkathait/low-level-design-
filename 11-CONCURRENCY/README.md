# 11 - Concurrency & Thread-Safe System Design

In senior engineering interviews, demonstrating thread safety for shared state (e.g. concurrent seat reservations, parking slot allocation, ATM transactions) separates good candidates from exceptional candidates.

---

## 🔒 Concurrency Primitives in Modern C++

| Primitive | Header | Use Case |
|---|---|---|
| `std::mutex` | `<mutex>` | Exclusive mutual exclusion lock |
| `std::lock_guard` / `std::scoped_lock` | `<mutex>` | RAII-based automatic locking & deadlock prevention |
| `std::shared_mutex` | `<shared_mutex>` | Reader-Writer lock (concurrent reads, exclusive writes) |
| `std::condition_variable` | `<condition_variable>` | Producer-Consumer thread synchronization |
| `std::atomic<T>` | `<atomic>` | Lock-free thread-safe counters, flags, and pointers |
| `std::jthread` (C++20) | `<thread>` | Auto-joining, cooperatively interruptible thread |

---

## 🛡️ Thread-Safe Design Patterns

### 1. Concurrent In-Memory Cache (Reader-Writer Lock)
```cpp
#include <shared_mutex>
#include <unordered_map>
#include <optional>
#include <string>

template <typename K, typename V>
class ThreadSafeCache {
private:
    mutable std::shared_mutex mutex_;
    std::unordered_map<K, V> cache_;

public:
    std::optional<V> get(const K& key) const {
        std::shared_lock lock(mutex_); // Multiple threads can read simultaneously
        auto it = cache_.find(key);
        if (it != cache_.end()) return it->second;
        return std::nullopt;
    }

    void put(const K& key, const V& value) {
        std::unique_lock lock(mutex_); // Only one thread can write
        cache_[key] = value;
    }
};
```

---

## ⚠️ Deadlock Prevention Rules
1. **Always use `std::scoped_lock(m1, m2)`** when acquiring multiple locks simultaneously.
2. **Never invoke external alien callbacks while holding a lock** (prevents callback deadlock).
3. **Minimize lock scope**: acquire late, release early.
