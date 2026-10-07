# 02 - Object Design Principles & Advanced Lifecycle

Object design is the discipline of breaking down systems into cohesive, loosely coupled objects. It focuses on giving each object a clear responsibility, strong boundaries, and strict rules about how it lives and dies (lifecycle).

We have combined all **25 Core Topics and Advanced Lifecycle Concepts** into this guide. **Every single topic is explained separately with its own code block!**

---

## Section 1: Responsibility & Domain Modeling

### Topic 01: Identifying Objects
The first step in design is reading the requirements and extracting the natural "nouns" (e.g., `User`, `Cart`, `Payment`, `Order`). These nouns become your objects.

**Code Example:**
```cpp
#include <iostream>
#include <string>

// Noun identified: User
class User {
public:
    std::string name;
};

// Noun identified: Cart
class Cart {
public:
    int totalItems = 0;
};
```

### Topic 02: Identifying Responsibilities
Once you have objects, you must decide what they do. A responsibility is what an object *knows* (its data) and what an object *does* (its methods).

**Code Example:**
```cpp
#include <iostream>

class Order {
private:
    // What the object KNOWS
    // Object ko kya pata hai
    double totalAmount = 50.0;
    
public:
    // What the object DOES
    // Object kya karta hai
    void printInvoice() {
        std::cout << "Invoice total: $" << totalAmount << "\n";
    }
};
```

### Topic 03: Assigning Responsibilities (GRASP)
Use patterns like "Information Expert". If an object has the information needed to perform a task, that object should be responsible for performing it. Don't let an outside class calculate things for it.

**Code Example:**
```cpp
#include <iostream>

class Wallet {
private:
    double balance = 100.0;
public:
    // Wallet is the Information Expert regarding money, so it handles the deduction
    // Wallet ke paas money ki info hai, isliye deduction yahi handle karega
    bool deduct(double amount) {
        if (balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }
};
```

### Topic 17: Domain Modeling
Translating business rules into code structures. A domain model represents real-world concepts in software.

### Topic 18: Entity vs Value Object
- **Entity**: An object with a unique identity (like a `User` with a User ID). Even if their name changes, they are the same user.
- **Value Object**: An object defined only by its attributes (like a `Date` or `Color`). It has no unique ID.

**Code Example:**
```cpp
#include <iostream>
#include <string>

// Value Object: Only data, no ID.
// Value Object: Sirf data, koi ID nahi.
class Address {
public:
    std::string city;
    Address(std::string c) : city(c) {}
};

// Entity: Identified by its unique ID.
// Entity: Apne unique ID se pehchana jata hai.
class User {
public:
    std::string userId;
    Address address;
    User(std::string id, Address addr) : userId(id), address(addr) {}
};
```

### Topic 19: Service Objects
A stateless class that orchestrates actions between multiple entities. It does not hold any permanent data itself.

**Code Example:**
```cpp
#include <iostream>

class OrderProcessorService {
public:
    // Stateless function: It just does a job using external inputs
    // Stateless function: Ye bas apna kaam karta hai bahar ke data se
    void process(User& user) {
        std::cout << "Processing order for user: " << user.userId << "\n";
    }
};
```

### Topic 20: Repository Concept
A class specifically responsible for saving entities to a database and fetching them back.

**Code Example:**
```cpp
#include <iostream>

class UserRepository {
public:
    // Handles database interaction
    // Database se baat karta hai
    void save(const User& user) {
        std::cout << "Saving User: " << user.userId << " to database.\n";
    }
};
```

### 🎯 Practice Coding Challenges (Section 1)
**Challenge 1: Entity vs Value Object**
- **Goal:** Differentiate between Objects with IDs and Objects with just values.
- **Task:** 
  - Design an `Order` class (Entity). Give it a unique `OrderID`.
  - Design a `Money` class (Value Object). Give it `currency` and `amount`.
  - The `Order` should store a `Money` object representing the total cost.

**Challenge 2: The Repository Pattern**
- **Goal:** Separate database logic from business logic.
- **Task:** 
  - Write an `InMemoryProductRepository` class.
  - Use a `std::vector` inside it to simulate a database.
  - Write methods to `save(Product)` and `findById(string id)`.

**Challenge 3: Stateless Service**
- **Goal:** Create a service that holds no state.
- **Task:** 
  - Create a `DiscountService` class.
  - Add a method `applyDiscount(Cart& cart, string promoCode)`.
  - Ensure the service itself holds no state (it should not have any class-level variables).

---

## Section 2: Cohesion, Coupling & Dependency

### Topic 05 & 07: Cohesion & High Cohesion
Cohesion measures how strongly related the responsibilities of a single class are. A class should have **High Cohesion**. It should do exactly *one* thing really well.

**Code Example:**
```cpp
// HIGH COHESION: This class only cares about Email.
// HIGH COHESION: Yeh class sirf Email ke baare mein sochti hai.
class EmailSender {
public:
    void sendEmail(std::string msg) {
        // sending logic
    }
};
```

### Topic 06 & 08: Coupling & Low Coupling
Coupling measures how strongly different classes depend on each other. We want **Low Coupling**. If Class A changes, Class B shouldn't break. 

**Code Example:**
```cpp
class Keyboard {};

class Computer {
private:
    // Low Coupling: Computer depends on a pointer, not a hard-coded object
    // Low Coupling: Computer ek pointer pe depend karta hai
    Keyboard* kb;
public:
    Computer(Keyboard* k) : kb(k) {} // Injected from outside!
};
```

### Topic 11: Dependency Management
Managing which class relies on which. You want your outer layers (UI, Database) to depend on your inner layers (Core Business Logic), never the other way around.

### Topic 25: Resolving Circular Dependencies
When Class A depends on Class B, and Class B depends on Class A. You resolve this in C++ by using forward declarations (`class B;`) and pointers.

**Code Example:**
```cpp
#include <iostream>

// Forward Declaration breaks the loop!
// Forward Declaration se loop toot jata hai!
class Developer; 

class Manager {
public:
    void assignTask(Developer* dev);
};

class Developer {
private:
    Manager* boss;
public:
    Developer(Manager* m) : boss(m) {}
    void doTask() { std::cout << "Coding...\n"; }
};

void Manager::assignTask(Developer* dev) {
    dev->doTask();
}
```

### 🎯 Practice Coding Challenges (Section 2)
**Challenge 1: Low Coupling (Constructor Injection)**
- **Goal:** Break hard dependencies.
- **Task:** 
  - You have a `Car` class that creates a `new V8Engine()` directly inside its constructor.
  - Refactor it. Make the `Car` accept an `IEngine*` interface from the outside via its constructor.

**Challenge 2: Fix the Cycle (Circular Dependency)**
- **Goal:** Break an `#include` loop.
- **Task:** 
  - Create `Class A` and `Class B` in C++. Make them call methods on each other.
  - Use forward declarations (`class B;`) so the code compiles successfully.

**Challenge 3: High Cohesion Check**
- **Goal:** Make classes do exactly one thing.
- **Task:** 
  - Imagine a `UserAccount` class with these 4 methods: `login()`, `logout()`, `sendEmail()`, and `printInvoice()`.
  - Break this single class down into 3 highly cohesive classes.

---

## Section 3: Boundaries & Behavior

### Topic 04: Encapsulation Boundaries
Shielding internal implementation details from external callers. No outside object should be able to directly modify another object's internal variables.

### Topic 09: Information Hiding
Expose *what* the object does through a clear public contract (interfaces), but hide *how* it does it.

### Topic 10: Programming to Interfaces
Always depend on abstract classes (`IEngine`) rather than concrete implementations (`V8Engine`). This makes swapping out components much easier.

**Code Example:**
```cpp
#include <iostream>

// The Interface
class IEngine {
public:
    virtual void start() = 0;
};

// Concrete implementation
class V8Engine : public IEngine {
public:
    void start() override { std::cout << "V8 Engine started!\n"; }
};

// The Car only knows about IEngine, not V8!
// Car ko sirf IEngine ke baare mein pata hai!
class Car {
private:
    IEngine* engine;
public:
    Car(IEngine* e) : engine(e) {}
    void drive() { engine->start(); }
};
```

### Topic 14: Tell, Don't Ask
Tell an object what to do, don't ask it for its internal state to make a decision outside of it.

**Code Example:**
```cpp
class Door {
private:
    bool isOpen = true;
public:
    // TELL: We tell the door to close. It handles the logic internally.
    // TELL: Hum door ko bolte hain close hone, logic woh khud dekhega.
    void close() {
        if (isOpen) {
            isOpen = false;
        }
    }
};
```

### Topic 15: Law of Demeter (LoD)
"Don't talk to strangers." Avoid deep method chaining like: `driver.getCar().getEngine().start()`.

**Code Example:**
```cpp
class Engine {
public: void start() {}
};

class Car {
private: Engine engine;
public: 
    // Good: Car handles its own engine
    // Good: Car apna engine khud handle karti hai
    void startCar() { engine.start(); } 
};

class Driver {
public:
    void drive(Car& car) {
        // Good: Driver only talks to Car, not Engine
        // Good: Driver sirf Car se baat karta hai, Engine se nahi
        car.startCar(); 
    }
};
```

### 🎯 Practice Coding Challenges (Section 3)
**Challenge 1: Law of Demeter (Don't Talk to Strangers)**
- **Goal:** Prevent deep method chaining.
- **Task:** 
  - You have code doing: `driver.getCar().getEngine().start()`.
  - Refactor the classes so the `Driver` just calls `driver.startCar()`.

**Challenge 2: Programming to Interfaces**
- **Goal:** Depend on abstractions, not concretions.
- **Task:** 
  - Create a function `void exportData(IExporter& exporter)`.
  - Pass an `XmlExporter` into the exact same function to prove it works dynamically.

---

## Section 4: Anti-Patterns

### Topic 21 & 22: Manager Classes & God Objects
A "God Object" is a class that knows everything and does everything. You must refactor these by breaking them down into smaller, highly cohesive classes.

**Code Example:**
```cpp
// BAD: God Object
class SystemManager {
    void handlePhysics() {}
    void handleAudio() {}
    void handleNetwork() {}
};

// GOOD: Broken down into smaller classes
class AudioSystem { void playSound() {} };
class NetworkSystem { void sendPacket() {} };
```

### Topic 23: Avoiding Anemic Domain Models
An anemic model happens when your classes are just bags of data (only getters and setters) with zero business logic. In true OOP, data and behavior should sit together.

**Code Example:**
```cpp
#include <iostream>
#include <string>

// RICH MODEL (Good OOP)
class Account {
private:
    double balance;
public:
    Account(double b) : balance(b) {}

    // Behavior is inside the class!
    // Logic class ke andar hi hai!
    void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
        }
    }
};
```

### 🎯 Practice Coding Challenges (Section 4)
**Challenge 1: Refactor a God Object**
- **Goal:** Break down a massive monolithic class.
- **Task:** 
  - Take a massive `GameManager` class.
  - Break it down into smaller classes: `AudioSystem`, `PhysicsEngine`, and `UIManager`.

---

## Section 5: Advanced Lifecycle, Ownership & DI

### Topic 12 & 13: Separation of Concerns & Composition Over Inheritance
Isolating different parts of your application and favoring Composition (combining small parts) over rigid Inheritance trees.

### Topic 16: Immutability
Once an object is created, its state cannot be changed (no setter methods). This makes the object incredibly safe to use in multi-threaded environments.

**Code Example:**
```cpp
class RGBColor {
public:
    const int r, g, b;
    // Immutable: Values are set once and can never be changed
    // Immutable: Ek baar set ho gaya toh change nahi hoga
    RGBColor(int red, int green, int blue) : r(red), g(green), b(blue) {}
};
```

### Object Ownership Models
- `std::unique_ptr`: Strict single ownership. Memory frees automatically.
- `std::shared_ptr`: Shared ownership (reference counted). Memory frees when count hits 0.
- `std::weak_ptr`: Observes a `shared_ptr` without increasing the count (solves cyclic references).

**Code Example:**
```cpp
#include <memory>

class Node {
public:
    // weak_ptr prevents cyclic memory leaks!
    // weak_ptr cyclic memory leak ko rokta hai!
    std::weak_ptr<Node> parent; 
    std::shared_ptr<Node> child;
};
```

### Dependency Injection (DI) & Pluggable Architecture
Passing dependencies into a class via its constructor, rather than having the class hard-code their creation.

**Code Example:**
```cpp
#include <iostream>
#include <memory>

class ILogger {
public: virtual void log() = 0; 
};

class FileLogger : public ILogger {
public: void log() override { std::cout << "Logging to File\n"; }
};

class Application {
private:
    std::unique_ptr<ILogger> logger; 
public:
    // Constructor Injection
    // Hum bahar se dependency de rahe hain!
    Application(std::unique_ptr<ILogger> l) : logger(std::move(l)) {}
    void run() { logger->log(); }
};
```

### 🎯 Practice Coding Challenges (Section 5)
**Challenge 1: Immutability**
- **Goal:** Create a read-only object that is thread-safe.
- **Task:** 
  - Create an `RGBColor` class where `r`, `g`, `b` are `const`. 
  - Provide a method `mix()` that returns a completely *new* `RGBColor` object instead of modifying the existing one.

**Challenge 2: Weak Pointers (Breaking Cycles)**
- **Goal:** Prevent memory leaks in shared ownership.
- **Task:** 
  - Create a cyclic reference using two classes `NodeA` and `NodeB` that hold a `std::shared_ptr` to each other.
  - Change one of the pointers to `std::weak_ptr` and prove the destructors now run correctly.
