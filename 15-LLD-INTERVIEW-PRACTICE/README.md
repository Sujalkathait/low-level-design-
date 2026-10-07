# Unit 1: Clean Coding, Object Oriented Principles & Machine Coding

Welcome to the foundation of Low-Level Design (LLD). This module focuses on writing clean, scalable, and modular code by deeply understanding Object-Oriented Principles, SOLID principles, and various Design Patterns. The ultimate goal is to prepare for machine coding rounds by solving real-world LLD case studies.

---

## 🧠 Clean Coding Mindset
- **Readable, Modular and Maintainable Code:** Writing code that is easy for humans to read and understand.
- **Naming Conventions:** Using descriptive, unambiguous, and consistent names for variables, classes, and methods.
- **Avoiding Code Smells:** Identifying and refactoring bad practices (e.g., duplicated code, long methods, God classes).
- **Scalable Code Structure:** Designing directory layouts and code modules that grow seamlessly as project requirements expand.

## 🏗️ Object-Oriented Thinking
- **Encapsulation:** Bundling the data and the methods that operate on the data into a single unit (class), restricting direct access to some of the object's components.
- **Abstraction:** Hiding complex implementation details behind simple interfaces.
- **Inheritance vs Composition:** 
  - *Inheritance (IS-A):* Acquiring properties and behaviors from a parent class.
  - *Composition (HAS-A):* Building complex objects by combining simpler ones (strongly preferred over deep inheritance trees).
- **Polymorphism:** Allowing objects of different types to be treated as objects of a common base type, typically through virtual functions.

## 📊 UML & ER Diagrams
- **Class Diagrams:** Visualizing class structure, attributes, methods, and relationships (Association, Aggregation, Composition, Inheritance).
- **Sequence Diagrams:** Modeling the interaction and flow of messages between objects in a sequential order over time.
- **ER Diagrams (Entity-Relationship):** Modeling database schemas, defining entities, their attributes, and how they relate to one another.

## 🚀 SOLID Principles
Understanding bad vs refactored designs through the lens of SOLID:
- **S - Single Responsibility Principle (SRP):** A class should have one, and only one, reason to change.
- **O - Open/Closed Principle (OCP):** Software entities should be open for extension but closed for modification.
- **L - Liskov Substitution Principle (LSP):** Objects of a superclass should be replaceable with objects of its subclasses without breaking the application.
- **I - Interface Segregation Principle (ISP):** Clients should not be forced to depend on interfaces they do not use (prefer small, focused interfaces).
- **D - Dependency Inversion Principle (DIP):** High-level modules should not depend on low-level modules; both should depend on abstractions.

## 🎨 Design Patterns
Design patterns are typical solutions to common problems in software design.

### Creational Patterns
- **Singleton:** Ensures a class has only one instance and provides a global point of access to it.
- **Factory Method:** Defines an interface for creating an object, but lets subclasses decide which class to instantiate.
- **Abstract Factory:** Provides an interface for creating families of related or dependent objects.
- **Builder:** Separates the construction of a complex object from its representation, allowing the same construction process to create various representations.

### Structural Patterns
- **Adapter:** Allows classes with incompatible interfaces to work together.
- **Decorator:** Attaches additional responsibilities to an object dynamically, providing a flexible alternative to subclassing.
- **Proxy:** Provides a surrogate or placeholder for another object to control access to it.
- **Bridge:** Decouples an abstraction from its implementation so that the two can vary independently.

### Behavioral Patterns
- **Strategy:** Defines a family of algorithms, encapsulates each one, and makes them interchangeable at runtime.
- **Observer:** Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified automatically.
- **Command:** Encapsulates a request as an object, thereby allowing parameterization of clients with different requests, queueing, and logging.

---

## 💻 Machine Coding & Low Level Design Case Studies (2025-26 Onwards)

Machine coding rounds involve requirement analysis, class design, establishing relationships, and modular code implementation within a limited timeframe. 

As part of group activities and self-learning (approx. 6 hours), we will analyze poorly designed code, refactor it using clean coding practices, and implement the following LLD systems from scratch:

1. **[Tic Tac Toe / Chess](./01-Tic-Tac-Toe-Chess)**
2. **[LRU Cache](./02-LRU-Cache)**
3. **[Parking Lot](./03-Parking-Lot)**
4. **[ATM System](./04-ATM-System)**
5. **[Elevator System](./05-Elevator-System)**
6. **[Movie Ticket Booking](./06-Movie-Ticket-Booking)**

*Students shall implement selected design patterns, prepare UML diagrams, and practice object-oriented modeling for these real-world software systems.*
