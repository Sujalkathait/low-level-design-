# 08 - Design Pattern Selection & Anti-Overengineering

A critical skill in senior LLD interviews is knowing when **not** to use a design pattern. Premature pattern usage causes unnecessary indirection, cognitive load, and boilerplates.

---

## 🧭 Pattern Selection Decision Framework

```mermaid
flowchart TD
    Q1{Do you need runtime algorithmic flexibility?}
    Q1 -- Yes --> Strategy[Use Strategy Pattern]
    Q1 -- No --> Q2{Are you composing part-whole hierarchies?}
    Q2 -- Yes --> Composite[Use Composite Pattern]
    Q2 -- No --> Q3{Do objects transition between distinct states with unique behaviors?}
    Q3 -- Yes --> State[Use State Pattern]
    Q3 -- No --> Q4{Do you need one-to-many event notification?}
    Q4 -- Yes --> Observer[Use Observer Pattern]
    Q4 -- No --> Simple[Keep it Simple: Simple Class or Function]
```

---

## ⚖️ Trade-off Matrix

| Requirement | Right Choice | Over-Engineered Trap |
|---|---|---|
| Single creation point with 2 variations | Simple Factory function | Abstract Factory with 5 factory classes |
| Variable configuration parameters | Builder pattern | 15 overloaded constructors |
| Passing a small callback | `std::function` or lambda | Heavyweight Command object hierarchy |
| Notification to 1 subscriber | Direct method call / delegate | Heavyweight Pub/Sub broker |
