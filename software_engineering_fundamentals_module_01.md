# Software Engineering Fundamentals

**Senior Software Engineer Interview Preparation · Module 01**

Our objective is not simply to memorize OOP definitions, SOLID principles, or programming acronyms. The objective is to develop the engineering judgment expected of a Senior Software Engineer: understanding why a design works, recognizing when it will fail, choosing appropriate alternatives, and explaining those decisions clearly.

Your C#/.NET background gives us a practical foundation. We will use C# for implementation examples, but the concepts will be language-independent.

# Part 1. Complete Curriculum

The module is divided into 10 sections, each containing focused lessons. We will progress sequentially, with exercises and interview questions throughout.

## 1. Object-Oriented Programming (OOP)

- Classes and objects
- State, behavior and identity
- Encapsulation
- Abstraction
- Inheritance
- Polymorphism
- Composition
- Interfaces
- Object lifecycle
- Value versus reference semantics
- Immutability
- Equality

## 2. SOLID Principles

- Single Responsibility Principle (SRP)
- Open/Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
- Interface Segregation Principle (ISP)
- Dependency Inversion Principle (DIP)
- Practical violations and refactoring
- Dependency injection
- Design trade-offs and advanced applications

## 3. Clean Code and Readability

- Naming
- Functions and methods
- Abstraction levels
- Side effects
- Control flow
- Error handling
- Exceptions
- Null handling
- Comments
- Code organization
- Testability
- Code readability at scale

## 4. Core Software Design Principles

- DRY (Don't Repeat Yourself)
- KISS (Keep It Simple, Stupid)
- YAGNI (You Aren't Gonna Need It)
- Separation of concerns
- Single source of truth
- Principle of least knowledge (Law of Demeter)
- Fail-fast
- Information hiding
- Principle of least astonishment
- Defensive programming
- Rule of Three

## 5. Coupling

- Tight versus loose coupling
- Compile-time coupling
- Runtime coupling
- Data coupling
- Control coupling
- Temporal coupling
- Dependency graphs
- Coupling across services
- Change propagation
- Dependency direction
- Techniques for reducing unnecessary dependencies

## 6. Cohesion

- Functional cohesion
- Sequential cohesion
- Communicational cohesion
- Procedural cohesion
- Temporal cohesion
- Coincidental cohesion
- High cohesion
- Class and module boundaries
- Feature-oriented organization
- Identifying misplaced responsibilities

## 7. Abstraction and Encapsulation in Depth

- Levels of abstraction
- Contracts
- Interfaces
- Implementation hiding
- Abstraction leakage
- Leaky abstractions
- Appropriate abstraction boundaries
- Over-abstraction
- Under-abstraction
- Domain-oriented abstractions

## 8. Maintainability and Evolution

- Technical debt
- Code smells
- Refactoring
- Backwards compatibility
- Extensibility
- Complexity
- Changeability
- Maintainability
- Design for change without overengineering

## 9. Applying Fundamentals to Enterprise .NET

- Dependency injection
- ASP.NET Core
- Entity Framework Core
- Repositories
- Domain models
- Services
- Middleware
- Event-driven systems
- Messaging
- Distributed transactions
- Microservices
- Configuration and infrastructure boundaries

## 10. Senior-Level Design Reviews and Interview Scenarios

- Reviewing flawed code
- Comparing alternative designs
- Identifying principle violations
- Defending architectural decisions
- Balancing simplicity and extensibility
- Refactoring legacy systems
- Practical design exercises
- Comprehensive assessment

---

# Part 2. How Each Lesson Will Work

Every lesson will follow the same teaching structure.

| Stage | What we'll do |
|---|---|
| 1. Fundamentals | Define concepts and terminology precisely. |
| 2. Deep understanding | Explain mechanisms and how concepts work internally. |
| 3. Implementation | Study practical C#/.NET code. |
| 4. Enterprise application | Examine realistic production scenarios. |
| 5. Engineering judgment | Discuss trade-offs, alternatives and mistakes. |
| 6. Senior expectations | Identify what interviewers expect from a senior candidate. |
| 7. Interview preparation | Practice questions with strong example answers. |
| 8. Knowledge assessment | Solve exercises and answer follow-up questions. |

We will use three levels when evaluating answers:

- **Mid-level:** Understands the principle and can apply it in familiar situations.
- **Senior-level:** Understands the context, trade-offs, failure modes and implications for maintainability.
- **Strong senior / Staff-level thinking:** Can evaluate system-wide consequences, challenge assumptions, recognize organizational constraints and explain why one approach is better in a particular context.

A topic will not be marked as mastered just because it has been discussed. Answers and practical exercises will determine that.

---

# Section 1. Object-Oriented Programming (OOP)

## Lesson 1.1 — The Object Model

**Level:** Fundamental

## 1. What Is Object-Oriented Programming?

Object-Oriented Programming is a programming paradigm that organizes software around objects.

An object combines:

1. **State** — the information it maintains.
2. **Behavior** — the operations it can perform.
3. **Identity** — what makes it distinguishable from another object.

The central idea is that related data and behavior can be grouped into meaningful units that interact with other units.

Consider an enterprise banking application. You might have:

- `BankAccount`
- `Customer`
- `Transaction`
- `BankTransfer`
- `Payment`

Each represents a concept within the business domain.

For example, a bank account has a balance, an account number and operations such as depositing and withdrawing money.

The important distinction is that an object is not merely a container for data. It can also be responsible for maintaining valid state.

### 1.1 Classes versus objects

These two terms are related but not interchangeable.

- **Class:** A definition describing the structure and behavior of objects.
- **Object:** A runtime instance of a class.

Consider this C# example:

```csharp
public class BankAccount
{
    public string AccountNumber { get; set; }

    public decimal Balance { get; private set; }

    public void Deposit(decimal amount)
    {
        Balance += amount;
    }
}
```

`BankAccount` is a class.

Creating an instance:

```csharp
var account = new BankAccount
{
    AccountNumber = "MK123456"
};

account.Deposit(1000m);
```

Now `account` refers to an object.

Creating another instance:

```csharp
var account1 = new BankAccount
{
    AccountNumber = "MK111111"
};

var account2 = new BankAccount
{
    AccountNumber = "MK222222"
};

account1.Deposit(1000m);
account2.Deposit(500m);
```

Both objects share the same class definition but maintain independent state.

**Why this matters professionally**

A class defines what operations are available. Each instance maintains its own state.

This distinction becomes important when designing:

- Request-scoped services in ASP.NET Core.
- Domain entities in enterprise applications.
- Background processing components.
- Stateful workflows.
- Concurrent applications where multiple operations interact with objects.

A common mistake is to confuse a class with a singleton or assume that all instances of a class share state. They do not, unless that state is explicitly shared, for example through static members or shared referenced objects.

## 2. State, Behavior and Object Identity

These are three essential characteristics of object-oriented design.

### 2.1 State

State represents the data an object maintains at a particular point in time.

For example:

```csharp
public class Order
{
    public Guid Id { get; init; }

    public string CustomerId { get; init; }

    public string Status { get; private set; }

    public decimal TotalAmount { get; private set; }
}
```

An order might have:

- An identifier.
- A customer.
- A status.
- A total amount.

When these values change, the state of the object changes.

For example:

```text
Order A
  Status: Pending
  Total: 100 EUR

After confirmation:

Order A
  Status: Confirmed
  Total: 100 EUR
```

The object is still the same conceptual order, but its state has changed.

### 2.2 Behavior

Behavior defines what an object can do.

In C#, behavior is commonly implemented through methods.

```csharp
public class Order
{
    public string Status { get; private set; } = "Pending";

    public void Confirm()
    {
        if (Status != "Pending")
        {
            throw new InvalidOperationException(
                "Only pending orders can be confirmed.");
        }

        Status = "Confirmed";
    }
}
```

Notice something important: the object does not expose a public setter for `Status`.

Instead, the object controls the operation that changes its state.

This is the beginning of encapsulation, which we will study in detail in Lesson 1.3.

Why is this better than allowing any part of the application to modify the status directly?

Because the object can protect business rules.

For example, an order should not be confirmed twice, and a cancelled order should not suddenly become confirmed through an arbitrary property assignment.

### 2.3 Identity

Object identity answers:

**Is this the same object instance, or merely another object containing equivalent data?**

Consider:

```csharp
var account1 = new BankAccount
{
    AccountNumber = "MK123",
};

var account2 = new BankAccount
{
    AccountNumber = "MK123",
};
```

Both objects contain the same account number, but they are two different object instances.

```csharp
Console.WriteLine(account1 == account2);
```

For ordinary classes that have not overloaded `==`, this returns `false` because they are different references.

We can explicitly check identity:

```csharp
Console.WriteLine(
    ReferenceEquals(account1, account2));
```

This also returns `false`.

However, business equality can be different from reference identity.

Imagine that these objects were loaded from two different database queries:

```csharp
var order1 = LoadOrder(orderId);
var order2 = LoadOrder(orderId);
```

They might represent the same business order, with the same database ID, but be two separate objects in memory.

A business application may consider them equivalent because their identifiers match.

This introduces an important distinction:

| Concept | Meaning |
|---|---|
| Reference identity | Are these the same instance? |
| Value equality | Do these objects contain equivalent values? |
| Domain identity | Do these represent the same business entity? |

This distinction is particularly important in domain modeling, caching, Entity Framework Core tracking, distributed applications and serialization.

## 3. How C# Implements Objects Internally

A Senior Software Engineer should understand more than the syntax of classes and objects.

Let's examine the CLR perspective.

### 3.1 Reference types

In C#, classes are reference types.

```csharp
var account1 = new BankAccount();
var account2 = account1;
```

What happens?

`account1` refers to an object. When assigning `account1` to `account2`, C# copies the reference, not the object itself.

Conceptually:

```text
account1 ──┐
           ├──> One BankAccount object
account2 ──┘
```

Consequently:

```csharp
account1.Deposit(100);

Console.WriteLine(account2.Balance);
```

The second reference observes the updated balance because both variables refer to the same object.

This behavior is important when passing objects between methods.

For example:

```csharp
public void ProcessAccount(BankAccount account)
{
    account.Deposit(100);
}
```

Calling this method modifies the referenced object.

One subtlety: C# passes arguments by value by default. For a reference type, the value being copied is the reference itself. The method receives its own copy of that reference, which still points to the same object.

This is different from passing an argument with `ref` or `out`.

### 3.2 Value types

C# also has value types:

- `int`
- `decimal`
- `bool`
- `DateTime`
- `Guid`
- `struct`
- `enum`

Example:

```csharp
int a = 10;
int b = a;

b = 20;

Console.WriteLine(a); // 10
Console.WriteLine(b); // 20
```

Here, the value is copied. Unlike the previous reference assignment, changing `b` does not change `a`.

A `struct` behaves similarly in terms of value semantics.

However, be careful with an important distinction:

**Value type does not mean it is always stored on the stack. Reference type does not mean its variable is always stored on the heap.**

Storage depends on context and implementation.

For example:

- A local value-type variable might be stored in a register or on the stack.
- A value-type field inside a class is stored as part of that object's storage.
- A reference-type instance is generally allocated on the managed heap.
- A local variable holding a reference can reside in a register or on the stack.

The CLR and JIT compiler manage these implementation details.

### 3.3 Garbage collection and object lifetime

When we create objects:

```csharp
var order = new Order();
```

The CLR manages memory for the managed object.

The garbage collector determines whether an object is still reachable from roots such as:

- Active stack references.
- Static references.
- CPU/register-tracked references.
- Other GC-tracked references.

Objects that are no longer reachable can eventually be collected.

This does not mean that garbage collection happens immediately when a variable goes out of scope.

The CLR decides when collection occurs.

Senior engineers should understand that:

- The garbage collector manages memory, not every external resource.
- Database connections, file handles and network resources need appropriate disposal.
- `IDisposable` and `using` provide deterministic resource cleanup.
- Memory leaks can still occur in managed applications through unintended references, event subscriptions, caches or static collections.

Example:

```csharp
using var stream = File.OpenRead("data.json");

// Read file...

// Dispose is called when execution leaves the scope.
```

Do not confuse object lifetime with resource lifetime. We will revisit this when discussing object lifecycle and immutability.

## 4. Classes, Structs and Records: Choosing the Right Model

In real C# applications, you have several ways to represent concepts.

The distinction matters because they have different semantics.

| Feature | `class` | `struct` | `record class` |
|---|---|---|---|
| Type category | Reference | Value | Reference |
| Default equality | Reference identity | Value-based | Value-based |
| Inheritance | Class inheritance | No class inheritance | Class inheritance |
| Typical usage | Entities, services | Small values | Data-centric models with value equality |
| Mutable by default | Yes | Yes | Yes |

### Example: class entity

```csharp
public class Customer
{
    public Guid Id { get; init; }

    public string Name { get; set; }
}
```

A customer is generally an entity with identity. Two customers with the same name are not necessarily the same customer.

### Example: record value object

```csharp
public record Money(
    decimal Amount,
    string Currency);
```

Now:

```csharp
var price1 = new Money(100, "EUR");
var price2 = new Money(100, "EUR");

Console.WriteLine(price1 == price2); // True
```

The generated record equality compares the relevant component values.

This is useful for values such as:

- Money.
- Coordinates.
- Date ranges.
- Addresses, where appropriate.
- Measurement values.
- Configuration values.

### Example: struct

```csharp
public readonly struct Point
{
    public double X { get; }
    public double Y { get; }

    public Point(double x, double y)
    {
        X = x;
        Y = y;
    }
}
```

A small, immutable value is a reasonable candidate for a struct.

However, using structs indiscriminately can introduce unnecessary copying, larger value sizes and boxing.

Do not choose structs purely because you heard they are faster.

**Senior engineering consideration:** Choose a type based primarily on its intended semantics, ownership and lifecycle, then consider performance and measurement.

## 5. Real-World Enterprise Example: Order Processing

Let's connect the concepts to an actual enterprise application.

Imagine an order processing platform with these components:

- ASP.NET Core API.
- Order management domain.
- Entity Framework Core.
- Azure Service Bus.
- Background payment processing.

A customer submits an order.

The system creates an `Order` object. That object contains state such as its customer, order lines and status.

The order has behavior:

- Add a line.
- Remove a line.
- Calculate its total.
- Confirm the order.
- Cancel the order.

The payment service does not need to manipulate every internal property of the order. It should interact with clearly defined operations or application-level workflows.

The order object's responsibility is to maintain its own valid state within the boundaries of its design.

For example:

```csharp
public class Order
{
    private readonly List<OrderLine> _lines = [];

    public Guid Id { get; private set; }

    public string Status { get; private set; } = "Draft";

    public IReadOnlyCollection<OrderLine> Lines =>
        _lines.AsReadOnly();

    public void AddLine(OrderLine line)
    {
        if (Status != "Draft")
        {
            throw new InvalidOperationException(
                "Cannot modify a non-draft order.");
        }

        ArgumentNullException.ThrowIfNull(line);

        _lines.Add(line);
    }

    public void Confirm()
    {
        if (Status != "Draft")
        {
            throw new InvalidOperationException(
                "Only draft orders can be confirmed.");
        }

        if (_lines.Count == 0)
        {
            throw new InvalidOperationException(
                "Cannot confirm an empty order.");
        }

        Status = "Confirmed";
    }
}

public record OrderLine(
    string ProductId,
    int Quantity,
    decimal UnitPrice);
```

This example demonstrates:

- An object maintaining state.
- Methods implementing behavior.
- Controlled state transitions.
- A collection of related objects.
- A distinction between the identity of an order and the values represented by an order line.

We will examine the design more critically when we study encapsulation, SOLID, cohesion and domain modeling.

An important production consideration: this object alone does not make order processing reliable. Persistence, concurrency, transaction boundaries, idempotency and messaging consistency still need to be addressed.

OOP helps organize the local model; it does not solve distributed systems problems automatically.

## 6. Common Mistakes and Trade-offs

A senior engineer should be able to recognize these problems.

| Mistake | Why it is problematic |
|---|---|
| Treating objects as data containers only | Business rules become scattered across services and handlers. |
| Making every property publicly mutable | Invalid state becomes easy to introduce. |
| Using inheritance for every form of reuse | Creates rigid hierarchies and unnecessary dependencies. |
| Treating all objects as reference-based entities | Value objects and immutable data often have different semantics. |
| Assuming one class equals one object | Causes confusion about state, identity and lifetimes. |
| Assuming GC immediately frees unused objects | Leads to incorrect memory and resource management assumptions. |
| Choosing structs automatically for performance | Can cause copying and boxing costs without measurable benefit. |
| Overusing OOP abstractions | Creates complexity without improving the design. |

A particularly important point:

**OOP is a tool for managing complexity, not a rule that everything must become a class.**

Functional programming, procedural code and data-oriented approaches can be better in certain contexts.

A good senior engineer knows how to combine paradigms rather than force every problem into one model.

## 7. Senior-Level Interview Preparation

Here are five questions you should be able to answer confidently after this lesson.

### Question 1: What is the difference between a class and an object?

**Strong example answer:**

A class defines the structure and behavior of a particular type, while an object is a runtime instance of that type. Multiple objects can be created from one class, each maintaining independent state. In object-oriented design, objects combine state and behavior and can have their own identity.

### Question 2: What is the difference between reference types and value types in C#?

**Strong example answer:**

Value types have value semantics, meaning assignment normally copies their value. Reference types have reference semantics, meaning assignment copies a reference to an object rather than duplicating the object itself.

In C#, classes are reference types, while structs and primitive numeric types are value types. Their actual storage location depends on the execution context and CLR implementation, so the common rule that reference types are on the heap and value types are on the stack is an oversimplification.

### Question 3: What is the difference between object identity and equality?

**Strong example answer:**

Object identity determines whether two references point to the same instance. Equality determines whether two objects should be considered equivalent based on their values or domain rules.

For example, two instances of a customer entity might have the same database identifier and therefore represent the same domain entity even though they are different instances in memory. In C#, reference equality and value equality can be implemented or checked separately.

### Question 4: Why should an object contain behavior instead of simply exposing data?

**Strong example answer:**

Combining relevant state and behavior helps keep business rules close to the data they protect. Rather than allowing different parts of an application to modify an object's state arbitrarily, the object can expose operations that enforce valid state transitions.

This improves consistency and reduces the likelihood of invalid states. However, I would not force every operation into an entity; orchestration and cross-aggregate workflows often belong in application services.

### Question 5: Is OOP always the best approach for enterprise applications?

**Strong example answer:**

No. OOP is useful for modeling entities, responsibilities and stateful behavior, especially where domain rules and lifecycle management are important. But other paradigms can be more appropriate for transformations, calculations, data processing and parallel workloads.

I would choose the approach based on the problem, desired boundaries, complexity and maintainability rather than applying OOP everywhere.

## 8. Practical Exercises

Do not look for solutions yet. These are designed to test whether you understand the underlying concepts rather than simply recognize terminology.

### Exercise A — C# Reference Semantics

Consider:

```csharp
public class Customer
{
    public string Name { get; set; }
}

var customer1 = new Customer
{
    Name = "John"
};

var customer2 = customer1;

customer2.Name = "Peter";

Console.WriteLine(customer1.Name);
Console.WriteLine(customer2.Name);
```

**Questions:**

1. What will the two `Console.WriteLine` statements output?
2. Why?
3. Does `customer2 = customer1` create another object?
4. How could you create an independent copy?
5. Would the answer change if `Customer` were a struct?

### Exercise B — Entity versus Value

You're building an e-commerce platform.

Classify the following concepts as likely entities or value objects, and explain your reasoning:

| Concept | Your classification |
|---|---|
| Customer | ? |
| Order | ? |
| Money | ? |
| OrderLine | ? |
| Product | ? |
| EmailAddress | ? |
| Address | ? |
| Payment | ? |

There can be context-dependent answers. The goal is to explain the reasoning, not merely provide a label.

### Exercise C — Code Review

A developer submits the following implementation:

```csharp
public class Order
{
    public Guid Id { get; set; }

    public string Status { get; set; }

    public decimal Total { get; set; }
}
```

And elsewhere:

```csharp
public class OrderService
{
    public void ConfirmOrder(Order order)
    {
        order.Status = "Confirmed";
    }

    public void CancelOrder(Order order)
    {
        order.Status = "Cancelled";
    }
}
```

You are reviewing this as a Senior Software Engineer.

Identify:

1. What design problems do you see?
2. What invalid states or transitions are possible?
3. What would you change?
4. Would you move all business logic into the `Order` class? Why or why not?

Don't just say "encapsulation violation." Explain the actual consequences for the enterprise application.

## 9. Knowledge Check — Interview Simulation

Imagine the interviewer asks:

> You have two separate instances of a `Customer` class. Both contain exactly the same values for `Id` and `Name`.
>
> One instance was retrieved from Entity Framework Core, while the other was reconstructed from a message received through Azure Service Bus.
>
> Should these objects be considered equal? What determines that? Would you implement equality on the class? Explain your reasoning.

This question deliberately connects several concepts:

- Reference identity.
- Value equality.
- Domain identity.
- ORM behavior.
- Distributed messaging.
- Serialization and reconstruction.
- Software design boundaries.

A mid-level answer might focus on overriding `Equals()`.

A strong senior answer should consider what equality means in the business domain, whether the type is an entity or a value object, how identity is represented, and what the consequences are for collections, tracking and message processing.

## 10. Learning Tracker

### Module 01 — Software Engineering Fundamentals

### Section 1 — OOP

| Topic | Status |
|---|---|
| Classes and objects; state, behavior and identity | Learning |
| Encapsulation and invariants | Not started |
| Abstraction and information hiding | Not started |
| Inheritance and polymorphism | Not started |
| Composition versus inheritance | Not started |
| Interfaces and abstract classes | Not started |
| Object lifecycle and immutability | Not started |
| Equality, value objects and reference semantics | Not started |

**Remaining sections:** SOLID, Clean Code, Core Design Principles, Coupling, Cohesion, Abstraction in Depth, Maintainability, Enterprise .NET Applications, and Senior-Level Design Reviews.

---

# Your First Assignment

Answer Exercises A, B and C, followed by the interview simulation question.

The answers will be evaluated for technical correctness, clarity, practical reasoning and senior-level judgment. Inaccurate assumptions will be corrected, and follow-up questions will be used to explore areas that need deeper examination.

We will not move to OOP Lesson 1.2 until the foundations are solid.

At the end of each lesson, we can also build a short interview revision sheet containing the essential concepts and questions.
