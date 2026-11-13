# Module 01 — Software Engineering Fundamentals

**Senior Software Engineer Academy · Module 01 of 12**

> **Learning objective:** Develop the engineering judgment expected of a Senior Software Engineer across the core foundations of software design: object-oriented mechanics, SOLID principles, clean code, design heuristics, coupling, cohesion, abstraction boundaries, maintainability, enterprise .NET architecture, and senior-level design reviews. The objective is not simply to recite definitions or acronyms, but to understand why designs succeed or fail, evaluate architectural trade-offs, and defend technical decisions under interview scrutiny.
>
> **Audience:** Experienced C#/.NET engineers preparing for Senior and Staff Software Engineer interviews. Professional experience is assumed, but fundamentals are taught with exact technical precision before advancing to architectural implications and production failure modes.
>
> **Version note:** Code examples target modern .NET (.NET 8 LTS and .NET 9) with C# 12/13. Modern language features such as collection expressions (`[]`), primary constructors, `init`-only properties, records, `required` members, and pattern matching are used where idiomatic.

## How to use this module

Every section in Part II provides comprehensive senior-level instruction:
1. **Fundamentals & Internal Mechanics:** Precise definitions, memory layout, compiler rewrites, and design forces.
2. **C#/.NET Implementation:** Production-grade code examples with strict invariant protection and clean idioms.
3. **Enterprise Application:** Realistic scenarios in order processing, billing, payments, multi-tenant SaaS, and background workers.
4. **Trade-offs, Alternatives & Failure Modes:** When a principle or pattern breaks down and when to deliberately relax it.
5. **What a Senior Engineer Is Expected to Know:** The contrast between a mid-level and a senior/staff answer.
6. **Interview Questions with Model Answers:** Real interview questions with structured, senior-level responses.
7. **Practical Exercises:** Deep problems without inline solutions, designed to test architectural judgment.

## Module boundaries

- **This module owns:** OOP mechanics, SOLID, clean code, DRY/KISS/YAGNI, coupling, cohesion, abstraction boundaries, maintainability heuristics, enterprise .NET fundamental patterns, and code review methodology.
- **Related topics owned by other modules:**
  - Concrete Gang of Four design patterns, MediatR, CQRS, and Clean Architecture → Module 04
  - CLR execution pipeline, JIT/AOT, GC internals, and memory allocation details → Module 03
  - Data structure selection, algorithmic complexity, and .NET collection internals → Module 02
  - Database persistence, EF Core internals, transaction isolation, and query tuning → Module 05
  - Distributed transactions, Sagas, Outbox pattern, and messaging semantics → Module 07
  - System-level scalability, Domain-Driven Design (strategic contexts), and microservices → Module 08

---

# Part I — Complete Curriculum

## Section 1 — Object-Oriented Programming (OOP) Deep Dive
**Outcome:** Master the internal mechanics of object identity, state management, polymorphism, value vs reference semantics, and immutability in modern .NET.
- 1.1 The Object Model: State, behavior, and identity; classes vs objects; entity identity vs reference identity vs value equality.
- 1.2 Value Types, Reference Types, and Memory Semantics: Structs, classes, record classes, record structs; layout, allocation context, boxing/unboxing, and defensive copying.
- 1.3 Encapsulation and Invariant Enforcement: Information hiding vs data hiding; protecting business invariants; eliminating anemic domain models.
- 1.4 Inheritance, Polymorphism, and Dispatch: Vtables, method tables, virtual dispatch, interface dispatch, shadowing (`new`) vs overriding, sealed classes.
- 1.5 Composition over Inheritance: Fragile base class problem; delegation; composition patterns in enterprise C#.
- 1.6 Interfaces vs Abstract Classes: Contract design, default interface methods, versioning, testability.
- 1.7 Object Lifecycle and Immutability: Construction invariants, `init`, `readonly`, shallow vs deep immutability, deterministic cleanup vs GC lifetime (`IDisposable`).
- 1.8 Equality and Hashing: `IEquatable<T>`, `GetHashCode` contracts, `IEqualityComparer<T>`, reference equality vs structural equality.
**Senior-level bar:** Explain the runtime dispatch mechanism of interfaces vs virtual methods, design types with immutable invariants, and articulate why inheritance fails in evolving enterprise domains.

---

## Section 2 — SOLID Principles in Practice
**Outcome:** Evaluate, apply, and critique SOLID principles without dogmatic over-engineering.
- 2.1 Single Responsibility Principle (SRP): Reason to change vs doing one thing; cohesion at class and package levels; God classes and shotgun surgery.
- 2.2 Open/Closed Principle (OCP): Extension mechanisms (polymorphism, strategy, delegates, decorators); predicting variation points vs speculative generality.
- 2.3 Liskov Substitution Principle (LSP): Behavioral subtyping, preconditions and postconditions, invariant preservation, return covariance and parameter contravariance.
- 2.4 Interface Segregation Principle (ISP): Role interfaces vs header interfaces; fat interfaces; client-driven contract design; ISP in .NET APIs.
- 2.5 Dependency Inversion Principle (DIP): Inversion of control vs dependency injection; high-level policy independent of low-level detail; composition roots.
- 2.6 SOLID Anti-Patterns and Over-Engineering: Interface soup, dependency injection abuse, premature abstraction, analysis paralysis.
**Senior-level bar:** Identify subtle LSP violations in inheritance hierarchies, refute the claim that SRP means "one method per class", and explain the exact architectural boundary where DIP is applied.

---

## Section 3 — Clean Code, Readability & Expressiveness at Scale
**Outcome:** Write self-documenting, maintainable code that minimizes cognitive load across large engineering teams.
- 3.1 Cognitive Load and Readability: Extraneous vs intrinsic cognitive load; readability as a safety property.
- 3.2 Naming as Architecture: Intention-revealing names, domain terminology (Ubiquitous Language), avoiding disinformation and mental mapping.
- 3.3 Method and Function Design: Single level of abstraction principle (SLAP); command-query separation (CQS); pure functions; parameter count and object arguments.
- 3.4 Control Flow and Nesting: Guard clauses, early returns, railway-oriented programming, avoiding deeply nested loops and conditionals.
- 3.5 Error Handling Philosophy: Exceptions for exceptional conditions vs result patterns (`Result<T>`, `OneOf`); exception hierarchies; catching what you can handle.
- 3.6 Nullability and Defensive Design: Nullable reference types (NRT), null-object pattern, explicit optionality (`Option<T>`), avoiding defensive null-checks everywhere.
- 3.7 Comments and Documentation: Self-documenting code vs explanatory comments; architectural documentation; obsolete comment rot.
**Senior-level bar:** Refactor nested, exception-heavy business logic into expressive, railway-oriented or guard-clause C# that enforces SLAP and CQS.

---

## Section 4 — Core Software Design Principles & Heuristics
**Outcome:** Balance conflicting design heuristics to achieve pragmatic, robust software architectures.
- 4.1 DRY (Don't Repeat Yourself): Duplication of knowledge vs accidental duplication of code; over-DRYing and premature coupling.
- 4.2 KISS (Keep It Simple, Stupid) & YAGNI (You Aren't Gonna Need It): Essential complexity vs accidental complexity; cost of speculative features; evolutionary design.
- 4.3 Separation of Concerns (SoC) & Single Source of Truth (SSOT): Data normalization vs denormalization; separating orchestration from business rules.
- 4.4 Law of Demeter (Principle of Least Knowledge): Dot-navigation chains (`a.B.C.DoSomething()`); train wrecks; wrapper methods vs moving behavior.
- 4.5 Fail-Fast & Defensive Programming: Validating inputs at boundaries; failing immediately upon illegal state vs masking errors; assertions.
- 4.6 Principle of Least Astonishment (POLA): Predictable APIs, side-effect-free getters, consistent naming conventions.
- 4.7 Rule of Three: Heuristic for abstraction; duplicate once, refactor on the third occurrence.
**Senior-level bar:** Articulate precisely when DRY leads to disastrous coupling between microservices or business domains, and defend YAGNI against speculative architectural abstractions.

---

## Section 5 — Coupling: Mechanics, Metrics & Minimization
**Outcome:** Diagnose, measure, and decouple software modules to allow independent evolution and testing.
- 5.1 Dimensions of Coupling: Afferent vs efferent coupling; instability metric ($I = C_e / (C_a + C_e)$); abstractness vs instability (the Main Sequence).
- 5.2 Forms of Coupling: Compile-time vs runtime coupling; data coupling; stamp coupling; control coupling; temporal coupling.
- 5.3 Temporal Coupling in API Design: Method execution order dependencies; builder invariants; eliminating temporal coupling via factory methods and state machines.
- 5.4 Change Propagation and Fragility: Blast radius of changes; dependency graphs; circular dependencies and breaking cycles.
- 5.5 Techniques for Decoupling: Event-driven notification, mediator pattern, inversion of control, anti-corruption layers (ACL), contracts and messaging.
**Senior-level bar:** Calculate instability and abstractness for a module, identify hidden temporal coupling in service methods, and redesign tightly coupled subsystems into loosely coupled event-driven or delegated components.

---

## Section 6 — Cohesion: Class, Module & Architectural Boundaries
**Outcome:** Group responsibilities into highly cohesive units that change for the same business reasons.
- 6.1 The Spectrum of Cohesion: Coincidental, logical, temporal, procedural, communicational, sequential, and functional cohesion.
- 6.2 High Functional Cohesion: Designing classes where every member collaborates toward a single well-defined task.
- 6.3 Module and Package Cohesion: Common Closure Principle (CCP); Common Reuse Principle (CRP); organizing by technical layer vs feature/slice.
- 6.4 Identifying Misplaced Responsibilities: Feature envy, inappropriate intimacy, anemic domain models with bloated manager services.
**Senior-level bar:** Refactor a low-cohesion "Utility" or "Manager" class into focused, functionally cohesive domain components aligned with the Common Closure Principle.

---

## Section 7 — Abstraction & Encapsulation in Depth
**Outcome:** Design crisp, durable abstraction boundaries that hide volatility without leaking implementation details.
- 7.1 Levels of Abstraction: High-level business policies vs low-level I/O mechanisms; defining stable contracts.
- 7.2 Leaky Abstractions: Mechanics of leakage (exceptions, performance characteristics, query capabilities like `IQueryable<T>`); mitigating leaks.
- 7.3 Over-Abstraction vs Under-Abstraction: Indirection tax; premature abstraction; when anemic interfaces add cost without benefit.
- 7.4 Information Hiding: David Parnas's criteria; hiding secret design decisions, data representations, and external integration quirks.
**Senior-level bar:** Explain why exposing `IQueryable<T>` across an architectural boundary is a catastrophic leaky abstraction, and propose a clean, encapsulated repository/query contract.

---

## Section 8 — Maintainability, Technical Debt & Evolution
**Outcome:** Manage technical debt pragmatically, refactor legacy codebases safely, and ensure long-term system evolvability.
- 8.1 Technical Debt Taxonomy: Deliberate vs inadvertent debt; prudent vs reckless debt (Martin Fowler's debt quadrant); interest vs principal.
- 8.2 Code Smell Catalog: Bloaters, Object-Orientation Abusers, Change Preventers, Dispensables, Couplers; automated static analysis (.NET analyzers, SonarQube).
- 8.3 Safe Refactoring Strategies: Working with legacy code (Michael Feathers); characterization tests, seams, sprout/wrap method, Mikado method.
- 8.4 Extensibility Without Over-Engineering: Designing extension points (events, middleware, plugins, strategy pattern) only at proven variation points.
- 8.5 Backwards Compatibility & Versioning: Semantic versioning; binary, source, and behavioral compatibility in C# libraries; deprecation strategies.
**Senior-level bar:** Formulate a prioritized technical debt remediation plan that quantifies business risk, cost of delay, and implementation safety using automated characterization testing.

---

## Section 9 — Applying Fundamentals to Enterprise .NET Architecture
**Outcome:** Apply software engineering fundamentals directly to modern ASP.NET Core, EF Core, and clean enterprise application architectures.
- 9.1 Dependency Injection in ASP.NET Core: Service lifetimes (Transient, Scoped, Singleton); captive dependencies; `IServiceScopeFactory`; object graph construction.
- 9.2 Domain Modeling vs Persistence Modeling: Separating EF Core entities from pure domain models; mapping strategies; encapsulation with private setters and backing fields.
- 9.3 Middleware Pipeline Architecture: Chain of Responsibility in ASP.NET Core; request/response short-circuiting; ambient context propagation.
- 9.4 Separation of Concerns in Web APIs: Minimal APIs vs Controllers; MediatR / command handlers; validation pipelines (FluentValidation); domain exceptions vs HTTP responses.
- 9.5 Enterprise Integration Boundaries: Ports and Adapters (Hexagonal); Anti-Corruption Layer (ACL); Outbox pattern for reliable domain event dispatching.
**Senior-level bar:** Identify captive dependency bugs that cause concurrency deadlocks or memory leaks, and design an EF Core domain model that preserves encapsulation without breaking ORM change tracking.

---

## Section 10 — Senior-Level Design Reviews & Interview Scenarios
**Outcome:** Conduct rigorous, constructive design reviews and articulate architectural decisions with authority in senior interview settings.
- 10.1 Systematic Code Review Methodology: Reviewing for correctness, invariants, concurrency, performance, and maintainability before style and syntax.
- 10.2 Reviewing Flawed Enterprise Code: Full walkthroughs of anemic models, primitive obsession, temporal coupling, and hidden race conditions.
- 10.3 Defending Architectural Trade-offs: Structuring interview responses using the STAR method; justifying technical choices against constraints.
- 10.4 Refactoring Legacy Systems: Staged migration plans, feature flags, strangler fig pattern, backward-compatible schema changes.
- 10.5 Comprehensive Assessment & Capstone: End-to-end evaluation scenario combining all fundamentals.
**Senior-level bar:** Deliver an authoritative, constructive critique of a complex enterprise PR, categorizing issues by severity, explaining business risks, and providing idiomatic refactored solutions.

---

# Part II — Lessons

## Section 1 — Object-Oriented Programming (OOP) Deep Dive

### 1.1 The Object Model: State, Behavior, and Identity

#### Fundamentals & Internal Mechanics
Object-Oriented Programming models software as collaborating units termed **objects**. An object is defined by three fundamental properties:
1. **State:** The data held by the object at any instantaneous moment in runtime memory.
2. **Behavior:** The operations, transformations, and business actions the object can perform upon its state or in coordination with other objects.
3. **Identity:** The unique existence of the object that distinguishes it from all other objects, even if their state is byte-for-byte identical.

In C#/.NET:
- A **Class** is the metadata and executable blueprint defined in IL (Intermediate Language) and loaded into the CLR's internal `MethodTable`.
- An **Object** is a concrete instance allocated on the GC Heap, consisting of an Object Header (sync block index), a MethodTable Pointer (`TypeHandle`), and memory fields.

#### C#/.NET Implementation
```csharp
public sealed class BankAccount
{
    private readonly List<Transaction> _transactions = [];

    public BankAccountId Id { get; }
    public AccountNumber Number { get; }
    public Money Balance { get; private set; }

    public BankAccount(BankAccountId id, AccountNumber number, Money initialDeposit)
    {
        Id = id ?? throw new ArgumentNullException(nameof(id));
        Number = number ?? throw new ArgumentNullException(nameof(number));
        ArgumentNullException.ThrowIfNull(initialDeposit);

        Balance = initialDeposit;
        _transactions.Add(new Transaction(Guid.CreateVersion7(), initialDeposit, TransactionType.Credit, DateTimeOffset.UtcNow));
    }

    public void Deposit(Money amount)
    {
        ArgumentNullException.ThrowIfNull(amount);
        if (amount.Amount <= 0)
            throw new ArgumentOutOfRangeException(nameof(amount), "Deposit amount must be positive.");

        Balance = Balance.Add(amount);
        _transactions.Add(new Transaction(Guid.CreateVersion7(), amount, TransactionType.Credit, DateTimeOffset.UtcNow));
    }

    public void Withdraw(Money amount)
    {
        ArgumentNullException.ThrowIfNull(amount);
        if (amount.Amount <= 0)
            throw new ArgumentOutOfRangeException(nameof(amount), "Withdrawal amount must be positive.");

        if (Balance.Amount < amount.Amount)
            throw new InvalidOperationException($"Insufficient funds. Current balance: {Balance.Amount}, requested: {amount.Amount}");

        Balance = Balance.Subtract(amount);
        _transactions.Add(new Transaction(Guid.CreateVersion7(), amount, TransactionType.Debit, DateTimeOffset.UtcNow));
    }

    public IReadOnlyCollection<Transaction> GetTransactions() => _transactions.AsReadOnly();
}
```

#### Enterprise Scenario
In enterprise banking systems, separating domain identity from runtime reference identity is critical. When two concurrent requests query the database for account `ACC-8831`, Entity Framework Core or Dapper reconstructs two separate instances in memory across different threads. They possess distinct reference identities (`object.ReferenceEquals(a1, a2) == false`), but represent the exact same enterprise entity with domain identity `ACC-8831`. Confusing reference identity with entity identity leads to concurrency bugs, caching inconsistencies, and duplicate record insertions.

#### Trade-offs, Alternatives & Common Mistakes
| Approach | Strengths | Failure Modes & Risks |
|---|---|---|
| **Rich Domain Model (OOP)** | Business rules reside with data; impossible to create invalid state. | Learning curve; requires careful mapping to ORM persistence layers. |
| **Anemic Domain Model (Anti-pattern)** | Simple DTOs with public getters/setters; easy serialization. | Business logic scatters across dozens of service classes; invariants easily bypassed. |
| **Pure Functional Model** | Immutable data structures and pure functions; zero side effects. | Verbose state threading in complex domain workflows; less idiomatic in standard C# ecosystems. |

#### What a Senior Engineer Is Expected to Know
A mid-level developer sees an object as a data packet with helper methods. A senior engineer recognizes that an object's primary duty is **invariant maintenance**: guaranteeing that from constructor return through every method execution, the object can never be coerced into an illegal business state.

---

### 1.2 Value Types, Reference Types, and Memory Semantics

#### Fundamentals & Internal Mechanics
The CLR type system divides all types into two semantic categories:
- **Reference Types (`class`, `record class`, `interface`, `delegate`):** Variables hold a reference (a pointer) to memory allocated on the managed heap. Assignment copies the reference, not the payload.
- **Value Types (`struct`, `record struct`, `enum`):** Variables hold the actual data payload. Assignment copies the values field-by-field.

**Common Myth Debunked:** "Value types live on the stack; reference types live on the heap."
*Reality:* Storage location is governed by lifetime and variable declaration context, not whether the type is a struct or class:
- A local value type variable inside a method executes on the stack (or CPU register).
- A value type defined as a field within a `class` resides entirely on the managed heap inside that class instance's memory buffer.
- Value types captured in lambda expressions (closures) or `async`/`await` state machines are hoisted to compiler-generated classes on the managed heap.

#### C#/.NET Type Category Matrix
| Feature | `class` | `struct` | `record class` | `record struct` |
|---|---|---|---|---|
| **Type Category** | Reference | Value | Reference | Value |
| **Default Assignment** | Copies reference | Copies memory bits | Copies reference | Copies memory bits |
| **Positional Syntax Defaults** | N/A | N/A | `init`-only properties (Immutable) | Mutable properties (unless `readonly record struct`) |
| **Default Equality** | Reference Identity | Structural (via reflection fallback `ValueType.Equals`) | Generated Value-based (fast code-gen) | Generated Value-based (fast code-gen) |
| **`==` and `!=` Operators** | Reference equality (unless overloaded) | **None** (must be explicitly overloaded) | Generated value equality | Generated value equality |
| **Inheritance** | Single class inheritance | Interfaces only | Single record inheritance | Interfaces only |
| **Heap Boxing Risk** | Never | When cast to `object` or `interface` | Never | When cast to `object` or `interface` |

#### Memory Layout and Allocation Mechanics
Every heap object in the 64-bit CLR has an overhead of 16 bytes:
1. **Object Header (8 bytes):** Stores synchronization block index, hash codes, and GC pinning flags.
2. **MethodTable Pointer (8 bytes):** Points to the type's runtime descriptor and virtual method dispatch table.

A `struct` has **zero object header overhead** when stored unboxed. However, casting a struct to an interface (e.g., `IComparable`) triggers **boxing**: the CLR allocates a box object on the heap, copies the struct value into it, and returns the reference.

#### C#/.NET Implementation
```csharp
// Record Class: Reference semantics with value equality and init-only immutability
public record Money(decimal Amount, string Currency)
{
    public Money Add(Money other)
    {
        if (Currency != other.Currency)
            throw new InvalidOperationException($"Currency mismatch: {Currency} vs {other.Currency}");
        return this with { Amount = Amount + other.Amount };
    }
}

// Readonly Record Struct: Value semantics, stack-friendly, no boxing, generated == operator
public readonly record struct GeoCoordinate(double Latitude, double Longitude)
{
    public GeoCoordinate
    {
        if (Latitude is < -90 or > 90)
            throw new ArgumentOutOfRangeException(nameof(Latitude), "Latitude must be between -90 and 90.");
        if (Longitude is < -180 or > 180)
            throw new ArgumentOutOfRangeException(nameof(Longitude), "Longitude must be between -180 and 180.");
    }
}
```

---

### 1.3 Encapsulation and Invariant Enforcement

#### Fundamentals & Internal Mechanics
Encapsulation is commonly misunderstood as simply putting private backing fields behind public properties with getters and setters. That is **data hiding**, which is merely a syntactic mechanism.
**Encapsulation** is the strict bundling of data with the business rules that manipulate it, such that the object hides its internal representation and guarantees that its **invariants** (rules that must always hold true) are never violated.

An **Anemic Domain Model** (where entities have public getters and setters and all logic lives in external `Service` classes) completely destroys encapsulation.

#### Enterprise Refactoring: Anemic Order vs Encapsulated Domain Model

```csharp
// BAD: Anemic Model violating encapsulation
public class AnemicOrder
{
    public Guid Id { get; set; }
    public string Status { get; set; } = default!; // Magic string! Anyone can set it to "Confirmed" without payment!
    public decimal Total { get; set; }              // Anyone can alter Total directly!
    public List<AnemicOrderLine> Lines { get; set; } = []; // External code can clear or add lines without recalculation!
}

// GOOD: Strictly Encapsulated Domain Entity
public sealed class Order
{
    private readonly List<OrderLine> _lines = [];

    public OrderId Id { get; }
    public OrderStatus Status { get; private set; }
    public CustomerId CustomerId { get; }
    public IReadOnlyCollection<OrderLine> Lines => _lines.AsReadOnly();
    public Money Total => _lines.Aggregate(new Money(0, "USD"), (acc, line) => acc.Add(line.Subtotal));

    public Order(OrderId id, CustomerId customerId)
    {
        Id = id ?? throw new ArgumentNullException(nameof(id));
        CustomerId = customerId ?? throw new ArgumentNullException(nameof(customerId));
        Status = OrderStatus.Draft;
    }

    public void AddLine(ProductId productId, int quantity, Money unitPrice)
    {
        if (Status != OrderStatus.Draft)
            throw new InvalidOperationException("Cannot add lines to an order that is not in Draft status.");

        if (quantity <= 0)
            throw new ArgumentOutOfRangeException(nameof(quantity), "Quantity must be strictly positive.");

        var existing = _lines.FirstOrDefault(l => l.ProductId == productId);
        if (existing is not null)
        {
            _lines.Remove(existing);
            _lines.Add(existing with { Quantity = existing.Quantity + quantity });
        }
        else
        {
            _lines.Add(new OrderLine(productId, quantity, unitPrice));
        }
    }

    public void Confirm()
    {
        if (Status != OrderStatus.Draft)
            throw new InvalidOperationException($"Cannot confirm order in status '{Status}'. Only Draft orders can be confirmed.");

        if (_lines.Count == 0)
            throw new InvalidOperationException("Cannot confirm an order with zero lines.");

        Status = OrderStatus.Confirmed;
    }

    public void Cancel(string reason)
    {
        if (Status == OrderStatus.Completed || Status == OrderStatus.Shipped)
            throw new InvalidOperationException($"Cannot cancel order in status '{Status}'.");

        Status = OrderStatus.Cancelled;
    }
}

public enum OrderStatus { Draft, Confirmed, Paid, Shipped, Completed, Cancelled }
public record OrderId(Guid Value);
public record CustomerId(Guid Value);
public record ProductId(Guid Value);
public record OrderLine(ProductId ProductId, int Quantity, Money UnitPrice)
{
    public Money Subtotal => new(UnitPrice.Amount * Quantity, UnitPrice.Currency);
}
```

> **Senior review note — find the hidden invariant leak:** `Total` seeds the aggregation with `new Money(0, "USD")`. If an order's lines are priced in EUR, `Money.Add` throws (or worse, silently mixes currencies if `Add` doesn't check). The real invariant is *"an order has exactly one currency"*, and nothing in this class owns it. The fix is to make currency part of the aggregate's state (`Order(OrderId id, CustomerId customerId, Currency currency)`) and reject any `AddLine` whose `unitPrice.Currency` differs. Interviewers love this kind of question: the code *looks* encapsulated, but an invariant was never actually given an owner.

#### Defeating Primitive Obsession: Value Objects & Strongly-Typed IDs

**Primitive Obsession** is when domain concepts are represented with raw primitives: `string email`, `decimal amount`, `Guid customerId`. It's the most common way encapsulation fails *between* objects rather than inside them:

1. **Validation gets scattered.** Every method that takes `string email` has to re-check the format, or trust that someone upstream did. In practice, someone eventually forgets.
2. **Arguments get swapped silently.** `Transfer(Guid fromAccountId, Guid toAccountId, Guid initiatedByUserId)` compiles just fine with the arguments in any order. The bug shows up in production as money moving the wrong way.
3. **Meaning gets lost.** `decimal 19.99` doesn't say whether it's EUR or USD, gross or net, or rounded to cents.

A **Value Object** fixes this by making the concept a type that **can only be constructed in a valid state**. Once a value of type `EmailAddress` exists, the rest of the system never needs to validate it again. This is often summarized as ***"parse, don't validate"***: check the raw input once at the boundary and turn it into a type that carries the proof.

```csharp
// 1. Strongly-typed IDs: zero-cost wrappers (readonly record struct = no heap allocation)
public readonly record struct OrderId(Guid Value)
{
    public static OrderId New() => new(Guid.CreateVersion7());
    public override string ToString() => Value.ToString();
}

public readonly record struct AccountId(Guid Value);
public readonly record struct UserId(Guid Value);

// Swapped arguments are now a COMPILE error, not a production incident:
public interface ITransferService
{
    Task TransferAsync(AccountId from, AccountId to, UserId initiatedBy, Money amount, CancellationToken ct);
}

// 2. Validated Value Object: impossible to construct an invalid instance
public sealed record EmailAddress
{
    public string Value { get; }

    private EmailAddress(string value) => Value = value;

    // "Parse, don't validate": the only way in is through this factory
    public static Result<EmailAddress> Create(string? raw)
    {
        if (string.IsNullOrWhiteSpace(raw))
            return Result<EmailAddress>.Failure(new Error("email.empty", "Email is required."));

        var normalized = raw.Trim().ToLowerInvariant();
        if (normalized.Length > 254 || !MailAddress.TryCreate(normalized, out _))
            return Result<EmailAddress>.Failure(new Error("email.invalid", "Email format is invalid."));

        return Result<EmailAddress>.Success(new EmailAddress(normalized));
    }

    public override string ToString() => Value;
}

// 3. EF Core persistence without leaking the primitive into the domain
public sealed class CustomerConfiguration : IEntityTypeConfiguration<Customer>
{
    public void Configure(EntityTypeBuilder<Customer> builder)
    {
        builder.Property(c => c.Id)
               .HasConversion(id => id.Value, value => new CustomerId(value));

        builder.Property(c => c.Email)
               .HasConversion(e => e.Value, raw => EmailAddress.Create(raw).Value) // DB data is trusted
               .HasMaxLength(254);
    }
}
```

**Trade-offs a senior engineer should name:**
- **Serialization & binding friction:** `System.Text.Json` and Minimal API binding need a `JsonConverter` or `TryParse`/`IParsable<T>` on each wrapper. Libraries such as *StronglyTypedId* or *Vogen* generate this boilerplate with source generators.
- **Where to stop:** Wrap concepts that carry **rules or meaning** (money, email, IDs that are easy to mix up, quantities with units). Don't wrap every `string Notes` field; that's ceremony without payoff.
- **`record struct` default value trap:** `default(OrderId)` is `Guid.Empty`. Struct wrappers can't stop `default` from existing, so validate at boundaries, or use a `sealed record` class when "unset" must be impossible.

---

### 1.4 Inheritance, Polymorphism, and Dispatch

#### Fundamentals & Internal Mechanics
Polymorphism allows objects of different concrete types to be manipulated through a unified interface or base class pointer.
The CLR implements polymorphic method execution through two distinct dispatch mechanisms:

1. **Virtual Method Dispatch (Vtable / MethodTable):**
   - Every class has a `MethodTable` structure created by the runtime at load time.
   - Non-virtual methods are bound at compile time directly to the native code address (static call `call`).
   - Virtual methods are invoked via indirect call (`callvirt`). The CPU looks up the object's `MethodTable`, indexes into the virtual method slot table, and branches to the overridden address.
2. **Interface Dispatch (Stub Dispatch):**
   - Because a class can implement dozens of interfaces in any order, interface methods cannot occupy fixed slot indexes in the class's primary method table.
   - The CLR uses **Virtual Stub Dispatch (VSD)** consisting of a cache hierarchy (monomorphic inline cache, polymorphic cache, and megamorphic hash table lookup) to resolve interface method addresses efficiently.

#### Shadowing (`new`) vs Overriding (`override`)
- `override`: Replaces the virtual slot in the object's `MethodTable`. Regardless of whether the variable is typed as the base class or derived class, the derived implementation executes.
- `new`: Declares a completely separate, non-polymorphic method that hides the base method by name. If invoked through a base class reference, the base method executes. This is a notorious source of enterprise bugs.

```csharp
public class BaseService
{
    public virtual string GetName() => "Base";
    public string GetRole() => "BaseRole";
}

public class DerivedService : BaseService
{
    public override string GetName() => "Derived";
    public new string GetRole() => "DerivedRole"; // Shadowing
}

// Calling behavior:
BaseService svc = new DerivedService();
Console.WriteLine(svc.GetName()); // "Derived" (Polymorphic vtable dispatch)
Console.WriteLine(svc.GetRole()); // "BaseRole"  (Static compile-time dispatch to BaseService!)
```

#### Why `sealed` by Default Matters
Sealing classes (`public sealed class X`) is a best practice in modern .NET:
1. **Devirtualization:** The JIT compiler recognizes that no derived class can exist, allowing it to bypass virtual table lookup and convert indirect calls into direct static calls or inline the method body entirely.
2. **Security & Invariants:** Prevents external callers from subclassing domain entities and tampering with state invariants or overriding disposal logic.

---

### 1.5 Composition over Inheritance

#### Fundamentals & Internal Mechanics
Inheritance is the strongest coupling relationship in object-oriented design. The **Fragile Base Class Problem** occurs when modifications to internal implementation details of a base class inadvertently break the invariants and behavior of derived classes.

#### The Problem: Inheritance Breakage
```csharp
// Base class provided by a framework or shared library
public class ObservableList<T> : List<T>
{
    public int AddCount { get; private set; }

    public new void Add(T item)
    {
        AddCount++;
        base.Add(item);
    }

    public new void AddRange(IEnumerable<T> collection)
    {
        foreach (var item in collection)
        {
            Add(item); // If base.AddRange internally calls Add(), AddCount gets double-counted!
        }
    }
}
```

#### The Solution: Composition with Delegation
Instead of inheriting, wrap the dependency as a private field and expose only the intended contract:
```csharp
public sealed class CountingBuffer<T> : IReadOnlyCollection<T>
{
    private readonly List<T> _items = [];

    public int AddCount { get; private set; }
    public int Count => _items.Count;

    public void Append(T item)
    {
        AddCount++;
        _items.Add(item);
    }

    public void AppendRange(IEnumerable<T> items)
    {
        ArgumentNullException.ThrowIfNull(items);
        foreach (var item in items)
        {
            Append(item);
        }
    }

    public IEnumerator<T> GetEnumerator() => _items.GetEnumerator();
    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}
```

---

### 1.6 Interfaces vs Abstract Classes

#### Comparison Matrix
| Dimension | `interface` | `abstract class` |
|---|---|---|
| **Multiple Implementation** | Yes (a class can implement multiple interfaces) | No (single base class inheritance only) |
| **State Storage** | Cannot store instance fields | Can declare instance fields, state, and constructors |
| **Evolution** | Adding members breaks implementers (unless Default Interface Methods are used) | Can add concrete virtual methods without breaking subclasses |
| **Speed** | Dispatched via Virtual Stub Dispatch | Dispatched via fixed MethodTable Vtable slot |
| **Purpose** | Defines a behavioral contract ("Can-Do") | Defines an incomplete template and shared identity ("Is-A") |

#### Default Interface Methods (DIM) in .NET
Introduced in C# 8, interfaces can provide default method implementations.
**Critical Rule:** DIM is intended for library authors evolving API contracts for backward compatibility. Default interface implementations are **not inherited by the implementing class directly**; they can only be invoked through an interface reference:
```csharp
public interface IAuditLogger
{
    void Log(string message);
    void LogError(string message) => Log($"[ERROR] {message}"); // Default implementation
}

public class ConsoleLogger : IAuditLogger
{
    public void Log(string message) => Console.WriteLine(message);
}

// Invocation:
var logger = new ConsoleLogger();
// logger.LogError("Crash"); // COMPILE ERROR! Not accessible directly on concrete class!
((IAuditLogger)logger).LogError("Crash"); // OK: Dispatched via interface reference
```

---

### 1.7 Object Lifecycle and Immutability

#### Fundamentals & Internal Mechanics
Garbage Collection handles managed memory reclamation, but **it does not manage external unmanaged resources** (operating system handles, database connections, sockets, locks).

#### `IDisposable` and the Standard Dispose Pattern
```csharp
public sealed class ReliableFileBuffer : IDisposable
{
    private SafeFileHandle? _fileHandle;
    private bool _disposed;

    public ReliableFileBuffer(string path)
    {
        _fileHandle = File.OpenHandle(path, FileMode.OpenOrCreate, FileAccess.ReadWrite);
    }

    public void Dispose()
    {
        if (_disposed) return;

        _fileHandle?.Dispose();
        _fileHandle = null;
        _disposed = true;
    }

    public void Write(ReadOnlySpan<byte> bytes)
    {
        ObjectDisposedException.ThrowIf(_disposed, this);
        RandomAccess.Write(_fileHandle!, bytes, 0);
    }
}
```

#### Immutability Mechanics
- **Shallow Immutability:** The object's own fields cannot be changed after instantiation, but referenced objects may remain mutable.
- **Deep Immutability:** The object and its entire transitive object graph are completely immutable.

```csharp
// Shallow immutability warning:
public record Team(string Name, List<string> Members); // Members list can be modified externally!

// Deep immutability:
public record ImmutableTeam(string Name, ImmutableList<string> Members);
```

---

### 1.8 Equality and Hashing

#### The Three Levels of Equality
1. **Reference Equality:** Do two references point to the exact same memory address on the heap? Checked via `object.ReferenceEquals(a, b)`.
2. **Value / Structural Equality:** Do two instances have the same field data? Implemented via `IEquatable<T>` and `operator ==`.
3. **Domain Entity Equality:** Do two distinct objects represent the same business entity regardless of memory address or mutated properties? Defined by unique domain identifier (e.g., `CustomerId`).

#### The Invariant Contract of `GetHashCode`
If two objects are equal according to `Equals`, their `GetHashCode` **must return the exact same integer**.
If `GetHashCode` changes while an object is stored as a key in a `Dictionary<TKey, TValue>` or `HashSet<T>`, the entry is permanently orphaned and cannot be retrieved.

```csharp
public sealed class CustomerEntity : IEquatable<CustomerEntity>
{
    public Guid Id { get; }
    public string Name { get; set; }

    public CustomerEntity(Guid id, string name)
    {
        Id = id;
        Name = name;
    }

    // Entity equality is defined SOLELY by Id
    public bool Equals(CustomerEntity? other)
    {
        if (other is null) return false;
        if (ReferenceEquals(this, other)) return true;
        return Id == other.Id;
    }

    public override bool Equals(object? obj) => obj is CustomerEntity other && Equals(other);

    public override int GetHashCode() => Id.GetHashCode();

    public static bool operator ==(CustomerEntity? left, CustomerEntity? right) => Equals(left, right);
    public static bool operator !=(CustomerEntity? left, CustomerEntity? right) => !Equals(left, right);
}
```

#### Customizing Equality Externally with `IEqualityComparer<T>`
While `IEquatable<T>` defines a type's *intrinsic* equality, enterprise applications often require *extrinsic* or context-specific equality—such as comparing third-party DTOs you do not own, or matching domain identifiers using normalized, case-insensitive rules in a `Dictionary<TKey, TValue>` or `HashSet<T>`. `IEqualityComparer<T>` decouples comparison strategy from the type itself.

```csharp
public sealed record TaxRegistrationCode(string CountryIso, string RawIdentifier);

public sealed class NormalizedTaxCodeComparer : IEqualityComparer<TaxRegistrationCode>
{
    public static readonly NormalizedTaxCodeComparer Instance = new();

    public bool Equals(TaxRegistrationCode? x, TaxRegistrationCode? y)
    {
        if (ReferenceEquals(x, y)) return true;
        if (x is null || y is null) return false;

        return string.Equals(x.CountryIso, y.CountryIso, StringComparison.OrdinalIgnoreCase)
            && Normalize(x.RawIdentifier).SequenceEqual(Normalize(y.RawIdentifier));
    }

    public int GetHashCode(TaxRegistrationCode obj)
    {
        ArgumentNullException.ThrowIfNull(obj);
        var hash = new HashCode();
        hash.Add(obj.CountryIso, StringComparer.OrdinalIgnoreCase);

        foreach (char c in obj.RawIdentifier)
        {
            if (char.IsLetterOrDigit(c))
            {
                hash.Add(char.ToUpperInvariant(c));
            }
        }

        return hash.ToHashCode();
    }

    private static string Normalize(string input) =>
        string.Create(input.Length, input, static (span, src) =>
        {
            int idx = 0;
            foreach (char c in src)
            {
                if (char.IsLetterOrDigit(c))
                    span[idx++] = char.ToUpperInvariant(c);
            }
        }).TrimEnd('\0');
}

// Usage: "de-123 456" and "DE123-456" resolve to the exact same dictionary bucket and key!
var registry = new Dictionary<TaxRegistrationCode, string>(NormalizedTaxCodeComparer.Instance);
```

---

### Section 1 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: What is the exact difference between how interfaces and virtual methods are dispatched at runtime in the CLR?**
> **Strong answer:** Virtual methods are dispatched using a fixed-index virtual function table (Vtable) located directly in the type's `MethodTable`. At call sites, the JIT emits a direct indexed indirect call (`callvirt`) relative to the object's method table pointer. Because a class can implement dozens of interfaces in arbitrary order, interfaces cannot share a fixed slot index. The CLR resolves interface calls using Virtual Stub Dispatch (VSD). VSD employs a multi-tiered caching mechanism: an inline monomorphic cache for single-implementer call sites, a polymorphic cache for multiple implementers, and a megamorphic global hash table lookup when polymorphism exceeds cache capacity. Consequently, interface dispatch can be slightly more expensive than class-based virtual dispatch unless the JIT successfully devirtualizes the call.

**Q2: Why should an enterprise domain entity never expose public property setters?**
> **Strong answer:** Exposing public property setters degrades the entity into an anemic data transfer object and destroys encapsulation. When setters are public, the entity cannot enforce its business invariants because any external service, controller, or test can mutate fields into invalid combinations (such as setting an Order to 'Shipped' without line items or payment confirmation). By making setters private and exposing meaningful domain methods with guard clauses (such as `ConfirmOrder()`, `AddLine()`, `Cancel()`), state transitions are strictly governed, invariants are enforced at compile and runtime boundaries, and domain rules remain centralized rather than scattered across procedural services.

**Q3: Can a struct implement `IDisposable`, and what is the risk of doing so?**
> **Strong answer:** Yes, a struct can implement `IDisposable`. In modern C#, using a struct with `using var s = new MyStruct();` is zero-allocation because the compiler emits a direct non-boxing `Dispose()` call on the stack. However, if the struct is cast to `IDisposable` (for instance, passed to a method accepting `IDisposable`), boxing occurs on the managed heap, creating garbage collection pressure and copying the struct value. If the struct mutates state during disposal, it mutates the boxed copy, leaving the original stack instance unaffected.

#### Practical Exercises (Attempt without documentation)
1. **Exercise 1.1:** Write a generic `ValueObject<T>` base record or struct that enforces value equality and demonstrates that two distinct instances placed into a `HashSet<T>` are treated as duplicates.
2. **Exercise 1.2:** Implement an `Order` aggregate with three states (`Created`, `Paid`, `Fulfilled`). Ensure that calling `Fulfill()` when `Status == Created` throws a domain exception, and prove that external callers cannot bypass this rule through collection manipulation or property assignment.
3. **Exercise 1.3:** Create a benchmark demonstrating the allocation difference between boxing a `struct` via an interface call versus using a generic constraint `where T : struct, IOperation`.

---

## Section 2 — SOLID Principles in Practice

### 2.1 Single Responsibility Principle (SRP)

#### Fundamentals & Internal Mechanics
> *"A class should have one, and only one, reason to change."* — Robert C. Martin.

SRP is not about making classes tiny or limiting them to one method. It is about **coupling to business actors**.
A "reason to change" corresponds to a stakeholder or business department requiring a modification:
- If a change requested by the Accounting team (e.g., tax calculation) breaks a feature used by the Logistics team (e.g., shipping slip generation), the class violates SRP.

#### Anti-Pattern: The God Class
```csharp
// VIOLATION: Has 3 distinct reasons to change (Accounting, Logistics, DBA)
public class OrderManager
{
    public void CalculateTax(Order order) { /* Accounting rule changes */ }
    public void GenerateShippingLabel(Order order) { /* Logistics vendor changes */ }
    public void SaveToSqlServer(Order order) { /* Database schema changes */ }
}
```

#### Refactored Architecture
```csharp
public sealed class TaxCalculator : ITaxCalculator
{
    public Money CalculateTax(Order order) => /* Pure domain math */;
}

public sealed class ShippingLabelGenerator : IShippingLabelGenerator
{
    public Label GenerateLabel(Order order) => /* Logistics layout */;
}

public sealed class SqlOrderRepository : IOrderRepository
{
    public Task SaveAsync(Order order, CancellationToken ct) => /* Persistence logic */;
}
```

---

### 2.2 Open/Closed Principle (OCP)

#### Fundamentals & Internal Mechanics
> *"Software entities should be open for extension, but closed for modification."*

You should be able to introduce new business behavior into a system without altering existing, tested source code. In C#, this is achieved via polymorphism, strategy patterns, decorators, and delegate injection.

#### Enterprise Scenario: Payment Processing Gateway
```csharp
// BAD: Violates OCP. Adding PayPal requires modifying this method and re-testing CreditCard!
public class PaymentProcessor
{
    public void Process(Order order, string paymentType)
    {
        if (paymentType == "CreditCard") { /* Stripe API */ }
        else if (paymentType == "PayPal") { /* PayPal API */ }
        else if (paymentType == "Crypto") { /* BitPay API */ }
    }
}

// GOOD: Open for extension via polymorphism and DI registration
public interface IPaymentGateway
{
    PaymentProvider Provider { get; }
    Task<PaymentResult> ChargeAsync(PaymentRequest request, CancellationToken ct);
}

public sealed class PaymentService(IEnumerable<IPaymentGateway> gateways)
{
    public async Task<PaymentResult> ProcessPaymentAsync(PaymentRequest request, CancellationToken ct)
    {
        var gateway = gateways.FirstOrDefault(g => g.Provider == request.Provider)
            ?? throw new NotSupportedException($"Gateway provider '{request.Provider}' is not supported.");

        return await gateway.ChargeAsync(request, ct);
    }
}
```

---

### 2.3 Liskov Substitution Principle (LSP)

#### Fundamentals & Internal Mechanics
> *"If $S$ is a subtype of $T$, then objects of type $T$ may be replaced with objects of type $S$ without altering any of the desirable properties of the program."* — Barbara Liskov (1987).

LSP defines behavioral subtyping. Syntactic inheritance is insufficient; the subtype must conform to the **behavioral contract** of the base type:
1. **Preconditions cannot be strengthened:** Derived methods cannot demand more strict input conditions than the base.
2. **Postconditions cannot be weakened:** Derived methods must guarantee at least everything the base guaranteed.
3. **Invariants must be preserved:** Subtypes cannot allow the object to enter states forbidden by the base.
4. **No new unexpected exceptions:** Derived methods must not throw exceptions that callers of the base type are unprepared to handle.

#### The Classic Violation: ReadOnly Collection Subtyping
```csharp
public class CustomCollection<T> : IList<T>
{
    // VIOLATION of LSP: Calling Add on a CustomReadOnlyCollection throws NotSupportedException!
    // Callers expecting an IList<T> expect Add() to work.
    public void Add(T item) => throw new NotSupportedException("Collection is read-only!");
}
```
*Correction:* Segregate interfaces. A read-only collection must implement `IReadOnlyList<T>`, not `IList<T>`.

#### Return Covariance (`out T`) and Parameter Contravariance (`in T`)
Liskov Substitution governs how generic interfaces and delegates preserve subtyping across type arguments:
1. **Covariance (`out T` — Producer / Return Position):**
   If `Derived` is a subtype of `Base` ($\text{Derived} \le \text{Base}$), a generic interface `IFoo<out T>` preserves the subtyping direction: `IFoo<Derived>` is substitutable for `IFoo<Base>`.
   - **Rule:** `T` can **only** appear in output (return) positions.
   - **.NET Examples:** `IEnumerable<out T>`, `IReadOnlyList<out T>`, `Func<out TResult>`.
   - **Why it is LSP-safe:** A caller expecting a stream of `Base` entities (`IEnumerable<Base>`) is completely safe receiving `IEnumerable<Derived>`, because every item produced out of the iterator satisfies the `Base` contract.
2. **Contravariance (`in T` — Consumer / Parameter Position):**
   A generic interface `IBar<in T>` *reverses* the subtyping direction: `IBar<Base>` is substitutable for `IBar<Derived>`.
   - **Rule:** `T` can **only** appear in input (method parameter) positions.
   - **.NET Examples:** `IComparable<in T>`, `IEqualityComparer<in T>`, `Action<in T>`.
   - **Why it is LSP-safe:** If a caller needs a handler that can validate a `VipCustomer` (`Action<VipCustomer>`), you can safely pass an `Action<Customer>` that knows how to validate *any* `Customer`. Because `Action<Customer>` demands *weaker* preconditions (only base `Customer` properties), passing a `VipCustomer` into it never violates LSP.
3. **Invariance (`T` — Both Input and Output):**
   Mutable collections like `IList<T>` are invariant because `T` is both consumed (`Add(T)`) and produced (`T this[int index]`). If `List<Dog>` were assignable to `IList<Animal>`, a caller could invoke `animals.Add(new Cat())`, corrupting the underlying `Dog` memory buffer at runtime (which is why C# array covariance `Animal[] a = new Dog[1]` was a historical design mistake that requires expensive runtime type-checks on every array write, throwing `ArrayTypeMismatchException`).

```csharp
public abstract record DomainEvent(Guid EventId, DateTimeOffset OccurredAt);
public sealed record OrderShippedEvent(Guid EventId, DateTimeOffset OccurredAt, Guid OrderId)
    : DomainEvent(EventId, OccurredAt);

// Contravariant consumer: accepts T in input positions only
public interface IEventHandler<in TEvent> where TEvent : DomainEvent
{
    void Handle(TEvent domainEvent);
}

public sealed class GlobalAuditEventHandler : IEventHandler<DomainEvent>
{
    public void Handle(DomainEvent domainEvent) =>
        Console.WriteLine($"[AUDIT] Event {domainEvent.EventId} at {domainEvent.OccurredAt:O}");
}

// LSP Contravariance in action:
// A handler for the BASE type (DomainEvent) can safely substitute for a handler of the DERIVED type!
IEventHandler<OrderShippedEvent> shippedHandler = new GlobalAuditEventHandler();
shippedHandler.Handle(new OrderShippedEvent(Guid.CreateVersion7(), DateTimeOffset.UtcNow, Guid.CreateVersion7()));

// LSP Covariance in action:
// A producer of DERIVED types can safely substitute for a producer of BASE types!
IReadOnlyList<OrderShippedEvent> shippedEvents = [new(Guid.CreateVersion7(), DateTimeOffset.UtcNow, Guid.CreateVersion7())];
IEnumerable<DomainEvent> baseEvents = shippedEvents;
```

---

### 2.4 Interface Segregation Principle (ISP)

#### Fundamentals & Internal Mechanics
> *"Clients should not be forced to depend upon interfaces that they do not use."*

Large "header interfaces" (interfaces with dozens of methods representing everything a service can possibly do) couple callers to irrelevant methods. When an interface changes, all implementing classes and consumer test suites must be recompiled and re-tested.

```csharp
// BAD: Fat interface
public interface IOrderService
{
    Task CreateOrderAsync(CreateOrderDto dto);
    Task CancelOrderAsync(Guid orderId);
    Task<OrderReportDto> GenerateMonthlyReportAsync(int year, int month);
    Task RecalculateLedgerAsync();
}

// GOOD: Segregated by consumer roles
public interface IOrderCreationService
{
    Task CreateOrderAsync(CreateOrderDto dto);
}

public interface IOrderReportingService
{
    Task<OrderReportDto> GenerateMonthlyReportAsync(int year, int month);
}
```

#### Role Interfaces vs Header Interfaces
- A **header interface** mirrors every public method of one implementation class (`IOrderService` mirrors `OrderService`, method for method). It's shaped by the *implementer*.
- A **role interface** describes exactly what one *client* needs (`IOrderReader`, `IClock`, `IEmailSender`). It's shaped by the *consumer*.

ISP is really a rule about **who designs the interface**: the client does. One implementation class can implement several role interfaces (`sealed class OrderService : IOrderCreationService, IOrderReportingService`), so splitting interfaces doesn't force you to split implementations.

#### ISP in the .NET BCL: Good and Bad Examples
- **Good:** `IReadOnlyList<T>` and `IReadOnlyDictionary<TKey, TValue>` let a method declare "I only read". A caller can pass a `List<T>`, an array, or an `ImmutableArray<T>`.
- **Good:** `IAsyncDisposable` is a separate role interface, not extra members bolted onto `IDisposable`.
- **Counter-example:** `System.IO.Stream` is a fat abstraction. Every stream has `Seek`, `Write`, and `Read`, guarded by `CanSeek` / `CanWrite` / `CanRead` flags. A `NetworkStream` throws `NotSupportedException` from `Seek`. That's a runtime capability check standing in for a compile-time contract, which is exactly what ISP is meant to prevent. The framework kept it for historical reasons. Don't copy that design into new APIs.

#### Why ISP Pays Off in Practice
1. **Smaller test doubles:** A handler that depends on `IOrderReader` (2 methods) needs a 2-method fake, not a 25-method mock where 23 members throw.
2. **Smaller blast radius:** Adding `RecalculateLedgerAsync()` to a fat interface forces every implementer and every test fake to change, even the ones that never call it.
3. **Clearer intent:** A constructor signature listing `IOrderReader, IClock` tells a reviewer what the class touches without reading its body.

---

### 2.5 Dependency Inversion Principle (DIP)

#### Fundamentals & Internal Mechanics
1. **High-level modules should not depend on low-level modules.** Both should depend on abstractions.
2. **Abstractions should not depend on details.** Details should depend on abstractions.

#### Architectural Boundary: Clean Architecture DIP
In clean architecture, the Core Domain (high-level policy) defines the interface `IOrderRepository`. The Infrastructure project (low-level detail) implements `IOrderRepository` using EF Core or Cosmos DB. The compile-time dependency arrows point inwards toward the Domain, inverting traditional procedural architectures where business logic depends directly on data access DLLs.

```text
[ Core Domain / Application ]       [ Infrastructure ]
   OrderService --------> IOrderRepository <|--- SqlOrderRepository (EF Core)
```

#### The Part Most Engineers Miss: Interface Ownership
The "inversion" is not about having an interface. It's about **which assembly owns it**.

- **Not inverted (common mistake):** `IOrderRepository` lives in `Company.Infrastructure.Data`, next to `SqlOrderRepository`. The Application project references Infrastructure to get the interface, so business logic still has a compile-time dependency on the data-access assembly. You've added an interface and kept the coupling.
- **Inverted:** `IOrderRepository` lives in `Company.Application` (the consumer). It's written in domain language (`Task<Order?> GetByIdAsync(OrderId id, ...)`, not `Task<OrderRow> SelectAsync(string sql)`). Infrastructure references Application and implements the port.

A quick test: **if you deleted the Infrastructure project, would the Application project still compile?** If not, DIP isn't applied.

#### The Composition Root
Something still has to connect abstractions to implementations. That place is the **Composition Root**: the one location (in ASP.NET Core, `Program.cs` or extension methods it calls) that references *every* project and builds the object graph:

```csharp
// Program.cs — the ONLY place that knows both the port and the adapter
builder.Services.AddScoped<IOrderRepository, SqlOrderRepository>();
builder.Services.AddSingleton(TimeProvider.System);          // the clock is a volatile dependency too
builder.Services.AddHttpClient<IPaymentGateway, StripePaymentGateway>();
```

Business classes must never call `serviceProvider.GetService<T>()` themselves. That's the **Service Locator** anti-pattern: it hides dependencies from the constructor signature and turns missing registrations into runtime failures.

#### Which Dependencies Deserve Inversion?
Mark Seemann's distinction between **stable** and **volatile** dependencies keeps DIP from turning into "an interface for everything":

| Volatile (invert these) | Stable (depend on them directly) |
|---|---|
| Databases, file systems, message brokers | `string`, `List<T>`, LINQ, `System.Text.Json` |
| External HTTP APIs and SDKs (Stripe, SendGrid) | Your own pure domain types (`Money`, `Order`) |
| Non-determinism: clock (`TimeProvider`), randomness, GUID generation | Deterministic helper logic with no I/O |
| Anything still being designed, or that you may swap | Mature BCL types with stable contracts |

---

### 2.6 SOLID Anti-Patterns and Over-Engineering
- **Interface Soup:** Creating an interface for every single class (`IOrder`, `ICustomer`, `IUser`) even when there is only one implementation and no polymorphic variance. This adds indirection without architectural value.
- **Dependency Injection Explosion:** Constructors accepting 15 dependencies indicate an SRP violation, not good DI practices.

#### SOLID Principles Pull Against Each Other
Applying each principle to its maximum doesn't give the best design, because they conflict:
- **SRP vs cohesion:** Splitting a class by every conceivable "reason to change" produces dozens of 10-line classes that must always change *together*. That's low cohesion in disguise, and it's now spread over 12 files. SRP should group code by **actor** (who requests changes), not by verb.
- **OCP vs YAGNI:** Making every module open for extension means guessing future variation points. Wrong guesses become dead abstractions that still have to be maintained. Apply OCP **after** the second or third variation shows up, not before.
- **DIP vs readability:** Every inverted dependency adds a hop when someone reads the code. Inverting a pure, deterministic calculator gains nothing and costs navigation.

#### When Does an Abstraction Earn Its Place?
Introduce an interface when at least one of these is true:
1. **There's a real second implementation**, either now or explicitly on the roadmap.
2. **It sits on an I/O or non-determinism boundary** that unit tests need to replace (database, HTTP, clock, queue).
3. **It's a published contract** consumed by another team or package, so it needs to be stable regardless of the implementation.

If none apply, a `sealed` concrete class is the better choice. It's simpler to read, the JIT can devirtualize it, and adding an interface later is a mechanical refactoring that IDEs automate.

---

### Section 2 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How do you explain the difference between Dependency Inversion, Inversion of Control, and Dependency Injection?**
> **Strong answer:** Inversion of Control (IoC) is the overarching architectural principle where the framework or runtime controls program flow rather than procedural custom code (the Hollywood Principle: 'Don't call us, we'll call you'). Dependency Inversion Principle (DIP) is a specific design rule stating that high-level business policies must not depend on low-level technical mechanisms; both must depend on abstractions. Dependency Injection (DI) is a concrete structural design pattern used to realize DIP and IoC: instead of a class instantiating its dependencies internally, those dependencies are supplied ('injected') from the outside, typically via constructor arguments resolved by a composition root or DI container.

**Q2: What is a subtle LSP violation you have encountered in .NET libraries?**
> **Strong answer:** A classic example is `Array.AsReadOnly()` or `Collection<T>` implementing `IList<T>`. When callers hold an `IList<T>`, the interface contract implies that invoking `.Add()` or `.Remove()` is legal. However, read-only wrappers throw `NotSupportedException` at runtime. This violates LSP because the subtype weakens the behavioral guarantees of the base abstraction. Modern .NET resolved this cleanly by introducing `IReadOnlyCollection<T>` and `IReadOnlyList<T>`, allowing callers to declare intent precisely at compile time.

#### Practical Exercises
1. **Exercise 2.1:** Take a monolithic `UserManager` class with registration, password hashing, email verification, and SQL logging, and decompose it into SRP-compliant classes wired together using decorators and events.
2. **Exercise 2.2:** Demonstrate an OCP-compliant tax calculation system that uses C# reflection or DI scanning to discover new country tax strategies dynamically without editing existing calculation files.

---

## Section 3 — Clean Code, Readability & Expressiveness at Scale

### 3.1 Cognitive Load and Readability
Code is read far more often than it is written. Clean code minimizes **extraneous cognitive load**—the mental overhead required to parse convoluted syntax, cryptic naming, and deep nesting that is unrelated to the actual business problem.

### 3.2 Naming as Architecture

A useful name communicates a domain concept, its units, and its observable contract. `Process()` hides the business action; `ReserveInventory()` tells the reader what must become true. `timeoutMilliseconds` prevents a unit mistake that `timeout` invites. Prefer the vocabulary used by domain experts over interchangeable suffixes such as `Helper`, `Manager`, and `Processor`.

Names also expose missing decisions:
- `GetCustomerAsync` versus `FindCustomerAsync`: document whether absence throws, returns `null`, or produces a typed not-found result. Naming alone is not enforcement.
- `AuthorizePaymentAsync` versus `CapturePaymentAsync`: these are different business operations, not synonyms for `PayAsync`.
- `createdAtUtc` versus `businessDate`: an instant and a calendar date require different semantics; a clearer name often reveals the need for a different type.

**Review technique:** Read the public signatures without their implementations. Can a caller predict side effects, units, failure cases, and ownership? If not, improve the contract rather than merely making the name longer.

### 3.3 Method Design & Single Level of Abstraction Principle (SLAP)
A method should do one conceptual thing at one consistent level of abstraction. A high-level orchestration method should not mix high-level business workflow steps with raw byte manipulation, string splitting, or low-level SQL connection handling.

```csharp
// BAD: Violates SLAP (Mixes high-level checkout flow with raw string parsing and SQL queries)
public async Task CheckoutAsync(Guid cartId)
{
    var cart = await _db.QueryAsync("SELECT * FROM Carts WHERE Id = @Id", new { Id = cartId });
    if (cart.Lines.Split(',').Length == 0) throw new Exception("Empty");
    // ...
}

// GOOD: Conforms to SLAP (Every line is at the exact same architectural level)
public async Task CheckoutAsync(CartId cartId, CancellationToken ct)
{
    var cart = await _cartRepository.GetByIdAsync(cartId, ct);
    cart.ValidateForCheckout();

    var payment = await _paymentService.AuthorizePaymentAsync(cart.Total, ct);
    var order = cart.ConvertToOrder(payment.TransactionId);

    await _orderRepository.SaveAsync(order, ct);
    await _eventPublisher.PublishAsync(new OrderPlacedEvent(order.Id), ct);
}
```

#### Command-Query Separation (CQS)
Methods should either:
- **Execute a Command:** Mutate state, returning `void` (or `Task`).
- **Execute a Query:** Return data without observable side effects.

Invoking a getter or query method should never alter database state or increment transaction balances.

**Where the heuristic bends:** A command may reasonably return the identifier it created, an outcome, or the item atomically removed from a queue. Splitting `TryDequeue` into `Peek` followed by `Remove` would introduce a race. The important property is that callers can predict mutation, not that every mutating method returns `void`. CQS is a method-design heuristic; CQRS is the larger architectural separation covered in Module 04.

#### Functional Core, Imperative Shell

Keep deterministic decisions separate from orchestration when it makes the rule easier to understand and test. For example, a pricing function can accept an immutable order snapshot, a tax policy, and an explicit effective date, then return a price breakdown. The application handler loads that snapshot, supplies the clock value, and persists the result.

This does not require replacing the whole domain model with functions. An aggregate can protect its state while delegating a calculation to a pure function. The payoff is being able to test rounding and policy boundaries without a database, clock, or mock framework. The shell still needs integration tests: a correct calculation can be persisted twice or applied to stale state.

### 3.4 Control Flow: Guard Clauses over Arrow Anti-Patterns
Avoid nested `if/else` ladders (the "Arrow Anti-pattern") by checking failure conditions early and returning immediately:

```csharp
// GOOD: Flat, legible guard clauses
public void ProcessRefund(Order order, decimal amount)
{
    ArgumentNullException.ThrowIfNull(order);
    if (amount <= 0)
        throw new ArgumentOutOfRangeException(nameof(amount), "Refund must be positive.");

    if (order.Status != OrderStatus.Paid)
        throw new InvalidOperationException("Can only refund paid orders.");

    if (amount > order.PaidAmount)
        throw new InvalidOperationException("Refund exceeds paid amount.");

    // Core business action executed flat at the end:
    order.ApplyRefund(amount);
}
```

### 3.5 Error Handling: Result Pattern vs Exceptions
In modern high-throughput C# systems, **Exceptions should be reserved for exceptional, unrecoverable circumstances** (network timeouts, database connection drops, hardware failure). Using exceptions for regular business validation (e.g., `InvalidEmailException`) introduces severe performance penalties (stack unwinding costs) and encourages unstructured goto-like control flow.

#### Idiomatic Result Pattern
```csharp
public readonly record struct Error(string Code, string Message);

public readonly struct Result<TValue>
{
    public bool IsSuccess { get; }
    public TValue Value { get; }
    public Error Error { get; }

    private Result(TValue value)
    {
        IsSuccess = true;
        Value = value;
        Error = default;
    }

    private Result(Error error)
    {
        IsSuccess = false;
        Value = default!;
        Error = error;
    }

    public static Result<TValue> Success(TValue value) => new(value);
    public static Result<TValue> Failure(Error error) => new(error);
}
```

---

### 3.6 Nullability, NRT Attributes & The Null-Object / Option Pattern

#### Nullable Reference Types (NRT) & Roslyn Static Flow Analysis
In modern .NET (`<Nullable>enable</Nullable>`), reference types are non-nullable by default (`Customer` vs `Customer?`). Crucially, **NRT is a compile-time static flow analysis feature, not a runtime guarantee** (`Customer` and `Customer?` compile to the exact same IL metadata type, annotated with `[Nullable]`). If external callers (or JSON deserializers) pass `null` into a non-nullable reference parameter, the runtime does not automatically block it unless your public boundary enforces `ArgumentNullException.ThrowIfNull(arg)`.

To make custom `Try*` and validation methods integrate seamlessly with the compiler's flow analyzer, use `System.Diagnostics.CodeAnalysis` null-state attributes:
- `[NotNullWhen(true)]`: Informs the compiler that if the method returns `true`, the `out` or input parameter is guaranteed non-null.
- `[MaybeNullWhen(false)]`: Allows generic `TryGetValue<T>(out T value)` signatures to output `default` when returning `false`, even if `T` is a non-nullable reference type.
- `[NotNullIfNotNull(nameof(input))]`: Expresses that the return value is non-null whenever the named input argument is non-null.

```csharp
using System.Diagnostics.CodeAnalysis;

public sealed record DiscountVoucher(string Code, decimal PercentageOff);

public interface IDiscountPolicy
{
    Money Apply(Money originalTotal);
}

// 1. NRT Static Flow Analysis with [NotNullWhen(true)]
public static class VoucherParser
{
    public static bool TryParse(
        string? rawInput,
        [NotNullWhen(true)] out DiscountVoucher? voucher)
    {
        if (string.IsNullOrWhiteSpace(rawInput) || !rawInput.StartsWith("PROMO-", StringComparison.Ordinal))
        {
            voucher = null;
            return false;
        }

        voucher = new DiscountVoucher(rawInput.Trim(), 0.10m);
        return true;
    }
}

// 2. The Null-Object Pattern: Eliminates repetitive `if (policy != null)` checks across business workflows
public sealed class NoOpDiscountPolicy : IDiscountPolicy
{
    public static readonly NoOpDiscountPolicy Instance = new();
    private NoOpDiscountPolicy() { }

    public Money Apply(Money originalTotal) => originalTotal; // Neutral, safe default behavior
}

// 3. Explicit Value-Typed Option<T>: Forces exhaustive matching when a Null-Object does not make domain sense
public readonly struct Option<T> where T : notnull
{
    private readonly T? _value;
    public bool HasValue { get; }

    private Option(T value)
    {
        ArgumentNullException.ThrowIfNull(value);
        _value = value;
        HasValue = true;
    }

    public static Option<T> Some(T value) => new(value);
    public static Option<T> None => default;

    public TResult Match<TResult>(Func<T, TResult> onSome, Func<TResult> onNone) =>
        HasValue ? onSome(_value!) : onNone();
}
```

---

### 3.7 Comments and Architectural Documentation

#### Self-Documenting Code vs Explanatory *Why* Comments
Code can only ever describe **what** the system is doing and **how** it is doing it. Code cannot always express **why** a non-obvious decision was made, which alternatives were rejected, or what external bug is being worked around.

| Comment Category | Engineering Verdict | Example |
|---|---|---|
| **Redundant *What* Comment (Noise)** | **Delete.** Restates the code and rots when logic changes. | `// Increment retry counter by 1`<br>`retryCount++;` |
| **Apology for Bad Naming** | **Refactor.** Rename the method/variable using Ubiquitous Language. | `// Check if customer has 0 unpaid invoices and active KYC`<br>`if (c.Inv == 0 && c.Stat == 2)` $\to$ `if (customer.IsEligibleForCreditIncrease())` |
| **Explanatory *Why* / Workaround Comment** | **Essential.** Preserves domain or hardware constraints invisible in code. | `// Legacy SAP gateway silently truncates payloads > 4000 bytes without returning HTTP 413.`<br>`// We chunk batches at 50 items to stay strictly below the 4KB frame limit (see ADR-019).` |
| **Public API Contract (`///` XML Docs)** | **Mandatory at boundaries.** Documents preconditions, thread-safety, and exceptions for NuGet/SDK consumers. | `/// <exception cref="InvalidOperationException">Thrown when account is frozen.</exception>` |

#### Preventing Comment Rot
Comments are not compiled or executed by the test suite; consequently, they decay silently when surrounding code is refactored (**comment rot**). A misleading, outdated comment is far more dangerous than no comment at all because it actively deceives the reader.
1. **Encode invariants in types and tests first:** Prefer `ReadOnlySpan<byte>`, `readonly record struct`, and unit test names over prose warnings.
2. **Keep Architecture Decision Records (ADRs) in source control:** Document macro-level trade-offs in versioned markdown files (`docs/adr/0019-sap-batch-chunking.md`) and link the ADR identifier directly in the code comment.

---

### Section 3 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: What are the architectural trade-offs between throwing domain exceptions versus returning a `Result<T>` pattern?**
> **Strong answer:** Throwing domain exceptions leverages native runtime control flow and forces callers to handle failures or abort execution. However, exceptions incur significant CPU and memory allocation overhead during stack-trace capture, make method signatures dishonest (a method signature does not indicate which exceptions it may throw), and can lead to uncontrolled bubbling. The `Result<T>` pattern turns expected domain failure modes into explicit, typed return values. This forces callers to handle errors at compile time, improves performance on high-throughput paths, and makes control flow deterministic. The trade-off is slightly more boilerplate and potential friction with standard ASP.NET Core exception filter middleware, which can be mitigated using ProblemDetails mapping.

#### Practical Exercises
1. **Exercise 3.1:** Refactor a 100-line nested procedural method containing 5 levels of `if/else` nesting into a flat, readable method enforcing SLAP and CQS with guard clauses.
2. **Exercise 3.2:** Implement an enterprise `Result<TValue, TError>` type with railway-oriented `Bind` and `Map` extension methods in C#.

## Section 4 — Core Software Design Principles & Heuristics

### 4.1 DRY (Don't Repeat Yourself)

#### Fundamentals & Internal Mechanics
> *"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."* — Andy Hunt and Dave Thomas (*The Pragmatic Programmer*).

DRY is frequently misunderstood as a purely syntactic rule: "never write the same block of code twice."
That is a dangerous misinterpretation. DRY applies to **duplication of knowledge and business rules**, not structural coincidences.

#### Accidental Duplication vs Knowledge Duplication
- **Knowledge Duplication (True DRY violation):** The algorithm for calculating sales tax is copied across both the billing service and the reporting pipeline. When tax laws change, one system is updated while the other is forgotten, creating financial discrepancies.
- **Accidental Duplication (Premature abstraction):** A `UserSignupRequest` in the API and a `CustomerEntity` in the database happen to share three fields (`FirstName`, `LastName`, `Email`). Forcing them to share a common base class or interface couples the external HTTP contract directly to internal database schema evolution.

```csharp
// BAD: Coupling independent domains under the guise of "DRY"
public class SharedPersonBase
{
    public string FirstName { get; set; } = default!;
    public string LastName { get; set; } = default!;
    public string Email { get; set; } = default!;
}

// When the Marketing team demands that Signups allow nickname-only logins,
// changing SharedPersonBase breaks internal database auditing rules!

// GOOD: Deliberate separation of domain contracts
public record UserRegistrationRequest(string FirstName, string LastName, string Email);
public sealed class CustomerEntity
{
    public CustomerId Id { get; init; } = default!;
    public string LegalFirstName { get; private set; } = default!;
    public string LegalLastName { get; private set; } = default!;
    public EmailAddress PrimaryEmail { get; private set; } = default!;
}
```

---

### 4.2 KISS (Keep It Simple, Stupid) & YAGNI (You Aren't Gonna Need It)

#### Fundamentals & Internal Mechanics
- **KISS:** Software design should favor simplicity over cleverness. A straightforward, explicit solution that is easy to reason about is vastly superior to an elaborate, meta-programmed framework.
- **YAGNI:** Never implement speculative features or abstractions based on hypothetical future requirements. Future requirements almost always arrive with different shapes, assumptions, and constraints than anticipated. The code written "just in case" carries ongoing maintenance costs, bugs, and comprehension taxes.

#### The Indirection Tax
Every layer of abstraction (generic base repositories, dynamic reflection dispatchers, custom expression visitors) adds cognitive overhead and debugging friction.
A senior engineer asks: *"Does this abstraction solve an existing, concrete problem, or does it merely flatter our architectural ego?"*

---

### 4.3 Separation of Concerns (SoC) & Single Source of Truth (SSOT)

#### Fundamentals & Internal Mechanics
- **Separation of Concerns:** Distinct concerns (e.g., authorization, data validation, database transactions, domain math, telemetry) must be modularized into independent constructs.
- **Single Source of Truth:** Every distinct state value (e.g., an order balance, a user's subscription status) must have exactly one authoritative storage owner.

In distributed cloud architectures, violating SSOT by caching state in local server memory without synchronization leads to split-brain scenarios and data corruption.

---

### 4.4 Law of Demeter (Principle of Least Knowledge)

#### Fundamentals & Internal Mechanics
> *"Only talk to your immediate friends."*

An object method should invoke only:
1. Methods on itself.
2. Methods on objects passed as method parameters.
3. Methods on objects it instantiates directly.
4. Methods on its own direct instance fields.

It must **never navigate object graphs** (the "Train Wreck" anti-pattern):
```csharp
// VIOLATION: Train wreck navigation
var zipCode = order.GetCustomer().GetPrimaryAddress().GetPostalCode().Value;

// If Customer changes Address to a collection, this line and 40 other files break!

// GOOD: Tell, Don't Ask
var zipCode = order.GetDestinationPostalCode();
```

---

### 4.5 Fail-Fast & Defensive Programming

#### Fundamentals & Internal Mechanics
- **Fail-Fast:** Detect and report an invalid assumption near its source; reject the affected operation before it causes further damage. Invalid client input should not terminate an otherwise healthy service.
- **Defensive Programming:** Anticipating edge cases, network blips, and untrusted inputs by providing robust fallbacks and defensive assertions.

**The Golden Rule:** Be strict and fail-fast at system ingestion boundaries (API endpoints, message queue deserialization). Inside trusted domain models, rely on strict type constructors and invariants rather than cluttering internal business methods with hundreds of redundant `if (x is null)` checks.

---

### 4.6 Principle of Least Astonishment (POLA)

- **Principle of Least Astonishment:** A component, method, or API must behave in a manner that will not surprise a developer using it.
  - Property getters must never trigger expensive database queries or mutate internal state.
  - A method named `FindCustomer()` should not modify the customer's last-active timestamp.

### 4.7 Rule of Three

Wait for enough concrete examples to understand the shared rule before extracting an abstraction. Three is a reminder to gather evidence, not a mandatory threshold. Centralize a critical rounding policy immediately if two copies must always agree; keep three similar workflows separate if they change for unrelated reasons.

**Decision exercise:** Two teams both validate a ten-character reference today. One is a regulated invoice reference; the other is a marketing campaign code. Explain why identical code does not yet establish a shared domain rule, and what evidence would justify extraction later.

---

### Section 4 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How do you determine whether code duplication represents a violation of DRY or an acceptable coincidence?**
> **Strong answer:** Duplication is evaluated by analyzing the rate and reason for change. If two code blocks represent the exact same business rule or core knowledge—such that an update to one without the other would cause system inconsistency—it is a true DRY violation and must be centralized. However, if the code blocks represent distinct business concepts that simply happen to share syntactic structure (such as an API contract DTO and a database persistence entity), deduplicating them creates artificial coupling. When the external API and the database schema inevitably evolve in different directions, that shared abstraction becomes a bottleneck. In such cases, duplication of code is vastly preferable to the wrong abstraction.

**Q2: What is the Law of Demeter, and how does violating it manifest in enterprise .NET applications?**
> **Strong answer:** The Law of Demeter states that a module should not know the inner workings or navigable object graph of the objects it manipulates. In enterprise .NET applications, violations manifest as long dot-chains such as `service.Context.Configuration.ConnectionStrings.Database.Timeout`. This creates tight structural coupling: the calling code is coupled not just to the immediate dependency, but to the entire object hierarchy. If any intermediate class is refactored, the calling code breaks. It also makes unit testing painful, requiring complex mocking of multi-tiered object trees. We resolve this by applying 'Tell, Don't Ask' and pushing behavior into the owning classes.

#### Practical Exercises
1. **Exercise 4.1:** Identify three violations of the Law of Demeter in an existing legacy order-fulfillment handler and refactor them by moving behavior to the root aggregate.
2. **Exercise 4.2:** Write a case study demonstrating an enterprise incident where a speculative generic repository pattern (YAGNI violation) prevented the team from adopting EF Core compiled queries and batch updates.

---

## Section 5 — Coupling: Mechanics, Metrics & Minimization

### 5.1 Dimensions & Architectural Metrics of Coupling

Coupling is the degree of interdependence between software modules.
In Robert C. Martin's package architecture metrics:
- **Afferent Coupling ($C_a$):** The number of classes *outside* this module that depend on classes *inside* this module (incoming dependencies; measures responsibility).
- **Efferent Coupling ($C_e$):** The number of classes *inside* this module that depend on classes *outside* this module (outgoing dependencies; measures instability).

$$\text{Instability } (I) = \frac{C_e}{C_a + C_e}$$
- $I = 0$: Maximally stable. Highly depended upon, depends on nothing else. Hard to change because many consumers rely on it.
- $I = 1$: Maximally instable. Depends on many external modules, no one depends on it. Easy to change.

$$\text{Abstractness } (A) = \frac{\text{Number of Abstract Classes and Interfaces}}{\text{Total Number of Types}}$$

$$\text{Distance from the Main Sequence } (D) = |A + I - 1|$$
- $D\approx 0$: The module balances stability and abstractness perfectly (The Main Sequence).
- The **Zone of Pain** ($A\approx 0, I\approx 0$): Highly concrete, highly stable. Changing this module creates massive change propagation (e.g., a massive concrete utility library used everywhere).
- The **Zone of Uselessness** ($A\approx 1, I\approx 1$): Highly abstract, but nobody depends on it. Pure overhead.

**Interpretation, not a target:** A package with $C_a=8$ and $C_e=2$ has $I=0.2$: many consumers make changes expensive. This says nothing about its runtime reliability or actual change frequency. With no incoming or outgoing dependencies, the ratio is undefined; tools may use a convention. An immutable, widely reused `Money` type can sensibly be concrete and stable. Do not create interfaces solely to improve a metric; inspect change history and dependency direction first.

---

### 5.2 Forms of Coupling

1. **Compile-Time Coupling:** Module A directly references the assembly of Module B. Any interface change in B requires recompilation of A.
2. **Runtime Coupling:** Module A invokes Module B over in-process virtual dispatch, reflection, or HTTP/gRPC.
3. **Control Coupling:** Module A passes a flag, boolean, or enum to Module B to dictate which internal branches Module B executes.
4. **Data Coupling:** Modules share simple primitive data values (ideal, lowest coupling).
5. **Stamp Coupling:** Module A passes an entire complex object (e.g., a 40-field `Customer` entity) to Module B when Module B only requires a single integer `CustomerId`.
6. **Temporal Coupling:** Module A requires that methods on Module B be called in a strict chronological sequence without enforcing this requirement via compile-time types.

---

### 5.3 Temporal Coupling in API Design

#### The Vulnerability
```csharp
// BAD: Severe temporal coupling!
var client = new SmtpEmailClient();
client.SetHost("smtp.sendgrid.net");
client.SetPort(587);
client.Authenticate("user", "pass");
client.Send(message); // What happens if caller calls Send() before Authenticate()? Runtime crash!
```

#### Eliminating Temporal Coupling via Type State / Builder Pattern
```csharp
// GOOD: Invariants enforced by construction and compile-time state transitions
public sealed class SmtpEmailClient
{
    private SmtpEmailClient() { }

    public static async Task<AuthenticatedSmtpSession> ConnectAndAuthenticateAsync(
        string host, int port, NetworkCredential credentials, CancellationToken ct)
    {
        var session = new AuthenticatedSmtpSession(host, port, credentials);
        await session.InitializeAsync(ct);
        return session; // It is physically impossible to possess a session that is unauthenticated!
    }
}

public sealed class AuthenticatedSmtpSession
{
    internal AuthenticatedSmtpSession(string host, int port, NetworkCredential credentials) { /* ... */ }
    public Task SendAsync(MimeMessage message, CancellationToken ct) => /* ... */;
}
```

---

### 5.4 Change Propagation & Circular Dependencies

A circular dependency occurs when Module A depends on Module B, which depends on Module C, which depends on Module A ($A \to B \to C \to A$).
Circular dependencies:
- Prevent independent compilation and deployment.
- Make unit testing impossible in isolation.
- Lead to deadlocks in static constructors and DI container instantiation.

#### Breaking Circular Dependencies
1. **Apply the Dependency Inversion Principle:** Extract an interface into a shared domain contracts layer.
2. **Apply the Mediator / Event-Driven Pattern:** Replace direct synchronous method invocation with an in-process or out-of-process event publish/subscribe mechanism.

---

### 5.5 Techniques for Decoupling: Choose the Dependency You Remove

Decoupling does not mean eliminating all dependencies. It means keeping necessary dependencies explicit while removing knowledge that makes unrelated changes propagate.

| Technique | Dependency reduced | Cost that remains or is introduced |
|---|---|---|
| Consumer-owned port plus adapter | Business code knowing a vendor SDK or persistence implementation | Mapping, contract tests, and adapter maintenance |
| In-process notification | Publisher knowing each reaction directly | Handler ordering, failure propagation, and transaction policy still need decisions |
| Durable asynchronous message | Producer requiring the consumer to be available now | Eventual consistency, duplicate delivery, schema evolution, and operational recovery |
| Smaller input/output contract | Caller and callee sharing a large internal object graph | Translation and explicit versioning at the boundary |

Replacing a method call with an event is not automatically an improvement. If checkout must receive a reservation decision before confirming an order, an explicit call can be easier to reason about. If analytics may lag, a notification can remove an unnecessary availability dependency. Follow messaging reliability details in Module 07 rather than treating an event bus as a correctness mechanism.

**Checkpoint:** Name the compile-time, runtime, and temporal dependencies before and after your proposed change. If you can only say "it uses interfaces now," the analysis is incomplete.

---

### Section 5 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: What is control coupling, and why should it be eliminated in enterprise services?**
> **Strong answer:** Control coupling occurs when one module directs the internal control flow of another by passing control flags, booleans, or mode enums (for example, `ProcessOrder(order, isVip: true, sendEmail: false)`). This tightly couples the consumer to the internal execution branches of the callee and signals an SRP violation. It means the callee is doing multiple distinct things depending on the flag. We eliminate control coupling by decomposing the callee into distinct, cohesive methods (e.g., `ProcessStandardOrder()` and `ProcessVipOrder()`), or by encapsulating the variation behind a Strategy or polymorphic Command pattern.

**Q2: How do you identify and refactor temporal coupling in an existing C# class?**
> **Strong answer:** Temporal coupling is identified when an object requires its methods or properties to be called in an exact sequence (such as calling `.Initialize()` or `.SetCredentials()` before `.Execute()`), but this sequence is not enforced by the compiler. If a caller calls `.Execute()` first, an `InvalidOperationException` or `NullReferenceException` is thrown at runtime. We refactor this by using factory methods, builder patterns with fluent state machines, or constructor injection where all required state must be supplied up front. Once the object reference is obtained, it is guaranteed to be fully initialized and safe to use.

#### Practical Exercises
1. **Exercise 5.1:** Measure afferent and efferent coupling across your solution's core projects using .NET architecture analyzers or NDepend/NetArchTest.
2. **Exercise 5.2:** Refactor an insecure multi-step onboarding wizard class suffering from temporal coupling into a compile-time type-state pipeline.

---

## Section 6 — Cohesion: Class, Module & Architectural Boundaries

### 6.1 The Spectrum of Cohesion

Cohesion measures how closely related the responsibilities of a single module, class, or package are.
Ranked from worst to best:

1. **Coincidental Cohesion (Worst):** Elements are bundled arbitrarily with no meaningful relationship (e.g., `GeneralHelper`, `CommonUtils`).
2. **Logical Cohesion:** Elements perform operations of the same logical category, but differ completely in mechanics (e.g., a `PrinterManager` with methods to print PDFs, print plain text, and send raw thermal printer ESC/POS bytes).
3. **Temporal Cohesion:** Elements are executed at the same point in time, but have nothing else in common (e.g., `StartupService` that initializes database connections, logs audit events, and checks for license key expiration).
4. **Procedural Cohesion:** Elements execute in a specific order to accomplish a process, but operate on different data.
5. **Communicational Cohesion:** Elements operate on the exact same input data, but perform independent, unrelated operations (e.g., `CustomerAnalyzer` that calculates credit scores and renders profile avatars).
6. **Sequential Cohesion:** The output of one operation serves as the input to the next operation (pipeline/assembly line).
7. **Functional Cohesion (Best):** Every single member of the class collaborates directly to execute one well-defined, singular business task.

---

### 6.2 Designing for High Functional Cohesion

```csharp
// BAD: Low Coincidental Cohesion
public static class CommonUtils
{
    public static string ToSlug(string title) => /* ... */;
    public static void SendSlackAlert(string msg) => /* ... */;
    public static decimal CalculateVat(decimal amount) => /* ... */;
}

// GOOD: High Functional Cohesion
public sealed class SlugGenerator
{
    public string Generate(string text) => /* Focused string transformation */;
}

public sealed class VatCalculator
{
    public Money Calculate(Money netAmount, VatRate rate) => /* Pure financial computation */;
}
```

---

### 6.3 Module and Package Cohesion: CCP and CRP

- **Common Closure Principle (CCP):** Classes that change together for the same business reasons should be packaged together. If an accounting regulation changes, the updates should touch only one project/assembly, not ripple across ten projects.
- **Common Reuse Principle (CRP):** Classes that are not reused together should not be packaged together. If a consumer only needs your domain math, they should not be forced to take a dependency on your EF Core database provider or Azure SDK.

---

### 6.4 Identifying Misplaced Responsibilities

**Feature envy** appears when a method repeatedly extracts another object's fields to make decisions that belong to that object. A refund handler checking invoice status, paid balance, and every earlier refund is a candidate for an `Invoice.RequestRefund` operation. Move the rule with the state it protects; keep HTTP calls and persistence orchestration outside the invoice.

**Inappropriate intimacy** is broader: two classes rely on each other's private representation or lifecycle. Bidirectional navigation alone is not proof, but a small representation change requiring coordinated edits in both classes is evidence.

Use three questions before moving behavior:
1. Who owns the invariant and has the information to enforce it?
2. Which business change causes this behavior and state to change together?
3. Would moving it introduce I/O or a dependency cycle into an otherwise cohesive type?

**Critical boundary:** Encapsulation protects one in-memory instance, not all concurrent instances of an entity. Two `InventoryItem` objects can each approve the last unit. A database constraint, conditional update, concurrency token, or appropriate lock must enforce the shared-state invariant. Private setters are not transaction isolation; see Module 05 for persistence enforcement.

**When a simple model is enough:** Read-only reporting DTOs and straightforward CRUD screens do not need rich aggregates merely to satisfy an OOP rule. Introduce behavioral models where meaningful invariants or state transitions need an owner.

---

### Section 6 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How do cohesion and coupling relate to each other in enterprise system architecture?**
> **Strong answer:** Cohesion and coupling are dual forces. High cohesion inside a module naturally leads to low coupling between modules. When a class has high functional cohesion, it owns all the state and behavior necessary to fulfill its single responsibility; it does not need to constantly chat with external objects to get work done. Conversely, when cohesion is low—such as in an anemic domain model with separate manager and helper classes—coupling explodes because business logic must reach across multiple objects to orchestrate state mutations. Our goal is always high cohesion within boundaries and low coupling across boundaries.

#### Practical Exercises
1. **Exercise 6.1:** Inspect a legacy `OrderService` in your codebase. Catalog all methods by their cohesion type (e.g., logical, communicational, functional).
2. **Exercise 6.2:** Apply the Common Closure Principle to reorganize a technical-layered solution (`Controllers`, `Services`, `Repositories`) into a feature-sliced modular monolith architecture.

## Section 7 — Abstraction & Encapsulation in Depth

### 7.1 Levels of Abstraction and Contract Stability

An abstraction is a simplified model of an underlying complex reality. In software engineering, abstractions exist in a strict hierarchy:
- **Level 3 (Business Policy):** High-level rules, workflows, orchestration (e.g., `OrderFulfillmentPolicy`).
- **Level 2 (Domain Operations):** Entities, value objects, domain events (e.g., `Order.Confirm()`, `Money`).
- **Level 1 (Application Services & Ports):** Interface contracts (e.g., `IPaymentGateway`, `IOrderRepository`).
- **Level 0 (Technical Mechanisms):** EF Core SQL queries, TCP socket buffers, JSON serialization.

A senior engineer ensures that dependencies flow strictly downward, and that Level 3 business policies never depend directly upon Level 0 mechanisms.

---

### 7.2 Leaky Abstractions: Mechanics and Mitigation

> *"All non-trivial abstractions, to some degree, are leaky."* — Joel Spolsky (The Law of Leaky Abstractions).

An abstraction is **leaky** when the consumer must understand the underlying technical implementation details to use it safely or correctly.

#### The Classic .NET Leaky Abstraction: `IQueryable<T>` across Service Boundaries
Developers often expose `IQueryable<T>` from repositories to avoid writing specific query methods:
```csharp
// BAD: Catastrophic Leaky Abstraction!
public interface IOrderRepository
{
    IQueryable<Order> Query();
}
```
**Why this leaks disastrously:**
1. **Deferred Execution & DbContext Lifetime:** If the caller evaluates the query (`.ToList()`) after the request-scoped `DbContext` has disposed, an `ObjectDisposedException` crashes the app.
2. **Unsupported LINQ-to-Entities Expressions:** The caller can write valid C# expressions (like `Regex.IsMatch` or calling custom C# methods) that compile fine but throw runtime `InvalidOperationException: The LINQ expression could not be translated` when EF Core executes.
3. **N+1 Query Explosions:** Callers inadvertently trigger hundreds of round-trips to the database without realizing it because lazy-loading or missing `.Include()` calls are hidden behind the collection interface.
4. **Transaction Boundary Leakage:** Database locking hints, query timeouts, and isolation semantics bleed into the presentation or application layer.

#### The Encapsulated Solution
Expose explicit, task-focused asynchronous methods that return materialized results or domain aggregates:
```csharp
public interface IOrderRepository
{
    Task<Order?> GetByIdAsync(OrderId id, CancellationToken ct);
    Task<IReadOnlyList<OrderSummaryDto>> GetRecentOrdersForCustomerAsync(CustomerId customerId, int limit, CancellationToken ct);
    Task SaveAsync(Order order, CancellationToken ct);
}
```

---

### 7.3 Over-Abstraction vs Under-Abstraction: The Indirection Tax

#### Fundamentals & Internal Mechanics
Every abstraction introduces a cognitive and runtime **Indirection Tax**. While **under-abstraction** tangles high-level domain policies with low-level I/O mechanics (making unit testing and vendor changes painful), **over-abstraction** buries simple business rules beneath layers of pass-through interfaces, generic base classes, and mapper ceremonies.

#### When Premature Abstraction Hurts Readability & Runtime Performance
1. **Cognitive Fragmentation:** Navigating `Controller -> IOrderFacade -> OrderFacade -> IOrderOrchestrator -> OrderOrchestrator -> IOrderDomainService` where 80% of classes are 5-line pass-through wrappers forces engineers to keep 7 files open to trace a single field assignment.
2. **JIT Devirtualization Barriers:** In .NET, invoking a method on a concrete `sealed` class allows the Tier-1 JIT compiler (and Dynamic PGO in .NET 8/9) to devirtualize and inline the method body directly into the caller. Wrapping every internal helper and value calculator in an interface (`ITaxMultiplierHelper`) forces **Virtual Stub Dispatch (VSD)**. If a call site becomes megamorphic or crosses assembly boundaries without inlining, the CPU suffers indirect branch mispredictions and loses register-allocation optimizations across the call boundary.
3. **Diagnostic & Refactoring Friction:** Stack traces expand by dozens of frames, DI container startup validation slows down, and adding a single parameter to a business workflow requires shotgun surgery across four pass-through interfaces.

| Architectural Symptom | Under-Abstraction | Pragmatic Sweet Spot (Senior Bar) | Over-Abstraction (Indirection Tax) |
|---|---|---|---|
| **I/O & External Volatility** | `new SqlConnection()` & `HttpClient` hardcoded inside domain methods. | Interfaces (`IOrderRepository`, `IPaymentGateway`) at true **architectural seams** (I/O, clock, external vendors). | Interfaces for pure deterministic internal math (`IDecimalRoundingHelper`) and DTOs (`IOrderDto`). |
| **Data Access Layer** | Raw SQL strings scattered in Razor views or Minimal API lambdas. | Encapsulated repository or vertical slice handler using `DbContext` directly as its unit of work. | Generic `IRepository<TEntity>` wrapping `DbSet<T>`, hiding EF Core's change tracker, `AsNoTracking()`, and bulk `ExecuteUpdateAsync()`. |
| **Extension Points** | 400-line `switch` statement modified every week by 4 teams. | Polymorphic Strategy (`IEnumerable<IPricingRule>`) introduced at **proven variation points** (Rule of Three). | Speculative plugin engine with reflection scanning and XML DSL built for a requirement that never changes. |

---

### 7.4 Information Hiding: David Parnas's Criteria (1972)

David Parnas established the true criterion for decomposing systems into modules:
**A module should be designed to hide a secret.**
What secrets should a module hide?
1. **Volatile Business Rules:** Tax formulas, discount tier algorithms.
2. **Data Representation Secrets:** Whether an order's lines are stored in a contiguous array, a linked list, or a document table.
3. **Hardware / Vendor Integration Secrets:** SendGrid API specifics, Stripe payload shapes, Azure Service Bus connection strings.

If a vendor changes its JSON payload format, exactly one adapter class in your infrastructure layer should change. If your domain entities change as a result, your information hiding has failed.

---

### Section 7 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why is exposing `IQueryable<T>` from a domain repository considered an architectural anti-pattern by senior engineers?**
> **Strong answer:** Exposing `IQueryable<T>` completely violates the repository abstraction and breaks encapsulation. The repository pattern exists to encapsulate data access behind a collection-like interface of domain aggregates. When `IQueryable<T>` is returned, database concerns (SQL translation capabilities, indexing requirements, deferred execution, and DbContext lifetimes) leak into the application and presentation layers. It allows calling layers to execute arbitrary, unindexed queries that can degrade database performance, or invoke C# expressions that fail at runtime because the EF Core provider cannot translate them. Repositories should return materialized aggregates (`Task<Order?>`) or specialized read-only DTOs.

#### Practical Exercises
1. **Exercise 7.1:** Audit an existing ASP.NET Core service that returns `IQueryable<T>` to an MVC controller or Minimal API endpoint. Refactor it into a cleanly encapsulated specification or method-based query repository.

---

## Section 8 — Maintainability, Technical Debt & Evolution

### 8.1 Technical Debt Taxonomy: The Debt Quadrant

Martin Fowler categorizes technical debt along two axes: **Intentionality** (Deliberate vs Inadvertent) and **Discipline** (Prudent vs Reckless):

| | Prudent | Reckless |
|---|---|---|
| **Deliberate** | "We must ship by Friday for the conference; we will omit the Redis cache and query SQL directly, tracking the ticket to add caching next sprint." | "We don't have time to write tests or design a domain model; just dump everything in the Controller." |
| **Inadvertent** | "Now that we have processed 10 million transactions, we understand our domain much better and realize our initial aggregate boundaries need refactoring." | "What are design principles? We just write code until it compiles." |

A Senior Software Engineer recognizes that **prudent, deliberate technical debt is a valid strategic tool**, whereas reckless debt is engineering malpractice.

---

### 8.2 Code Smell Catalog & Automated Static Analysis

#### The Five Families of Structural Code Smells
Following Martin Fowler and Kent Beck's refactoring taxonomy, structural code smells fall into five diagnostic families:

| Smell Category | Specific Smells | Enterprise .NET Symptom & Remediation |
|---|---|---|
| **1. Bloaters** | Long Method, Large Class (God Object), Primitive Obsession, Long Parameter List, Data Clumps | Passing `(string street, string city, string zip, string country)` to 12 methods instead of a `PostalAddress` `readonly record struct`; using `decimal` and `string` instead of a strongly-typed `Money` value object. |
| **2. Object-Orientation Abusers** | Switch Statements on Type Codes, Refused Bequest, Temporary Field, Alternative Classes with Different Interfaces | Subclasses inheriting from a base class solely to reuse 2 helper methods while throwing `NotSupportedException` on virtual overrides (Refused Bequest / LSP violation) $\to$ Replace inheritance with composition. |
| **3. Change Preventers** | Divergent Change, Shotgun Surgery, Parallel Inheritance Hierarchies | **Divergent Change:** One class (`OrderService`) is modified for tax rules, SQL tweaks, and email templates (violates SRP). **Shotgun Surgery:** Adding one tax field requires editing 14 files across 6 projects (violates CCP). |
| **4. Dispensables** | Dead Code, Speculative Generality, Redundant Comments, Lazy Class | Interfaces with a single implementation and zero test doubles created "for future flexibility" (Speculative Generality) $\to$ Collapse hierarchy until the Rule of Three applies. |
| **5. Couplers** | Feature Envy, Inappropriate Intimacy, Message Chains, Middle Man | **Feature Envy:** A method in `InvoiceCalculator` accesses 9 properties of `CustomerTier` to compute a discount $\to$ Move the method onto `CustomerTier`. |

#### Enforcing Architectural Hygiene via `.editorconfig` and Roslyn Analyzers
Senior engineers do not rely on human willpower during code reviews to catch nullability bypasses, unused values, or async pitfalls; they fail the CI build deterministically using `.NET SDK AnalysisLevel` and `.editorconfig`:

```ini
# .editorconfig — Enterprise Senior Engineering Baseline
root = true

[*.cs]
# Treat asynchronous and resource-lifecycle bugs as compile-time errors
dotnet_diagnostic.CA2007.severity = none       # No ConfigureAwait(false) noise in ASP.NET Core app code
dotnet_diagnostic.CA2000.severity = error      # Dispose objects before losing scope
dotnet_diagnostic.CA1859.severity = warning    # Use concrete types when possible for improved JIT devirtualization
dotnet_diagnostic.CA1822.severity = warning    # Mark members as static when they do not access instance data
dotnet_diagnostic.CA1068.severity = error      # CancellationToken parameters must come last
dotnet_diagnostic.CS8600.severity = error      # Converting null literal or possible null value to non-nullable type
dotnet_diagnostic.CS8602.severity = error      # Dereference of a possibly null reference
```

---

### 8.3 Safe Refactoring Strategies for Legacy Code (Michael Feathers)

When modifying legacy systems without existing automated test coverage:
1. **Find a Seam:** A seam is a place where you can alter program behavior without editing the source code in place (e.g., an interface, a virtual method, a DI registration).
2. **Write Characterization Tests:** Write automated tests that capture the *current, actual behavior* of the legacy code (including bugs and quirks) to establish a safety net.
3. **Sprout Method / Sprout Class:** Instead of editing a 2,000-line legacy method, write your new feature in a completely separate, clean, unit-tested class, and invoke it via a single-line call from the legacy method.
4. **Wrap Method / Wrap Class:** Wrap the legacy call inside a decorator that handles new pre- and post-conditions (e.g., logging, validation, metrics) without tampering with the internal legacy spaghetti.

---

### 8.4 Extensibility Without Over-Engineering

#### Designing Extension Points Only at Proven Variation Points
True architectural agility comes from keeping code simple and cohesive so that adding an extension point *when the second or third variation arrives* takes 15 minutes—not from littering the codebase with speculative plugin engines on day one.

1. **Identify the Axis of Volatility:** Before introducing an abstraction, ask: *"What concrete force has caused this module to change in the last 6 months?"* If the answer is "nothing," keep it a `sealed` concrete class.
2. **Closed Core, Open Seams:** When variation is proven (e.g., supporting multiple regional tax authorities or fraud rules), define a narrow role interface (`IFraudRule`) and compose instances via constructor-injected `IEnumerable<IFraudRule>` or a Decorator pipeline.

```csharp
public sealed record FraudEvaluationContext(OrderId OrderId, CustomerId CustomerId, Money Amount, string IpCountry);
public readonly record struct FraudVerdict(bool IsApproved, string? RejectionReason = null);

// Narrow extension seam introduced ONLY after multiple fraud rules became a concrete business requirement
public interface IFraudDetectionRule
{
    int PriorityOrder { get; }
    ValueTask<FraudVerdict> EvaluateAsync(FraudEvaluationContext context, CancellationToken ct);
}

public sealed class FraudEvaluationPipeline(IEnumerable<IFraudDetectionRule> rules)
{
    private readonly IFraudDetectionRule[] _orderedRules = [.. rules.OrderBy(r => r.PriorityOrder)];

    public async ValueTask<FraudVerdict> EvaluateAsync(FraudEvaluationContext context, CancellationToken ct)
    {
        foreach (var rule in _orderedRules)
        {
            var verdict = await rule.EvaluateAsync(context, ct);
            if (!verdict.IsApproved)
                return verdict; // Short-circuit immediately on first rule rejection
        }

        return new FraudVerdict(IsApproved: true);
    }
}
```

---

### 8.5 Backwards Compatibility & Versioning in C#

In enterprise libraries and shared NuGet packages:
- **Binary Compatibility:** Existing compiled consumer DLLs can run against the new assembly without recompilation.
- **Source Compatibility:** Existing consumer code recompiles against the new assembly without compile errors.
- **Behavioral Compatibility:** The code compiles and links, but runtime behavior (e.g., ordering, side effects, exception types) remains consistent.

**Breaking Change Warning in C#:**
Adding an optional parameter with a default value (`void Process(int id, bool flag = false)`) is **source compatible**, but **binary incompatible**! The C# compiler bakes the default value `false` directly into the calling assembly's call site IL. If the consumer does not recompile, a `MissingMethodException` crashes the process at runtime!

---

### Section 8 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: How do you introduce automated unit and integration tests into a 5,000-line legacy C# class with zero tests?**
> **Strong answer:** You never attempt a mass rewrite of a 5,000-line legacy class without a safety net. Following Michael Feathers's methodology, the first step is identifying seams where we can intercept execution. We begin by writing characterization tests—black-box integration tests using `WebApplicationFactory` or harness calls that record existing system behavior for a matrix of inputs. Once the behavioral baseline is locked, we avoid modifying the legacy method directly for new features; instead, we use the Sprout or Wrap method to implement new functionality in clean, isolated, fully-tested classes. For existing code, we refactor in tiny, verified steps using automated refactoring tools to extract cohesive units behind interfaces.

#### Practical Exercises
1. **Exercise 8.1:** Take a monolithic 500-line console app with hard-coded `new SqlConnection()` calls, identify two structural seams, and introduce characterization tests without breaking existing output.

---

## Section 9 — Applying Fundamentals to Enterprise .NET Architecture

### 9.1 Dependency Injection in ASP.NET Core: Service Lifetimes & Traps

The built-in .NET DI container (`Microsoft.Extensions.DependencyInjection`) provides three service lifetimes:
1. **Transient (`AddTransient`):** Created every single time they are requested. Ideal for lightweight, stateless utility operations.
2. **Scoped (`AddScoped`):** Created once per logical operation scope (e.g., once per incoming HTTP request in ASP.NET Core). Essential for stateful request contexts like EF Core `DbContext`.
3. **Singleton (`AddSingleton`):** Created once at application startup and shared across all threads and requests throughout the process lifetime. Must be strictly thread-safe.

#### The Captive Dependency Bug (Critical Senior Failure Mode)
A **Captive Dependency** occurs when a service with a longer lifetime captures a service with a shorter lifetime.
For example, injecting a **Scoped** `DbContext` into a **Singleton** background worker or cache manager:
```csharp
// DISASTER: Singleton captures Scoped DbContext!
public sealed class BackgroundMetricsReporter(AppDbContext dbContext) // DbContext is scoped!
{
    // dbContext is now captured forever in a Singleton!
    // Result: The DbContext change tracker grows unbounded, leaking memory.
    // Concurrency crashes: DbContext is NOT thread-safe; concurrent threads will throw InvalidOperationException!
}
```

#### Correct Solution: `IServiceScopeFactory`
```csharp
public sealed class BackgroundMetricsReporter(IServiceScopeFactory scopeFactory)
{
    public async Task ReportMetricsAsync(CancellationToken ct)
    {
        using var scope = scopeFactory.CreateScope();
        var dbContext = scope.ServiceProvider.GetRequiredService<AppDbContext>();

        var count = await dbContext.Orders.CountAsync(ct);
        // Scope ends; DbContext cleanly disposed!
    }
}
```

---

### 9.2 Encapsulating Domain Models in Entity Framework Core

A common senior challenge is keeping domain entities encapsulated (private setters, read-only collections) while allowing EF Core to map and track data without public exposure.

```csharp
public sealed class OrderConfiguration : IEntityTypeConfiguration<Order>
{
    public void Configure(EntityTypeBuilder<Order> builder)
    {
        builder.HasKey(o => o.Id);

        // Convert strongly-typed IDs
        builder.Property(o => o.Id)
               .HasConversion(id => id.Value, value => new OrderId(value));

        // Map private backing fields directly
        builder.Navigation(o => o.Lines)
               .UsePropertyAccessMode(PropertyAccessMode.Field);

        // EF Core 8+ Complex Types for Value Objects
        builder.ComplexProperty(o => o.Total, b =>
        {
            b.Property(m => m.Amount).HasColumnName("TotalAmount").HasPrecision(18, 2);
            b.Property(m => m.Currency).HasColumnName("TotalCurrency").HasMaxLength(3);
        });
    }
}
```

---

### 9.3 Middleware Pipeline Architecture

#### Chain of Responsibility in ASP.NET Core
The ASP.NET Core HTTP pipeline is a canonical implementation of the **Chain of Responsibility** and **Russian Doll (Decorator)** patterns. Each middleware component wraps the next `RequestDelegate` in the pipeline, executing pre-processing logic on the inbound pass, awaiting `next(context)`, and executing post-processing logic on the outbound pass—or **short-circuiting** the pipeline by returning early without invoking `next`.

#### Convention-Based Middleware vs Factory-Activated `IMiddleware`
| Characteristic | Convention-Based Middleware | `IMiddleware` (Factory-Activated) |
|---|---|---|
| **Lifetime** | **Singleton** (instantiated once at host startup). | Determined by DI registration (`Scoped` or `Transient`). |
| **Dependency Injection** | Constructor can only inject `Singleton` services; `Scoped` services must be injected into `InvokeAsync(HttpContext, MyScopedService)`. | Constructor can safely inject `Scoped` services (e.g., `AppDbContext`, `ITenantContext`) directly without captive dependency bugs. |
| **Contract Enforcement** | Duck-typed (`Invoke` / `InvokeAsync` method resolved via reflection at startup). | Strongly-typed compile-time interface `IMiddleware`. |

#### Ambient Context Propagation with `AsyncLocal<T>`
When propagating cross-cutting correlation IDs or tenant identifiers across asynchronous `await` boundaries without polluting every domain method signature, `ThreadLocal<T>` fails because continuations after `await` resume on arbitrary thread-pool threads. `AsyncLocal<T>` stores state inside the CLR's `ExecutionContext`, which flows automatically (copy-on-write) across `Task.Run`, `await`, and child async flows.

```csharp
public sealed record TenantSnapshot(string TenantId, string CorrelationId);

public static class AmbientTenantContext
{
    private static readonly AsyncLocal<TenantSnapshot?> CurrentSnapshot = new();

    public static TenantSnapshot? Current => CurrentSnapshot.Value;

    public static IDisposable BeginScope(TenantSnapshot snapshot)
    {
        var prior = CurrentSnapshot.Value;
        CurrentSnapshot.Value = snapshot;
        return new ScopeResetter(prior);
    }

    private sealed class ScopeResetter(TenantSnapshot? prior) : IDisposable
    {
        public void Dispose() => CurrentSnapshot.Value = prior;
    }
}

public sealed class TenantResolutionMiddleware : IMiddleware
{
    public async Task InvokeAsync(HttpContext context, RequestDelegate next)
    {
        if (!context.Request.Headers.TryGetValue("X-Tenant-Id", out var tenantHeader) ||
            string.IsNullOrWhiteSpace(tenantHeader))
        {
            // Short-circuit pipeline immediately: downstream handlers and DB queries never execute
            context.Response.StatusCode = StatusCodes.Status400BadRequest;
            await context.Response.WriteAsJsonAsync(new ProblemDetails
            {
                Title = "Missing Tenant Identifier",
                Detail = "The X-Tenant-Id header is required for all API requests.",
                Status = StatusCodes.Status400BadRequest
            });
            return;
        }

        var snapshot = new TenantSnapshot(tenantHeader.ToString(), context.TraceIdentifier);
        using (AmbientTenantContext.BeginScope(snapshot))
        {
            await next(context);
        }
    }
}
```

---

### 9.4 Separation of Concerns in Web APIs

#### Minimal APIs vs Controllers & Validation Pipelines
Whether using Minimal APIs (`MapPost` with `IEndpointFilter`) or Controllers, an HTTP endpoint's **sole responsibility** is protocol translation:
1. Bind and validate transport input (via an `IEndpointFilter` or MediatR validation behavior).
2. Dispatch a command/query to the application/domain layer.
3. Translate the `Result<TValue>` into an HTTP status code or **RFC 9457 `ProblemDetails`** payload.

```csharp
public sealed class ValidationEndpointFilter<TRequest>(IValidator<TRequest> validator) : IEndpointFilter
    where TRequest : class
{
    public async ValueTask<object?> InvokeAsync(
        EndpointFilterInvocationContext context,
        EndpointFilterDelegate next)
    {
        var request = context.Arguments.OfType<TRequest>().FirstOrDefault();
        if (request is null)
            return TypedResults.BadRequest();

        var validation = await validator.ValidateAsync(request, context.HttpContext.RequestAborted);
        if (!validation.IsValid)
        {
            return TypedResults.ValidationProblem(validation.ToDictionary());
        }

        return await next(context);
    }
}

public static class OrderProblemMapper
{
    public static IResult ToProblemDetails(Error error, HttpContext httpContext) =>
        TypedResults.Problem(new ProblemDetails
        {
            Type = $"https://api.enterprise.internal/errors/{error.Code}",
            Title = "Domain Rule Violation",
            Detail = error.Message,
            Status = error.Code switch
            {
                "Order.NotFound" => StatusCodes.Status404NotFound,
                "Order.ConcurrentConflict" => StatusCodes.Status409Conflict,
                _ => StatusCodes.Status422UnprocessableEntity
            },
            Instance = httpContext.Request.Path
        });
}
```

---

### 9.5 Enterprise Integration Boundaries

#### Hexagonal Architecture (Ports & Adapters) and the Anti-Corruption Layer (ACL)
When integrating with a legacy ERP or external payment provider whose data model is cryptic, unstable, or anemic, allowing external SDK types (`Stripe.Charge`, `LegacySapInvoiceXml`) to enter your domain model couples your core business logic to third-party volatility.

- **Port (Domain Interface):** Defined inside your Application/Domain project using pure Ubiquitous Language (`ICreditBureauPort`).
- **Adapter + Anti-Corruption Layer (Infrastructure Implementation):** Lives in the Infrastructure project, invokes the external transport, and translates foreign codes, quirks, and error shapes into clean domain value objects.

```csharp
// PORT: Lives in Core Domain — zero awareness of legacy SOAP/XML or vendor quirks
public enum CreditRiskRating { Prime, Standard, HighRisk, Frozen }
public sealed record CreditAssessment(CustomerId CustomerId, CreditRiskRating Rating, Money ApprovedLimit);

public interface ICreditBureauPort
{
    Task<Result<CreditAssessment>> EvaluateCustomerCreditAsync(CustomerId customerId, CancellationToken ct);
}

// EXTERNAL VENDOR DTO: Cryptic legacy Mainframe/SOAP response shape
public sealed record LegacyEquifaxPayload(string CustRef, int RawScoreCode, string? FreezeFlag, long CentsLimit);

// ADAPTER & ANTI-CORRUPTION LAYER (ACL): Lives in Infrastructure — quarantines external ugliness
public sealed class EquifaxAntiCorruptionAdapter(ILegacySoapClient soapClient) : ICreditBureauPort
{
    public async Task<Result<CreditAssessment>> EvaluateCustomerCreditAsync(CustomerId customerId, CancellationToken ct)
    {
        LegacyEquifaxPayload raw = await soapClient.FetchScoreAsync(customerId.Value.ToString("N"), ct);

        if (raw.RawScoreCode == -999)
            return Result<CreditAssessment>.Failure(new Error("CreditBureau.Unavailable", "Upstream mainframe offline."));

        CreditRiskRating rating = (raw.FreezeFlag, raw.RawScoreCode) switch
        {
            ("Y", _) => CreditRiskRating.Frozen,
            (_, >= 740) => CreditRiskRating.Prime,
            (_, >= 620) => CreditRiskRating.Standard,
            _ => CreditRiskRating.HighRisk
        };

        var limit = new Money(raw.CentsLimit / 100m, "USD");
        return Result<CreditAssessment>.Success(new CreditAssessment(customerId, rating, limit));
    }
}
```

---

### Section 9 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: What is a captive dependency in ASP.NET Core, and how do you prevent and diagnose it?**
> **Strong answer:** A captive dependency occurs when a service with a longer lifetime directly consumes a service with a shorter lifetime—most commonly, a Singleton service injecting a Scoped service like EF Core's `DbContext`. Because the Singleton lives for the entire application lifecycle, the captured Scoped dependency is never disposed, leading to severe memory leaks as change trackers accumulate data. More critically, because `DbContext` is not thread-safe, concurrent requests hitting the Singleton will use the same `DbContext` instance concurrently, causing multi-threaded state corruption and `InvalidOperationException`. In development, ASP.NET Core enables `ValidateScopes = true` by default, which throws an exception at host startup if a captive dependency is detected. In production or background hosted services, we resolve this by injecting `IServiceScopeFactory` and creating explicit, short-lived scopes.

#### Practical Exercises
1. **Exercise 9.1:** Configure an ASP.NET Core test host with `ValidateScopes = true`, inject a Scoped repository into a Singleton background worker, verify the startup failure, and refactor it using `IServiceScopeFactory`.

---

## Section 10 — Senior-Level Design Reviews & Interview Scenarios

### 10.1 Systematic Code Review Methodology

A Senior Software Engineer reviews pull requests through a prioritized hierarchy of concerns:
1. **Architecture & Invariants (P0):** Does this break domain boundaries? Can the entity enter an invalid state? Is there a race condition?
2. **Correctness & Reliability (P0):** Are resources deterministically disposed? Are cancellation tokens propagated? Are null checks handled via types?
3. **Performance & Scalability (P1):** Are there N+1 query leaks, captive dependencies, or unindexed database scans?
4. **Maintainability & Clean Code (P2):** Does it follow SLAP? Are names intention-revealing? Are there control coupling flags?
5. **Syntax & Formatting (P3):** Automated away by `.editorconfig` and Roslyn analyzers; never waste review time on formatting debates.

---

### 10.2 Reviewing Flawed Enterprise Code: Complete Walkthrough

Consider this Pull Request submitted by a mid-level engineer:

```csharp
// FLAWED SUBMISSION
public class InvoiceService
{
    private readonly AppDbContext _context;

    public InvoiceService(AppDbContext context)
    {
        _context = context;
    }

    public async Task ProcessInvoice(Guid invoiceId, bool isUrgent = false)
    {
        var invoice = _context.Invoices.Include(i => i.Lines).FirstOrDefault(i => i.Id == invoiceId);
        if (invoice == null)
        {
            throw new Exception("Not found");
        }

        if (invoice.Status == "Draft")
        {
            decimal total = 0;
            foreach (var line in invoice.Lines)
            {
                total += line.Price * line.Quantity;
            }
            invoice.Total = total;

            if (isUrgent)
            {
                invoice.Priority = 1;
                var client = new HttpClient();
                await client.PostAsync("https://sms.internal/urgent", new StringContent("Urgent Invoice " + invoice.Id));
            }

            invoice.Status = "Processed";
            await _context.SaveChangesAsync();
        }
    }
}
```

#### Senior Code Review Feedback:
1. **P0 (Concurrency & Correctness):** Instantiating `new HttpClient()` in a method causes socket exhaustion under high load. Inject `IHttpClientFactory`.
2. **P0 (Encapsulation):** `Invoice` is an anemic domain model with magic strings (`"Draft"`, `"Processed"`). Business logic for calculating totals and updating status should reside inside an encapsulated `Invoice.Process()` method.
3. **P1 (Control Coupling):** The parameter `bool isUrgent = false` is control coupling. Split into dedicated business flows or command handlers.
4. **P1 (Reliability):** Generic `throw new Exception("Not found")` hides errors. Use a typed domain exception or `Result<T>` pattern.
5. **P1 (Async & Cancellation):** Missing `CancellationToken ct` parameter propagation across all asynchronous database and HTTP calls.

---

### 10.3 Defending Architectural Trade-Offs

#### Structuring Senior Interview Responses: Context $\to$ Forces $\to$ Decision $\to$ Trade-offs
In senior and staff interviews, there are no universally "correct" architectures—only trade-offs aligned with specific business constraints. When defending a design decision, structure your answer around four pillars:
1. **Context & Scale:** Quantify throughput, team topology, regulatory constraints, and SLA targets (e.g., "200 RPS peak, strict PCI-DSS auditability, 6-engineer team").
2. **Competing Design Forces:** State the tension explicitly (e.g., "Immediate transactional consistency vs cross-service availability during downstream ERP maintenance windows").
3. **The Chosen Architecture & Why Alternatives Were Rejected:** Explain why a Modular Monolith with an transactional Outbox beat a premature 12-microservice mesh for a 6-person team.
4. **Accepted Downsides & Mitigation:** Acknowledge what your design sacrifices and how you monitor or bound that risk.

### 10.4 Refactoring Legacy Systems: Strangler Fig & Branch by Abstraction
Never propose a "Big Bang" 12-month freeze-and-rewrite of a revenue-generating production system. Instead, migrate incrementally in production using the **Strangler Fig Pattern**:

1. **Introduce an Abstraction Seam (Proxy / Router / `IFulfillmentEngine`):** Place an interception point in front of the legacy subsystem.
2. **Dark Launching & Shadow Traffic (Verification Phase):** Execute the new refactored domain logic in parallel with the legacy path (in a fire-and-forget shadow background task), comparing the outputs of `LegacyEngine` and `ModernEngine` and logging discrepancies to telemetry without affecting user responses.
3. **Canary Rollout via Feature Flags:** Route 1% $\to$ 10% $\to$ 50% $\to$ 100% of live traffic (by `TenantId` or `OrderId` hash) to `ModernEngine`, with an instant kill-switch fallback to `LegacyEngine` if error rates spike.
4. **Expand-and-Contract Database Schema Migration:**
   - *Expand:* Add nullable new columns/tables alongside legacy columns; deploy dual-write code that populates both.
   - *Backfill:* Migrate historical rows in idempotent background batches.
   - *Switch Reads:* Point application reads to the new schema.
   - *Contract:* Remove legacy writes and drop obsolete columns in a subsequent release.

---

### 10.5 Comprehensive Assessment & Capstone

You are asked in an interview:
> *"We have an enterprise e-commerce platform processing 10,000 orders an hour. During flash sales, the inventory service frequently allows products to oversell. The legacy codebase uses a monolithic `OrderService` that updates stock balances directly in a SQL transaction with no optimistic locking. Walk us through how you would diagnose the failure, redesign the domain model, and refactor the architecture safely."*

#### Senior Model Response Strategy:
1. **Diagnose the Root Cause:** Identify the race condition: read-modify-write without row versioning or pessimistic locking (`SELECT stock` followed by `UPDATE stock`). Under concurrency, multiple threads read the same stock balance simultaneously.
2. **Domain Boundary Redesign:** Encapsulate `InventoryItem` as an aggregate root with an invariant: `DeductStock(int quantity)` throws if quantity exceeds available stock.
3. **Concurrency Control:** Implement optimistic concurrency control via a `RowVersion` / concurrency token in EF Core, or use an atomic SQL increment statement (`UPDATE Inventory SET Stock = Stock - @qty WHERE Id = @id AND Stock >= @qty`).
4. **Architectural Decoupling:** Decouple order placement from immediate inventory fulfillment using an asynchronous reservation pattern backed by messaging (Outbox pattern).

---

### Section 10 Review: Interview Questions & Practice Exercises

#### Realistic Interview Questions & Strong Model Answers

**Q1: Why did instantiating `new HttpClient()` inside `InvoiceService.ProcessInvoice()` receive a P0 blocker severity in the code review?**
> **Strong answer:** Although `HttpClient` implements `IDisposable`, disposing or re-instantiating it per request creates a new underlying `HttpMessageHandler` and TCP socket connection every time. When disposed, OS sockets do not close immediately; they remain in the `TIME_WAIT` state for up to 240 seconds to catch delayed packets. Under bursty enterprise traffic, this rapidly exhausts the ephemeral TCP port pool on the host machine, throwing `SocketException` across the entire process. Additionally, a single static `HttpClient` without handler rotation ignores DNS TTL changes. The production fix is injecting `IHttpClientFactory` (or a typed `HttpClient`), which pools and rotates `SocketsHttpHandler` instances safely while respecting DNS updates.

**Q2: How do you convince product management to invest engineering sprints in refactoring an anemic, tightly coupled legacy module when "it currently works"?**
> **Strong answer:** Avoid pitching refactoring in abstract technical terms like 'SOLID compliance' or 'code aesthetics.' Frame technical debt using Martin Fowler's interest-vs-principal model tied directly to business delivery metrics: lead time for changes, change failure rate (production incidents), and onboarding velocity. Show concrete evidence—for instance, that adding a new payment method took 3 weeks instead of 2 days due to shotgun surgery across 18 files and caused two regression outages. Then propose an incremental Strangler Fig or Sprout Class strategy folded into upcoming feature work on that module, guaranteeing zero feature freeze and measurable defect reduction.

**Q3: During a Strangler Fig migration, how do you verify that your newly refactored domain service produces identical financial calculations to a 10-year-old legacy stored procedure before switching live traffic?**
> **Strong answer:** We use **Branch by Abstraction** combined with a **Shadow / Dark-Read Comparison Harness**. The legacy stored procedure remains the authoritative source of truth that returns the response to the caller and commits state. Concurrently, we capture an immutable snapshot of the input request and run the new C# domain model in an isolated, read-only shadow execution path (guarded by a timeout and exception bulkhead so shadow failures never impact production). A comparison telemetry sink diffs the legacy output against the new domain output—checking line-item rounding, tax edge cases, and currency conversions—and emits structured mismatch events. Only after millions of production shadow executions achieve 100% parity do we flip the feature flag to cut over live writes.

#### Practical Exercises
1. **Exercise 10.1:** Take the flawed `InvoiceService` from Section 10.2 and write the complete, production-ready refactored solution: an encapsulated `Invoice` aggregate root, an `InvoiceId` strong ID, an `IUrgentNotificationPort` adapter using `HttpClient`, and a unit-tested application handler.
2. **Exercise 10.2:** Design and implement a generic `ShadowParityVerifier<TInput, TOutput>` decorator in C# that executes a primary legacy delegate and a secondary candidate delegate concurrently, logs structural differences via `ILogger`, and guarantees that exceptions or slowdowns in the candidate path never delay or fail the primary response.
3. **Exercise 10.3:** Write a 4-stage Expand-and-Contract migration plan (with C# entity states and SQL steps) to split a single `Customer.FullName` column into `GivenName` and `FamilyName` across a live zero-downtime ASP.NET Core deployment.

---

# Part III — Interview Readiness

## 1. Mid-Level vs Senior-Level Answer Patterns

| Topic | Mid-Level Candidate Response | Senior / Staff-Level Candidate Response |
|---|---|---|
| **Encapsulation** | "Encapsulation means making fields private and exposing them through public getters and setters." | "Encapsulation is invariant protection and information hiding. It bundles state with business rules to guarantee that an object can never enter an invalid state, hiding volatile internal data structures behind meaningful domain operations." |
| **Liskov Substitution Principle** | "LSP means a subclass should be able to replace its parent class without breaking compilation." | "LSP defines behavioral subtyping: a subtype cannot strengthen preconditions, weaken postconditions, or violate base invariants. If calling an inherited method throws an unexpected exception like `NotSupportedException`, it violates LSP." |
| **DRY Principle** | "Never copy and paste code. If two methods look similar, create a shared base class or utility method." | "DRY is about single representations of business knowledge, not syntactic code duplication. Prematurely unifying code from two different business domains creates tight coupling and makes future independent evolution painful." |
| **Dependency Inversion (DIP)** | "DIP means you should register all your classes with an IoC container and inject interfaces." | "DIP is an architectural boundary rule stating that high-level business policies must not depend on low-level technical mechanisms; both must depend on abstractions. DI is simply one concrete pattern used to fulfill DIP." |
| **Coupling & Cohesion** | "Coupling is bad, cohesion is good." | "Coupling measures external interdependence, while cohesion measures internal alignment of purpose. We optimize for high functional cohesion within boundaries to naturally minimize efferent coupling across module boundaries." |
| **`IQueryable<T>` in Repositories** | "It's great because it gives callers flexibility to filter and sort however they want." | "It is an architectural anti-pattern and a severe leaky abstraction. It leaks SQL provider translation details, DbContext lifetime requirements, and transaction boundaries into calling layers, causing N+1 queries and runtime translation crashes." |
| **Error Handling** | "Wrap every method in `try/catch` and throw custom exceptions for invalid business inputs." | "Reserve exceptions for truly exceptional, unrecoverable system events. For predictable business validation failures, use typed `Result<T, TError>` objects to enforce compile-time handling and avoid expensive stack unwinding." |

---

## 2. Rapid-Fire Revision Sheet (50 Senior-Level Truths)

1. Classes are reference types whose metadata resides in the CLR `MethodTable`; objects are heap instances with an Object Header (8 bytes) and MethodTable pointer (8 bytes).
2. Value types stored as fields within a class instance live on the managed heap inside that class object's memory buffer.
3. Positional `record class` types generate shallowly immutable `init`-only properties by default.
4. Positional `record struct` types generate **mutable** properties unless explicitly declared as `readonly record struct`.
5. Standard structs do **not** provide `operator ==` or `operator !=` by default; they must be explicitly declared or inherited via `record struct`.
6. `ValueType.Equals` uses reflection to compare fields if the struct contains reference types or alignment padding, degrading performance unless overridden.
7. Casting a struct to an interface causes the runtime to allocate a heap box object.
8. Virtual method dispatch indexes into a fixed Vtable slot; interface dispatch utilizes Virtual Stub Dispatch (VSD) with a three-tiered cache.
9. Marking classes `sealed` enables the JIT compiler to devirtualize method calls, converting indirect calls into direct static calls or inlining them.
10. Default Interface Methods (DIM) cannot be invoked directly on an instance of a concrete class; they require an interface reference cast.
11. Garbage Collection reclaims managed heap memory; it does not deterministically close unmanaged file handles, database connections, or socket buffers.
12. If two objects are equal according to `Equals()`, their `GetHashCode()` **must** return the exact same integer value.
13. Mutating an object while it serves as a key in a `Dictionary<TKey, TValue>` permanently breaks lookup capability for that key.
14. The Single Responsibility Principle governs cohesion relative to business actors, not method line counts.
15. Open/Closed Principle encourages extension via polymorphism, decorators, and pipelines rather than editing tested legacy code.
16. The Liskov Substitution Principle mandates that subtypes cannot strengthen preconditions or weaken postconditions.
17. The classic `Square` inheriting from `Rectangle` violates LSP because setting `Width` mutates `Height`, breaking caller invariants.
18. Interface Segregation Principle mandates role interfaces over monolithic header interfaces.
19. Dependency Inversion Principle dictates that compile-time dependencies point toward business policies, not persistence tools.
20. Single Level of Abstraction Principle (SLAP) demands that a method's statements operate at the exact same conceptual level.
21. Command-Query Separation (CQS) states that methods either mutate state (Command) or return data (Query), never both.
22. Deep `if/else` nesting (the Arrow Anti-pattern) should be refactored into early-return guard clauses.
23. Exceptions should never be used for standard control flow or expected domain validation errors due to stack-unwinding overhead.
24. The `Result<TValue, TError>` pattern turns expected domain failure modes into explicit, typed return values.
25. DRY applies to duplication of domain knowledge, not coincidental structural similarities between unrelated models.
26. YAGNI asserts that speculative code written "for the future" costs more in maintenance and cognitive load than writing it when needed.
27. The Law of Demeter forbids navigating object graphs (`a.B.C.D()`); use 'Tell, Don't Ask' instead.
28. Fail-Fast means detecting and reporting illegal states immediately at system boundaries rather than silently propagating errors.
29. Afferent Coupling ($C_a$) measures incoming dependencies; Efferent Coupling ($C_e$) measures outgoing dependencies.
30. Instability ($I$) is calculated as $C_e / (C_a + C_e)$; a package with $I=0$ is maximally stable.
31. The "Zone of Pain" contains highly concrete, highly stable modules that are painfully difficult to modify.
32. Stamp Coupling occurs when a method accepts a massive composite object when it only needs one primitive property.
33. Control Coupling occurs when a caller passes a boolean or enum flag to dictate internal branching logic in a callee.
34. Temporal Coupling exists when methods must be called in a secret chronological order not enforced by the compiler.
35. Factory methods and state-machine builders eliminate temporal coupling by enforcing complete initialization upon construction.
36. Circular dependencies prevent independent deployment, complicate testing, and risk static initialization deadlocks.
37. Functional Cohesion is the highest form of cohesion: every member participates directly in a single business task.
38. Coincidental Cohesion is the lowest form of cohesion: unrelated utilities grouped arbitrarily in a `Common` class.
39. The Common Closure Principle (CCP) states that classes that change together should be packaged together.
40. The Common Reuse Principle (CRP) states that classes not reused together should not be packaged together.
41. An abstraction is leaky when callers must understand internal implementation details to use it correctly.
42. Exposing `IQueryable<T>` outside of repositories leaks EF Core SQL translation limitations and DbContext lifetimes.
43. David Parnas defined modularization as information hiding: designing modules to hide volatile technical secrets.
44. Prudent, deliberate technical debt is a legitimate business trade-off; reckless debt is engineering negligence.
45. Michael Feathers defines legacy code simply as code without automated characterization tests.
46. A "seam" is a place where software behavior can be altered without editing the source code directly.
47. Adding an optional parameter with a default value in C# is source-compatible but binary-incompatible.
48. In ASP.NET Core DI, a Captive Dependency occurs when a Singleton captures a Scoped service, leading to memory leaks and race conditions.
49. EF Core 8+ complex types allow mapping rich value objects to database columns without public setters.
50. High-level code reviews prioritize architectural boundaries, domain invariants, concurrency safety, and performance over formatting syntax.

---

## 3. Self-Assessment Rubric

| Dimension | Needs Work (Junior) | Developing (Mid-Level) | Senior-Ready | Strong Senior / Staff-Level |
|---|---|---|---|---|
| **OOP Mechanics** | Confuses classes with objects; claims all structs are on the stack. | Understands value vs reference semantics; implements basic encapsulation. | Deeply understands CLR dispatch (Vtable vs VSD), boxing costs, memory layouts, and invariant enforcement. | Designs zero-allocation type architectures; leverages devirtualization, memory safety, and immutable data flows. |
| **SOLID Application** | Treats SOLID as a checklist; creates an interface for every single class. | Applies SOLID principles in familiar scenarios; catches obvious God classes. | Identifies subtle LSP and ISP violations; critiques premature abstraction; applies DIP at architectural boundaries. | Balances SOLID against cognitive load; articulates when violating a principle is the superior pragmatic choice. |
| **Clean Code & Invariants** | Writes deeply nested procedural code with magic strings and public setters. | Uses meaningful names; flattens control flow with guard clauses. | Enforces SLAP and CQS rigorously; eliminates anemic domain models; replaces exceptions with Result patterns on hot paths. | Mentors teams in domain expressiveness; establishes ubiquitous language; designs self-documenting architectures. |
| **Coupling & Cohesion** | Unaware of coupling types; creates circular dependencies without noticing. | Separates concerns into technical layers (Controller-Service-Repo). | Calculates instability and abstractness metrics; eliminates temporal and control coupling; designs for functional cohesion. | Aligns packaging with business domains using CCP/CRP; establishes Anti-Corruption Layers across enterprise systems. |
| **Enterprise Architecture** | Introduces captive dependencies; returns `IQueryable<T>` from repositories. | Configures standard ASP.NET Core DI lifetimes; maps entities with EF Core. | Prevents captive dependencies; encapsulates domain models inside EF Core; diagnoses subtle multi-threaded race conditions. | Designs resilient, scalable cloud architectures; formulates legacy refactoring roadmaps with automated characterization seams. |

---

# Part IV — References

1. **Microsoft Learn C# Documentation:**
   - [Structure of Value Types and Reference Types](https://learn.microsoft.com/dotnet/csharp/language-reference/builtin-types/value-types)
   - [Records and Value Equality in C#](https://learn.microsoft.com/dotnet/csharp/fundamentals/types/records)
   - [Dependency Injection in ASP.NET Core](https://learn.microsoft.com/aspnet/core/fundamentals/dependency-injection)
   - [Entity Framework Core In-Depth Mapping & Value Objects](https://learn.microsoft.com/ef/core/modeling/)
2. **Foundational Books & Papers:**
   - Martin, Robert C. *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall, 2017.
   - Martin, Robert C. *Agile Software Development, Principles, Patterns, and Practices*. Pearson, 2002.
   - Fowler, Martin. *Refactoring: Improving the Design of Existing Code* (2nd ed.). Addison-Wesley, 2018.
   - Feathers, Michael. *Working Effectively with Legacy Code*. Prentice Hall, 2004.
   - Ousterhout, John. *A Philosophy of Software Design* (2nd ed.). Yaknyam Press, 2021.
   - Liskov, Barbara; Wing, Jeannette. "A Behavioral Notion of Subtyping". *ACM Transactions on Programming Languages and Systems (TOPLAS)*, 1994.
   - Parnas, David L. "On the Criteria To Be Used in Decomposing Systems into Modules". *Communications of the ACM*, 1972.
   - Spolsky, Joel. "The Law of Leaky Abstractions". *Joel on Software*, 2002.
