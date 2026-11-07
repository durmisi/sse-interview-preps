# Module 04 — Design Patterns & Code Organization

**Senior Software Engineer Academy · Module 04 of 12**

> **Learning objective:** Master the pragmatic application, critique, and rejection of classic Gang of Four (GoF) and enterprise software design patterns. Develop the engineering discipline to organize enterprise .NET codebases using Dependency Injection as an architectural foundation, in-process CQRS pipelines, Clean Architecture, Vertical Slice Architecture, and Modular Monolith boundaries. Learn to defend architectural choices against over-engineering and premature abstraction in senior and staff technical interviews.
>
> **Audience:** Experienced C#/.NET engineers preparing for senior technical interviews and architectural design reviews. Real-world enterprise systems experience is assumed; patterns are evaluated for their concrete maintenance costs, runtime allocations, and cognitive load.
>
> **Version note:** Code examples target modern .NET (.NET 8 LTS and .NET 9) with C# 12/13. Features include keyed services (`[FromKeyedServices]`), `AddOptionsWithValidateOnStart`, options-validation source generators, `System.Threading.Lock` (.NET 9), primary constructors, and NetArchTest architecture rules.

## How to use this module

Every section in Part II provides comprehensive senior-level instruction:
1. **Intent & Design Forces:** The exact structural problem the pattern solves and the forces it balances.
2. **C#/.NET Production Implementation:** Idiomatic, nullable-aware implementations in realistic domains (orders, billing, tenants, notifications).
3. **Where .NET Uses It:** Concrete examples of the pattern embedded within the .NET BCL or ASP.NET Core framework.
4. **Trade-offs, Alternatives & Failure Modes:** When the pattern introduces needless indirection and should be deliberately rejected.
5. **What a Senior Engineer Is Expected to Know:** Mid-level vs Senior/Staff design judgment.
6. **Interview Questions with Model Answers:** Real interview questions with structured, senior-level responses.
7. **Practical Exercises:** Refactoring challenges and architecture design drills.

## Progress tracker

| Section | Topic | Status |
|---|---|---|
| Section 1 | Pattern Philosophy, Forces & Anti-Patterns | Complete |
| Section 2 | Creational Patterns (Factory, Builder, Singleton, Object Pool) | Complete |
| Section 3 | Structural Patterns (Adapter, Decorator, Facade, Composite, Proxy) | Complete |
| Section 4 | Behavioral Patterns (Strategy, Chain of Responsibility, Command, Mediator, State) | Complete |
| Section 5 | Dependency Injection as an Architectural Discipline | Complete |
| Section 6 | Enterprise Application Patterns (Repository, Unit of Work, Result, Specification) | Complete |
| Section 7 | In-Process CQRS & MediatR Pipeline Architecture | Complete |
| Section 8 | Clean, Onion & Hexagonal (Ports & Adapters) Architecture | Complete |
| Section 9 | Vertical Slice Architecture & Feature-Driven Design | Complete |
| Section 10 | Modular Monolith Architecture & Boundary Enforcement | Complete |
| Section 11 | Functional Design Patterns in Modern C# | Complete |
| Section 12 | Senior Scenarios, Codebase Refactoring & Capstone | Complete |

**Current position:** Full curriculum complete. Ready for self-study, exercises, and interview drills.

## Module boundaries

- **This module owns:** Gang of Four design patterns, in-process architectural patterns (CQRS, MediatR), codebase organization (Clean Architecture, Vertical Slice, Modular Monolith), DI container patterns, and NetArchTest boundary validation.
- **Related topics owned by other modules:**
  - Object-oriented mechanics, SOLID principles, and coupling/cohesion theory → Module 01
  - Data structure performance and algorithmic complexity → Module 02
  - CoreCLR runtime memory layouts, GC internals, and DI scope lifetimes → Module 03
  - Relational and NoSQL persistence patterns, EF Core DbContext mapping → Module 05
  - API protocol design, REST, gRPC, and OAuth2/OIDC → Module 06
  - Distributed systems patterns (Saga, Outbox, Event Sourcing, Event-driven architecture) → Module 07
  - Strategic Domain-Driven Design (Bounded Contexts) and high-level system design → Module 08

---

# Part I — Complete Curriculum

## Section 1 — Pattern Philosophy, Forces & Anti-Patterns
- 1.1 The Anatomy of a Pattern: Intent, Motivation, Structure, Participants, Collaborations, and Consequences.
- 1.2 Pattern Literacy vs Pattern Abuse: The "Golden Hammer" anti-pattern; when patterns become resume-driven development.
- 1.3 The Cost of Indirection: Evaluating code navigation overhead, stack trace complexity, and maintenance taxes.

## Section 2 — Creational Patterns
- 2.1 Factory Method & Abstract Factory: Decoupling creation from usage; family of products; DI container registration alternatives.
- 2.2 Builder Pattern: Step-by-step construction of complex invariant-heavy aggregates; fluent interfaces; `IHttpClientFactory` and `WebApplicationBuilder`.
- 2.3 Singleton Pattern vs DI Singleton: Classic GoF static singleton anti-pattern vs container-managed singletons; thread safety, testability, and state leakage.
- 2.4 Prototype & Object Pool: `ICloneable` pitfalls; deep vs shallow cloning; `Microsoft.Extensions.ObjectPool` for high-throughput buffer reuse.

## Section 3 — Structural Patterns
- 3.1 Adapter Pattern: Reconciling incompatible interfaces; integrating third-party SDKs; Anti-Corruption Layers (ACL).
- 3.2 Decorator Pattern: Adding behavior dynamically without subclassing; caching, logging, metrics, retry decorators; assembly scanning via Scrutor.
- 3.3 Facade Pattern: Providing a unified high-level interface to a complex subsystem; preventing leaky subsystem abstractions.
- 3.4 Composite Pattern: Tree structures where individual objects and compositions of objects share a uniform interface; UI trees, organizational hierarchies.
- 3.5 Proxy Pattern: Controlling access to an object; virtual proxies (lazy loading), protection proxies (authorization), and remote proxies (gRPC stubs).

## Section 4 — Behavioral Patterns
- 4.1 Strategy Pattern: Encapsulating interchangeable algorithms; avoiding `switch` statements; dictionary-based strategy resolution.
- 4.2 Chain of Responsibility: Passing requests along a handler chain; ASP.NET Core middleware pipeline; cancellation and short-circuiting.
- 4.3 Command Pattern: Encapsulating requests as standalone objects; undo/redo, command queuing, audit logging.
- 4.4 Mediator Pattern: Decoupling many-to-many communication; in-process MediatR; when Mediator hides true architectural coupling.
- 4.5 State Pattern: Encapsulating state-dependent behavior; finite state machines; eliminating nested conditionals in order lifecycles.
- 4.6 Specification Pattern: Encapsulating business rules and query predicates for reuse in both memory and EF Core query translation.

## Section 5 — Dependency Injection as an Architectural Discipline
- 5.1 The Composition Root: Bootstrapping application graphs in `Program.cs`; avoiding Service Locator anti-patterns (`IServiceProvider.GetService()`).
- 5.2 Keyed Services (.NET 8+): Registering and resolving multiple named implementations (`AddKeyedScoped`, `[FromKeyedServices]`).
- 5.3 The Options Pattern: `IOptions<T>`, `IOptionsSnapshot<T>`, `IOptionsMonitor<T>`; configuration binding with `ValidateOnStart` and source generators.
- 5.4 Decoration with Scrutor: Fluent automatic decoration (`services.Decorate<IOrderService, CachedOrderService>()`).

## Section 6 — Enterprise Application Patterns
- 6.1 Repository & Unit of Work Debate: Is the generic repository pattern redundant over EF Core's `DbSet` and `DbContext`? When specialized repositories are justified.
- 6.2 The Result Pattern: Replacing business exceptions with strongly-typed `Result<TValue, TError>` structures; railway-oriented programming.
- 6.3 Domain Events: In-process notification of state changes; aggregate root event recording; dispatching before vs after transaction commit.

## Section 7 — In-Process CQRS & MediatR Pipeline Architecture
- 7.1 Command Query Responsibility Segregation (CQRS) In-Process: Separating write operations (mutations) from read operations (DTO projections).
- 7.2 MediatR Pipeline Behaviors: `IPipelineBehavior<TRequest, TResponse>` for cross-cutting concerns (logging, validation with FluentValidation, transactions).
- 7.3 The Critique of MediatR: When MediatR creates unnecessary indirection, hides dependencies, and makes static analysis impossible.

## Section 8 — Clean, Onion & Hexagonal (Ports & Adapters) Architecture
- 8.1 The Dependency Rule: Source code dependencies must point inward toward higher-level domain policies.
- 8.2 Architectural Layers: Domain Core -> Application Services -> Infrastructure -> Presentation.
- 8.3 Ports and Adapters: Defining ports as interfaces in the application layer; implementing adapters in the infrastructure layer.

## Section 9 — Vertical Slice Architecture & Feature-Driven Design
- 9.1 Decomposing by Feature vs Technical Layer: Why traditional layered architectures suffer from high friction during changes.
- 9.2 Vertical Slice Structure: Grouping commands, queries, validators, DTOs, and endpoints into cohesive feature folders.
- 9.3 Sizing Slices: Balancing code reuse against feature autonomy; when sharing a domain model is necessary vs when duplication is preferred.

## Section 10 — Modular Monolith Architecture & Boundary Enforcement
- 10.1 Monolith vs Microservices: Why modular monoliths are often the ideal architecture for enterprise systems.
- 10.2 Module Boundaries & Public Contracts: Designing explicit module contracts; using C# `internal` and `[InternalsVisibleTo]`.
- 10.3 Automated Architectural Testing: Enforcing layering rules and preventing illegal dependencies with NetArchTest / ArchUnitNET.

## Section 11 — Functional Design Patterns in Modern C#
- 11.1 Immutability & Expressions: `record class`, `readonly record struct`, non-destructive mutation via `with` expressions.
- 11.2 Discriminated Unions & Pattern Matching: Exhaustive pattern matching; modeling domain outcomes with `OneOf<T0, T1, T2>`.
- 11.3 Monadic Pipelines: Composing operations with `Bind`, `Map`, and `Tap` extension methods.

## Section 12 — Senior Scenarios, Codebase Refactoring & Capstone
- 12.1 Refactoring an Over-Engineered Codebase: Identifying and removing useless abstractions, excessive repositories, and redundant layers.
- 12.2 Architectural Decision Defense: Presenting and justifying the choice between Clean Architecture and Vertical Slice to stakeholders.
- 12.3 Capstone Walkthrough: Complete design and implementation of a high-throughput, multi-tenant billing engine with modular slices.

---

# Part II — Lessons

## Section 1 — Pattern Philosophy, Forces & Anti-Patterns

### 1.1 The Anatomy of a Pattern and Pattern Literacy

A software design pattern is not a copy-paste code template; it is a **documented solution to a recurring design problem within a specific context**, balancing competing forces.
Every pattern consists of:
1. **Context:** The environment and architectural constraints where the problem occurs.
2. **Forces:** The trade-offs that pull the design in opposing directions (e.g., extensibility vs simplicity, runtime speed vs memory footprint).
3. **Solution:** The structural relationships and collaborating roles that resolve the forces.
4. **Consequences:** The new costs, overheads, and trade-offs introduced by applying the pattern.

#### The Golden Hammer Anti-Pattern
Mid-level engineers who have just learned design patterns often suffer from the "Golden Hammer" cognitive bias: treating every problem as an opportunity to apply an Abstract Factory or Mediator.
*Senior Engineering Rule:* **Do not introduce a design pattern unless you can articulate the exact design force it balances and the exact maintenance cost it imposes.**

---

### 1.2 Pattern Over-Engineering, YAGNI & GoF Taxonomy

#### The Classic Gang of Four (GoF) Taxonomy
In *Design Patterns: Elements of Reusable Object-Oriented Software* (1994), the 23 foundational patterns are classified across two orthogonal axes: **Purpose** (what a pattern does) and **Scope** (whether the pattern applies primarily to compile-time class inheritance or runtime object composition).

| Purpose | Class Scope (Compile-Time Inheritance) | Object Scope (Runtime Composition & Delegation) |
|---|---|---|
| **Creational** *(Decoupling object instantiation)* | Factory Method | Abstract Factory, Builder, Prototype, Singleton (+ modern Object Pool) |
| **Structural** *(Composing larger topologies)* | Adapter *(Class)* | Adapter *(Object)*, Bridge, Composite, Decorator, Facade, Flyweight, Proxy |
| **Behavioral** *(Algorithmic & responsibility flow)* | Interpreter, Template Method | Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy, Visitor |

> **Why Modern C# Eliminates Many GoF Boilerplate Structures:**
> Several 1994 patterns existed to work around missing language features in C++ and Smalltalk:
> - **Iterator** is built directly into C# via `IEnumerable<T>`, `IAsyncEnumerable<T>`, and the compiler's `yield return` state-machine generator.
> - **Strategy** and **Command** with a single method can often be represented directly as strongly-typed delegates (`Func<TInput, CancellationToken, Task<TOutput>>`) unless the strategy requires multiple collaborating dependencies or metadata properties.
> - **Visitor** is largely superseded in modern C# by exhaustive switch expressions and recursive positional/property pattern matching (`switch { ... }`).

#### The Cost of Indirection & Speculative Generality (YAGNI)
Every design pattern resolves rigidity by introducing a **seam of indirection** (an interface, an abstract base class, a wrapper, or a message dispatcher). That indirection is never free:

$$\text{Net Architectural Value} = (\text{Probability of Change} \times \text{Cost of Future Change without Pattern}) - \text{Ongoing Indirection Tax}$$

The **Ongoing Indirection Tax** compounds across three dimensions:
1. **Cognitive & Navigation Overhead:** When a single use case jumps through `Controller` $\to$ `IMediator` $\to$ `ValidationBehavior` $\to$ `CommandHandler` $\to$ `IDomainService` $\to$ `IFactory` $\to$ `IRepository`, an engineer debugging a production incident must hold seven abstractions in working memory.
2. **Static Analysis Blindness:** Heavy reliance on dynamic dispatch, reflection, or generic mediator pipelines breaks IDE "Find Implementation" and call-hierarchy graphing.
3. **Runtime Allocation & Dispatch Overhead:** Interface dispatch (`callvirt` via vtable/interface dispatch stub) inhibits JIT inlining unless guarded by Dynamic PGO (Profile-Guided Optimization) in .NET 8+, and wrapper/pipeline allocations increase Gen 0 GC pressure on hot paths.

#### Rule of Three vs Speculative Generality
Apply **YAGNI (You Aren't Gonna Need It)** and the **Rule of Three**:
- **1st occurrence:** Write direct, concrete, readable code (`sealed class`).
- **2nd occurrence:** Note the similarity; tolerate minor duplication or extract a simple helper method if the domain concept is identical.
- **3rd occurrence:** Now that you have three concrete data points showing *how* the axis of variation actually behaves in production, refactor toward the appropriate pattern (e.g., Strategy or Factory).

---

### Section 1 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: A developer on your team submits a PR where every single service has a corresponding `IFooService` interface, an `AbstractFooFactory`, and a `FooFacade`, even though each interface has only one implementation and no external I/O. How do you address this in a code review?**
> **Model Answer:**
> I evaluate abstractions based on the **design forces** they resolve. Creating 1:1 interfaces and factories for internal, deterministic logic with a single implementation is **Speculative Generality**—it violates YAGNI and inflates the navigation and maintenance tax without providing architectural value.
> In C#, interfaces are warranted at **architectural seams**:
> 1. **External I/O boundaries** (databases, HTTP clients, message brokers, clocks) where deterministic unit testing requires test doubles.
> 2. **True polymorphic axes of variation** (e.g., multiple payment providers or discount strategies selected at runtime).
> 3. **Module or layer boundary inversion** (Dependency Inversion Principle across assemblies, or Decorator chains like caching/retry).
> For pure internal domain calculation classes with one implementation, I recommend marking the class `sealed`, injecting it directly (or testing it directly as a state-based collaborator), and deferring factory or interface extraction until a second implementation or cross-cutting decorator is actually required.

**Q2: How has the evolution of C# (from C# 1.0 to C# 12/13) changed the way you implement classic GoF patterns?**
> **Model Answer:**
> Many GoF patterns were originally ceremony-heavy workarounds for missing first-class functions, algebraic data types, and language-level iterators in 1990s C++. In modern C# 12/13:
> - **Iterator Pattern:** Replaced by `IEnumerable<T>` / `IAsyncEnumerable<T>` and compiler-generated `yield return` state machines.
> - **Prototype Pattern:** Largely replaced on immutable models by `record class` and `readonly record struct` with compiler-synthesized `with` expressions.
> - **Visitor & State Patterns:** Often simplified using exhaustive switch expressions, list patterns, and property pattern matching over closed type hierarchies.
> - **Template Method:** Frequently replaced by higher-order functions accepting `Func<T, Task>` or `IPipelineBehavior` composition rather than brittle base-class inheritance.

**Q3: Explain the trade-off between the Open/Closed Principle (OCP) and the YAGNI principle when deciding whether to introduce a Strategy or Factory pattern.**
> **Model Answer:**
> OCP states that a module should be open for extension but closed for modification, which encourages introducing abstractions (`IStrategy`) upfront so new behaviors can be added as new classes. YAGNI warns against building abstractions for hypothetical requirements that may never materialize.
> A senior engineer resolves this tension by identifying **known axes of volatility**. If the business domain inherently requires frequent additions along a well-defined seam (e.g., onboarding a new tax jurisdiction every quarter, or supporting multiple webhook event types), applying Strategy upfront pays off immediately. Conversely, if a team abstracts the database provider behind a custom DAL "in case we switch from PostgreSQL to MongoDB next year," the probability of change is near zero ($\approx 0$), making the abstraction a net-negative maintenance burden.

#### Practice Exercises

1. **Indirection Audit Drill:** Take an existing microservice endpoint in your codebase and trace a single HTTP request from the entry point down to the database command. Count the number of interfaces, DTO mappings, and wrapper classes crossed. Identify at least two abstractions that have only a single implementation and zero test mocks, and write a refactoring proposal to collapse them.
2. **GoF-to-Modern-C# Refactoring:** Write a classic 4-class GoF `Visitor` hierarchy (`IVisitor`, `ElementA`, `ElementB`, `ConcreteVisitor`) for calculating shipping fees on `StandardParcel`, `HazmatParcel`, and `FreightPallet`, then refactor it into a single 15-line C# 12 `record` hierarchy with an exhaustive `switch` expression. Compare line count, allocation overhead, and what happens when a 4th parcel type vs a 2nd operation is added (the Expression Problem).

---

## Section 2 — Creational Patterns

### 2.1 Factory Method & Abstract Factory

- **Factory Method:** Defines an interface for creating an object, but lets subclasses or delegates decide which class to instantiate.
- **Abstract Factory:** Provides an interface for creating **families of related or dependent objects** without specifying their concrete classes.

#### C# Enterprise Implementation: Multi-Cloud Storage Abstract Factory
```csharp
public interface IBlobStorage
{
    Task UploadAsync(string fileName, Stream content, CancellationToken ct);
}

public interface IQueueStorage
{
    Task SendMessageAsync(string queueName, string payload, CancellationToken ct);
}

// Abstract Factory
public interface ICloudResourceFactory
{
    IBlobStorage CreateBlobStorage();
    IQueueStorage CreateQueueStorage();
}

// Concrete Factory for Azure
public sealed class AzureResourceFactory(AzureOptions options) : ICloudResourceFactory
{
    public IBlobStorage CreateBlobStorage() => new AzureBlobStorage(options.ConnectionString);
    public IQueueStorage CreateQueueStorage() => new AzureServiceBusStorage(options.ServiceBusEndpoint);
}
```

---

### 2.2 Builder Pattern

The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations while strictly enforcing invariants at build time.

```csharp
public sealed class Invoice
{
    public CustomerId CustomerId { get; }
    public Currency Currency { get; }
    public IReadOnlyList<InvoiceLine> Lines { get; }
    public DateTimeOffset DueDate { get; }

    internal Invoice(CustomerId customerId, Currency currency, IReadOnlyList<InvoiceLine> lines, DateTimeOffset dueDate)
    {
        CustomerId = customerId;
        Currency = currency;
        Lines = lines;
        DueDate = dueDate;
    }
}

public sealed class InvoiceBuilder
{
    private CustomerId? _customerId;
    private Currency? _currency;
    private readonly List<InvoiceLine> _lines = [];
    private DateTimeOffset? _dueDate;

    public InvoiceBuilder ForCustomer(CustomerId customerId)
    {
        _customerId = customerId ?? throw new ArgumentNullException(nameof(customerId));
        return this;
    }

    public InvoiceBuilder InCurrency(Currency currency)
    {
        _currency = currency ?? throw new ArgumentNullException(nameof(currency));
        return this;
    }

    public InvoiceBuilder AddItem(string description, decimal amount, int quantity)
    {
        _lines.Add(new InvoiceLine(description, amount, quantity));
        return this;
    }

    public InvoiceBuilder DueInDays(int days)
    {
        _dueDate = DateTimeOffset.UtcNow.AddDays(days);
        return this;
    }

    public Invoice Build()
    {
        if (_customerId is null) throw new InvalidOperationException("Invoice must specify a customer.");
        if (_currency is null) throw new InvalidOperationException("Invoice must specify a currency.");
        if (_lines.Count == 0) throw new InvalidOperationException("Invoice must have at least one line item.");
        if (_dueDate is null) throw new InvalidOperationException("Invoice must have a due date.");

        return new Invoice(_customerId, _currency, _lines.AsReadOnly(), _dueDate.Value);
    }
}
```

---

### 2.3 Classic Singleton Anti-Pattern vs Container-Managed Singleton

| Dimension | Classic Static Singleton (`MyClass.Instance`) | Container-Managed Singleton (`AddSingleton<T>()`) |
|---|---|---|
| **Instantiation** | Static constructor or static field | DI Container composition root at startup |
| **Coupling** | Callers couple directly to the concrete class | Callers couple only to an injected interface (`IMyService`) |
| **Unit Testing** | Impossible to mock; state leaks across test suites | Trivial to mock or replace with a test double in tests |
| **Thread Safety** | Must be manually implemented (locks, lazy) | Managed by container lifecycle |
| **Status** | **Architectural Anti-Pattern** | **Legitimate Enterprise Best Practice** |

---

### 2.4 Prototype Pattern (C# `with` Expressions vs Shallow/Deep Copy) & Object Pool (`ObjectPool<T>`)

#### Prototype Pattern & Why `ICloneable` Is Broken in .NET
The **Prototype Pattern** creates new objects by cloning an existing pre-configured template instance rather than instantiating and populating a class from scratch.
In .NET 1.0, `System.ICloneable` exposed a single `object Clone()` method, which is universally considered a framework design mistake by the .NET BCL team because:
1. It is untyped (`object`), forcing reference casting or boxing.
2. Its contract fails to specify whether `Clone()` performs a **shallow copy** (`Object.MemberwiseClone()`, which copies value fields bit-by-bit and copies reference pointers) or a **deep copy** (recursively cloning the entire referenced object graph).

#### Shallow vs Deep Copy Trap with C# `record` and `with` Expressions
C# 9+ `record` types synthesize a protected copy constructor and a `<Clone>$` method invoked by `with` expressions. Crucially, **`with` performs a shallow copy**. If a record contains a mutable reference collection (`List<T>`, `Dictionary<TKey, TValue>`, or an array `T[]`), both the original record and the cloned record point to the **exact same heap collection**!

```csharp
public sealed record TenantPricingTemplate(
    string PlanName,
    decimal BaseMonthlyFee,
    IReadOnlyList<string> EnabledFeatures)
{
    // Explicit Deep Clone method to protect mutable/collection reference graphs
    public TenantPricingTemplate DeepClone(string newPlanName) =>
        this with
        {
            PlanName = newPlanName,
            EnabledFeatures = [.. EnabledFeatures] // C# 12 collection expression allocates a fresh backing list
        };
}
```

#### High-Throughput Object Pooling with `Microsoft.Extensions.ObjectPool`
When objects are expensive to allocate, initialize, or garbage-collect (e.g., cryptographic `IncrementalHash` instances, `StringBuilder`, reusable `RecyclableMemoryStream` buffers, or XML/JSON serializers with pre-warmed caches), allocating them per HTTP request causes Gen 2 / Large Object Heap (LOH) fragmentation when buffers exceed $85{,}000\text{ bytes}$.
The **Object Pool Pattern** pre-allocates or recycles instances in a thread-safe pool (`ObjectPool<T>`).

```csharp
using System.Security.Cryptography;
using System.Text;
using Microsoft.Extensions.ObjectPool;

// 1. Expensive reusable state object holding a pre-allocated buffer & native crypto handle
public sealed class WebhookSignatureComputationContext : IDisposable
{
    public byte[]ScratchBuffer { get; } = new byte[64 * 1024]; // 64 KB reusable buffer
    public StringBuilder CanonicalPayloadBuilder { get; } = new(capacity: 4096);

    public void Reset()
    {
        CanonicalPayloadBuilder.Clear();
        Array.Clear(ScratchBuffer, 0, ScratchBuffer.Length);
    }

    public void Dispose() => Reset();
}

// 2. Custom PooledObjectPolicy<T> enforcing state hygiene on Return()
public sealed class SignatureContextPooledPolicy : PooledObjectPolicy<WebhookSignatureComputationContext>
{
    public override WebhookSignatureComputationContext Create() => new();

    public override bool Return(WebhookSignatureComputationContext obj)
    {
        // Guard against oversized buffers bloating pool memory permanently
        if (obj.CanonicalPayloadBuilder.Capacity > 64 * 1024)
        {
            return false; // Drop instance; let GC collect it instead of returning to pool
        }

        obj.Reset(); // CRITICAL: Scrub sensitive tenant data before returning to pool!
        return true;
    }
}

// 3. Production Consumer with try/finally Return guarantee
public sealed class WebhookVerifier(ObjectPool<WebhookSignatureComputationContext> pool)
{
    public bool VerifyPayload(string timestamp, string body, ReadOnlySpan<byte> secretKey, ReadOnlySpan<byte> expectedMac)
    {
        WebhookSignatureComputationContext ctx = pool.Get();
        try
        {
            ctx.CanonicalPayloadBuilder.Append(timestamp).Append('.').Append(body);
            int bytesWritten = Encoding.UTF8.GetBytes(
                ctx.CanonicalPayloadBuilder.ToString(),
                ctx.ScratchBuffer);

            Span<byte> computedHash = stackalloc byte[HMACSHA256.HashSizeInBytes];
            HMACSHA256.HashData(secretKey, ctx.ScratchBuffer.AsSpan(0, bytesWritten), computedHash);

            return CryptographicOperations.FixedTimeEquals(computedHash, expectedMac);
        }
        finally
        {
            pool.Return(ctx);
        }
    }
}

// Registration in Program.cs:
// builder.Services.AddSingleton<ObjectPoolProvider, DefaultObjectPoolProvider>();
// builder.Services.AddSingleton(sp =>
//     sp.GetRequiredService<ObjectPoolProvider>().Create(new SignatureContextPooledPolicy()));
```

> **Senior Security & Reliability Warning on Object Pools:**
> Failing to scrub state inside `IPooledObjectPolicy<T>.Return(T obj)` causes **cross-tenant data bleed** (Tenant B reading leftover buffer bytes from Tenant A's request). Furthermore, never pool objects whose creation cost is cheaper than the interlocked CAS (`CompareExchange`) synchronization overhead of the pool itself.

---

### Section 2 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: In a .NET service with Dependency Injection, when do you actually need a Factory (`IFactory<T>` or `Func<T>`) instead of simply injecting `T` directly into the constructor?**
> **Model Answer:**
> Direct constructor injection works when the dependency's concrete type and lifetime are known at container resolution time. A Factory is required in four concrete scenarios:
> 1. **Runtime Parameter Selection:** Selecting an implementation based on runtime data that only arrives inside a request payload (e.g., resolving a payment processor based on `request.Currency` or `request.CountryCode`).
> 2. **Deferred or Conditional Instantiation:** When an object is expensive to construct and is only needed on a rare branch of execution.
> 3. **Lifetime Mismatch (Singleton Consuming Scoped/Transient Work):** A `Singleton` service cannot directly inject a `Scoped` dependency without creating a **Captive Dependency** bug; instead, it injects `IServiceScopeFactory` or a custom factory to create short-lived instances per operation.
> 4. **Multiple Independent Instances per Operation:** When a single method call must instantiate $N$ separate stateful protocol sessions or builders.

**Q2: How can a fluent `Builder` enforce mandatory fields at compile time rather than throwing `InvalidOperationException` inside `Build()` at runtime?**
> **Model Answer:**
> Using the **Step Builder Pattern** (also known as a Progressive Fluent Interface). Instead of every fluent method returning the concrete `InvoiceBuilder`, each step returns a narrow interface representing the *next valid state* in a compile-time finite state machine:
> `InvoiceBuilder.Create()` returns `IRequireCustomer` $\to$ `.ForCustomer(id)` returns `IRequireCurrency` $\to$ `.InCurrency(usd)` returns `IRequireLineItems` $\to$ `.AddItem(...)` returns `IBuildableInvoice` (which exposes both `.AddItem(...)` and `.Build()`).
> This makes calling `.Build()` before setting `Customer` and `Currency` a **compile-time syntax error** rather than a runtime exception. In C# 11+, for simpler data transfer objects without complex multi-step invariant calculations, `required init` properties provide compile-time enforcement without needing a Step Builder.

**Q3: What happens if you forget to call `pool.Return(obj)` on `Microsoft.Extensions.ObjectPool<T>`, and how does it differ from failing to dispose a database connection in a connection pool?**
> **Model Answer:**
> `DefaultObjectPool<T>` does **not** block callers or throw pool-exhaustion exceptions when all pooled items are checked out. Instead, if the lock-free fast slot and bounded `ConcurrentQueue<T>` are empty, `pool.Get()` simply calls `policy.Create()` to allocate a brand-new instance on the managed heap.
> Therefore, forgetting to call `pool.Return(obj)` does not deadlock the application (unlike leaking `SqlConnection` instances, which exhausts the max pool size of 100 and throws timeout exceptions); instead, it silently degrades into **unpooled per-request heap allocations**, defeating the purpose of the pool and triggering heavy Gen 0 / LOH garbage collection.

#### Practice Exercises

1. **Step Builder Implementation:** Refactor `InvoiceBuilder` from Section 2.2 into a compile-time **Step Builder** using interfaces (`ICustomerStep`, `ICurrencyStep`, `ILineItemStep`, `IBuildStep`) so that `InvoiceBuilder.Start().Build()` fails to compile until at least one customer, currency, and line item have been supplied.
2. **Object Pool Benchmark & Leak Audit:** Implement a `PooledStringBuilderPolicy` with `DefaultObjectPoolProvider` that caps retained capacity at $16\text{ KB}$. Write an xUnit test verifying that a `StringBuilder` that grew to $128\text{ KB}$ during a large report export is rejected by `Return()` (`returns false`) while a $4\text{ KB}$ instance is cleared and reused on the subsequent `Get()` call.

---

## Section 3 — Structural Patterns

### 3.1 Decorator Pattern & Scrutor Assembly Decoration

The Decorator pattern attaches additional responsibilities to an object dynamically without subclassing. It is ideal for cross-cutting concerns: caching, logging, retry policies, and performance metrics.

#### C# Implementation: Caching Decorator
```csharp
public interface ICustomerRepository
{
    Task<Customer?> GetByIdAsync(CustomerId id, CancellationToken ct);
}

// Concrete Core Service
public sealed class SqlCustomerRepository(AppDbContext dbContext) : ICustomerRepository
{
    public async Task<Customer?> GetByIdAsync(CustomerId id, CancellationToken ct) =>
        await dbContext.Customers.FindAsync([id.Value], ct);
}

// Decorator wrapping ICustomerRepository
public sealed class CachedCustomerRepository(
    ICustomerRepository inner,
    IMemoryCache cache,
    ILogger<CachedCustomerRepository> logger) : ICustomerRepository
{
    public async Task<Customer?> GetByIdAsync(CustomerId id, CancellationToken ct)
    {
        string cacheKey = $"customer:{id.Value}";
        if (cache.TryGetValue(cacheKey, out Customer? cached))
        {
            logger.LogDebug("Cache hit for {Key}", cacheKey);
            return cached;
        }

        var customer = await inner.GetByIdAsync(id, ct);
        if (customer is not null)
        {
            cache.Set(cacheKey, customer, TimeSpan.FromMinutes(10));
        }

        return customer;
    }
}
```

#### Automatic Registration via Scrutor:
```csharp
builder.Services.AddScoped<ICustomerRepository, SqlCustomerRepository>();
builder.Services.Decorate<ICustomerRepository, CachedCustomerRepository>();
```

---

### 3.2 Adapter, Facade, Composite & Proxy Patterns in .NET

#### Facade Pattern vs Leaky Subsystems

A **Facade** provides a simple, high-level interface to a complex, multi-class subsystem.
In an enterprise ordering pipeline, placing an order requires:
1. Checking inventory stock.
2. Authorizing credit card with Stripe.
3. Generating an invoice PDF.
4. Publishing an Azure Service Bus event.

Without a Facade, client controllers must inject 4 distinct services and orchestrate the sequence. A `CheckoutFacade` provides a single clean `ExecuteOrderAsync()` method, shielding callers from subsystem volatility.

#### Adapter Pattern: Wrapping a Legacy SOAP/SDK Client (Anti-Corruption Layer)
An **Adapter** converts the interface of a class (the *Adaptee*) into another interface that clients expect (the *Target*). In Domain-Driven Design, Adapters serve as an **Anti-Corruption Layer (ACL)** so ugly third-party or legacy SOAP data structures (`int` status codes, XML strings, nullable arrays) never leak into your domain model.

```csharp
// 1. Clean Domain Port (Target Interface owned by our Application Layer)
public interface ITaxCalculationPort
{
    Task<Money> CalculateSalesTaxAsync(Address destination, Money subtotal, CancellationToken ct);
}

// 2. Legacy 3rd-Party SOAP/SDK Client (Adaptee — cannot be modified)
public sealed class LegacyVertexSoapClient
{
    public Task<VertexSoapResponse> InvokeTaxEnvelopeAsync(string zip5, double netAmountDouble, string isoCurr)
        => Task.FromResult(new VertexSoapResponse { StatusCode = 0, CalculatedTaxAmount = netAmountDouble * 0.0825 });
}

public sealed class VertexSoapResponse
{
    public int StatusCode { get; set; }
    public double CalculatedTaxAmount { get; set; }
}

// 3. Object Adapter (Translates clean Domain types <-> Legacy SOAP primitives)
public sealed class VertexTaxAdapter(LegacyVertexSoapClient soapClient) : ITaxCalculationPort
{
    public async Task<Money> CalculateSalesTaxAsync(Address destination, Money subtotal, CancellationToken ct)
    {
        ct.ThrowIfCancellationRequested();

        VertexSoapResponse raw = await soapClient.InvokeTaxEnvelopeAsync(
            destination.PostalCode[..5],
            (double)subtotal.Amount,
            subtotal.Currency);

        if (raw.StatusCode != 0)
        {
            throw new TaxProviderUnavailableException($"Legacy Vertex SOAP failed with code {raw.StatusCode}.");
        }

        decimal roundedTax = Math.Round((decimal)raw.CalculatedTaxAmount, 2, MidpointRounding.ToEven);
        return new Money(roundedTax, subtotal.Currency);
    }
}
```

#### Composite Pattern: Hierarchical Pricing & Permission Trees
The **Composite Pattern** composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual leaf objects (`SkuLineItem`) and nested compositions (`PromotionalBundle`) uniformly through a shared component interface.

```csharp
public interface IPricedComponent
{
    string Name { get; }
    decimal CalculatePrice();
}

// Leaf Node
public sealed record SkuItem(string Name, decimal UnitPrice) : IPricedComponent
{
    public decimal CalculatePrice() => UnitPrice;
}

// Composite Node (contains Leaf nodes and/or nested Composite bundles)
public sealed class PromotionalBundle(
    string name,
    decimal bundleDiscountPercentage,
    IReadOnlyList<IPricedComponent> children) : IPricedComponent
{
    public string Name => name;

    public decimal CalculatePrice()
    {
        decimal grossSum = children.Sum(child => child.CalculatePrice());
        return Math.Round(grossSum * (1m - bundleDiscountPercentage), 2, MidpointRounding.ToEven);
    }
}

// Usage: Uniform evaluation of arbitrary nesting depth
// var holidayPack = new PromotionalBundle("Ultimate Dev Station", 0.10m, [
//     new SkuItem("4K Monitor", 600m),
//     new PromotionalBundle("Peripheral Starter Kit", 0.05m, [
//         new SkuItem("Mechanical Keyboard", 150m),
//         new SkuItem("Ergonomic Mouse", 100m)
//     ])
// ]);
// decimal total = holidayPack.CalculatePrice(); // Evaluates tree recursively
```

#### Proxy Pattern: Virtual, Protection & Resilience Proxies
A **Proxy** provides a surrogate or placeholder for another object to control access to it.
While **Decorator** and **Proxy** share an identical UML class structure (both implement `IService` and wrap an inner `IService`), their **architectural intents** differ:
- **Decorator** focuses on *augmenting behavior* (stacking cross-cutting concerns onto a caller-supplied or DI-chained object).
- **Proxy** focuses on *controlling access and lifecycle* of the target subject:
  - **Virtual Proxy:** Delays expensive instantiation until the first method invocation (e.g., EF Core `Castle.Proxies` lazy-loading navigation properties or wrapping a heavy dependency inside `Lazy<T>`).
  - **Protection Proxy:** Enforces tenant isolation or RBAC authorization checks before delegating to the real subject.
  - **Remote / Resilience Proxy:** Manages network serialization and circuit-breaking (e.g., typed `HttpClient` with `Microsoft.Extensions.Http.Resilience` / Polly v8 pipelines, or generated gRPC client stubs).

```csharp
public sealed class TenantProtectionCustomerProxy(
    ICustomerRepository realSubject,
    ITenantContextAccessor tenantContext) : ICustomerRepository
{
    public async Task<Customer?> GetByIdAsync(CustomerId id, CancellationToken ct)
    {
        Customer? customer = await realSubject.GetByIdAsync(id, ct);
        if (customer is not null && customer.TenantId != tenantContext.CurrentTenantId)
        {
            throw new UnauthorizedAccessException(
                $"Cross-tenant access denied: Tenant {tenantContext.CurrentTenantId} cannot read Customer {id.Value}.");
        }

        return customer;
    }
}
```

---

### Section 3 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: Decorator, Proxy, and Adapter all wrap an underlying object. How do you distinguish them in an architectural design review?**
> **Model Answer:**
> They are distinguished by **interface compatibility** and **intent**:
> 1. **Adapter** changes the interface (`ITarget` wraps `Adaptee`). Its intent is *compatibility and translation* across mismatched boundaries (e.g., wrapping a third-party SDK behind a domain port).
> 2. **Decorator** keeps the exact same interface (`IService` wraps `IService`). Its intent is *open/closed behavior composition*—layering concerns like caching, telemetry, and validation dynamically.
> 3. **Proxy** also keeps the same interface (`IService` wraps `IService`), but its intent is *access control, lifecycle management, or location transparency* (e.g., lazy initialization, RBAC enforcement, or remote RPC marshaling). Often, a Proxy manages or restricts whether the underlying target is even instantiated or invoked.

**Q2: When stacking multiple Decorators in ASP.NET Core DI (e.g., `SqlCustomerRepository` wrapped by `CachedCustomerRepository` wrapped by `LoggingCustomerRepository`), why does registration order matter, and what happens if you get it backward?**
> **Model Answer:**
> In Scrutor (`services.Decorate<TService, TDecorator>()`), each call wraps the *previously registered* service descriptor like layers of an onion. The **last** decorator registered becomes the **outermost** wrapper invoked first by consumers:
> - Registering `SqlRepo` $\to$ `Decorate<CachedRepo>` $\to$ `Decorate<LoggingRepo>` means callers hit `LoggingRepo` $\to$ `CachedRepo` $\to$ `SqlRepo`. Every call (including cache hits) is logged and timed.
> - If you reverse `CachedRepo` and `LoggingRepo` (`SqlRepo` $\to$ `LoggingRepo` $\to$ `CachedRepo`), then cache hits return immediately from `CachedRepo` and **completely bypass `LoggingRepo`**, leaving you blind to cache-hit traffic and latency metrics!
> Similarly, a `RetryDecorator` must wrap the inner `SqlRepo` *inside* the `CachedRepo` so retries only execute on database misses rather than retrying memory cache reads.

**Q3: What is the danger of using `IMemoryCache` inside a Decorator that wraps an EF Core repository returning tracked entities?**
> **Model Answer:**
> `IMemoryCache` stores direct in-process object references on the local heap (it does not serialize by default). If `SqlCustomerRepository` returns an EF Core-tracked entity and `CachedCustomerRepository` caches that reference across HTTP requests:
> 1. **Thread-Safety & Change Tracker Corruption:** Concurrent HTTP requests retrieve the exact same entity reference and may mutate its properties simultaneously across threads.
> 2. **Captive `DbContext` Memory Leak:** If lazy-loading proxies or navigation fix-ups retain a reference back to the originating `DbContext`, caching the entity pins the disposed `DbContext` graph in memory.
> **Fix:** Either project to immutable `record` DTOs/read models with `.AsNoTracking()` before caching, or clone/serialize the snapshot before storing it in `IMemoryCache`.

#### Practice Exercises

1. **Multi-Decorator Ordering Pipeline:** Register an `IExchangeRateProvider` with three decorators using Scrutor: `ResilienceRetryExchangeRateDecorator`, `MemoryCacheExchangeRateDecorator`, and `OpenTelemetryMetricsExchangeRateDecorator`. Write an integration test with a fake inner provider that fails on call 1, succeeds on call 2, and serves from cache on call 3. Assert that total outer metrics count = 2 requests, inner provider invocation count = 2 (1 failure + 1 retry), and database/network hits on the 2nd external request = 0.
2. **Composite Authorization Tree:** Model an enterprise permission system using the **Composite Pattern** where `IPermissionGrant` is implemented by `AtomicPermission(string Scope)` and `RolePermissionGroup(string RoleName, IReadOnlyList<IPermissionGrant> Grants)`. Implement `bool HasPermission(string requiredScope)` and a cycle-detection guard in `RolePermissionGroup` so circular role assignments (`Admin` contains `Ops` contains `Admin`) throw on construction rather than causing a `StackOverflowException`.

---

## Section 4 — Behavioral Patterns

### 4.1 Strategy Pattern

The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable at runtime.

```csharp
public interface IDiscountStrategy
{
    CustomerTier Tier { get; }
    Money CalculateDiscount(Money total);
}

public sealed class VipDiscountStrategy : IDiscountStrategy
{
    public CustomerTier Tier => CustomerTier.Vip;
    public Money CalculateDiscount(Money total) => new(total.Amount * 0.20m, total.Currency);
}

public sealed class RegularDiscountStrategy : IDiscountStrategy
{
    public CustomerTier Tier => CustomerTier.Regular;
    public Money CalculateDiscount(Money total) => new(0m, total.Currency);
}

// Strategy Dispatcher:
public sealed class DiscountCalculator(IEnumerable<IDiscountStrategy> strategies)
{
    public Money ApplyDiscount(CustomerTier tier, Money total)
    {
        var strategy = strategies.FirstOrDefault(s => s.Tier == tier)
            ?? throw new NotSupportedException($"No strategy registered for tier {tier}");
        return strategy.CalculateDiscount(total);
    }
}
```

---

### 4.2 Chain of Responsibility Pattern

The Chain of Responsibility passes a request along a pipeline of handlers. Each handler decides whether to process the request, mutate the context, or pass it to the next handler in the chain.
**Where .NET Uses It:** ASP.NET Core Middleware (`app.Use(...)`) and MediatR Pipeline Behaviors (`IPipelineBehavior<TRequest, TResponse>`).

---

### 4.3 State Pattern in Domain Entities

The State pattern allows an object to alter its behavior when its internal state changes. Instead of massive `switch (status)` statements scattered across methods, state transitions are encapsulated in dedicated state objects.

```csharp
public interface IOrderState
{
    void AddLine(Order context, OrderLine line);
    void Cancel(Order context);
}

public sealed class DraftOrderState : IOrderState
{
    public void AddLine(Order context, OrderLine line) => context.InternalAddLine(line);
    public void Cancel(Order context) => context.SetState(new CancelledOrderState());
}

public sealed class ShippedOrderState : IOrderState
{
    public void AddLine(Order context, OrderLine line) =>
        throw new InvalidOperationException("Cannot add lines to an order that has already shipped.");
    public void Cancel(Order context) =>
        throw new InvalidOperationException("Cannot cancel an order that has already shipped.");
}
```

---

## Section 5 — Dependency Injection as an Architectural Discipline

### 5.1 The Composition Root & Keyed Services (.NET 8+)

- **Composition Root:** The single, unified location in an application where the entire dependency graph is registered and composed (in modern .NET: `Program.cs`).
- **Service Locator Anti-Pattern:** Injecting `IServiceProvider` or calling `serviceProvider.GetService<T>()` inside business classes. This hides dependencies, couples domain classes to the DI container, and makes unit testing painful.

#### Keyed Services in .NET 8+:
```csharp
// Registration:
builder.Services.AddKeyedScoped<INotificationService, EmailNotificationService>("email");
builder.Services.AddKeyedScoped<INotificationService, SmsNotificationService>("sms");

// Consumption:
public sealed class NotificationDispatcher(
    [FromKeyedServices("email")] INotificationService emailService,
    [FromKeyedServices("sms")] INotificationService smsService)
{
    public async Task AlertUserAsync(string message, bool isUrgent, CancellationToken ct)
    {
        if (isUrgent) await smsService.SendAsync(message, ct);
        else await emailService.SendAsync(message, ct);
    }
}
```

---

### 5.2 The Options Pattern with Compile-Time Validation

```csharp
public sealed class PaymentGatewayOptions
{
    public const string SectionName = "PaymentGateway";

    [Required, Url]
    public string BaseUrl { get; set; } = default!;

    [Range(1, 60)]
    public int TimeoutSeconds { get; set; } = 30;
}

// In Program.cs: Compile-time source generated validation at host startup!
builder.Services.AddOptions<PaymentGatewayOptions>()
    .Bind(builder.Configuration.GetSection(PaymentGatewayOptions.SectionName))
    .ValidateDataAnnotations()
    .ValidateOnStart(); // Crashes immediately if config is missing or invalid!
```

---

## Section 6 — Enterprise Application Patterns

### 6.1 The Repository & Unit of Work Debate with EF Core

A frequent debate in senior interviews: *"Do we need a Generic Repository and Unit of Work on top of Entity Framework Core?"*

**The Senior Answer:**
- EF Core's `DbSet<T>` **is already** an implementation of the Repository Pattern.
- EF Core's `DbContext` **is already** an implementation of the Unit of Work Pattern.
- Creating a `GenericRepository<T>` with `GetById`, `GetAll`, `Add`, and `Delete` adds pure boilerplate, hides EF Core's powerful query capabilities (compiled queries, projections, batch updates), and leaks EF's change tracker anyway.
- **When Repositories ARE Justified:** Create **Specialized Aggregate Repositories** (e.g., `IOrderRepository`, not `IRepository<T>`) that return rich aggregate roots with invariants loaded, encapsulating complex data access rules and providing clear unit-testing boundaries.

---

## Section 7 — In-Process CQRS & MediatR Pipeline Architecture

### 7.1 Command Query Responsibility Segregation (CQRS)

In-Process CQRS splits operations into two distinct mental models:
1. **Commands:** Mutate state. Return `void`, `Result`, or created IDs. Never return complex query DTOs.
2. **Queries:** Read data without side effects. Return read-only DTOs optimized for the UI. Can bypass domain aggregates and query SQL directly via Dapper for maximum throughput.

#### MediatR Pipeline Behavior for Validation
```csharp
public sealed class ValidationBehavior<TRequest, TResponse>(IEnumerable<IValidator<TRequest>> validators)
    : IPipelineBehavior<TRequest, TResponse> where TRequest : notnull
{
    public async Task<TResponse> Handle(TRequest request, RequestHandlerDelegate<TResponse> next, CancellationToken ct)
    {
        if (!validators.Any()) return await next();

        var context = new ValidationContext<TRequest>(request);
        var validationResults = await Task.WhenAll(validators.Select(v => v.ValidateAsync(context, ct)));
        var failures = validationResults.SelectMany(r => r.Errors).Where(f => f != null).ToList();

        if (failures.Count != 0)
            throw new ValidationException(failures);

        return await next();
    }
}
```

#### The Critique of MediatR (Senior Staff Judgment)
While MediatR is ubiquitous, senior engineers recognize its drawbacks:
- It turns explicit code into untraceable "magic" by hiding call sites from static code analysis ("Find Usages" in IDEs fails).
- It introduces heap allocations for request records and handlers on high-throughput paths.
- It can encourage God-handlers where developers dump orchestration logic instead of modeling domain aggregates.
- In modern C# with Minimal APIs and direct service injection, MediatR is often an unnecessary layer of indirection.

---

## Section 8 — Clean, Onion & Hexagonal (Ports & Adapters) Architecture

### 8.1 The Dependency Rule

```text
+-------------------------------------------------------------+
| Presentation / Web API (Controllers, Minimal APIs)         |
|   +-------------------------------------------------------+ |
|   | Infrastructure (EF Core, Azure SDKs, Redis, Email)   | |
|   |   +-------------------------------------------------+ | |
|   |   | Application (Use Cases, Commands, Queries, DTOs)| | |
|   |   |   +-------------------------------------------+ | | |
|   |   |   | Domain Core (Entities, Value Objects,     | | | |
|   |   |   |              Domain Events, Invariants)   | | | |
|   |   |   +-------------------------------------------+ | | |
|   |   +-------------------------------------------------+ | |
|   +-------------------------------------------------------+ |
+-------------------------------------------------------------+
```
**The Inviolable Rule:** Dependencies must point **strictly inward**.
The Domain Core has **zero dependencies** on external libraries (no EF Core, no ASP.NET Core, no cloud SDKs).

---

## Section 9 — Vertical Slice Architecture & Feature-Driven Design

### 9.1 Technical Layering vs Vertical Slices

- **Technical Layering (Clean Architecture):** Organizes code horizontally by technical role (`Controllers/`, `Services/`, `Repositories/`, `Entities/`). Adding a single field to a form requires modifying 7 files across 4 distinct projects.
- **Vertical Slice Architecture:** Organizes code vertically by **business feature**. Every slice is an independent vertical column containing its endpoint, command, handler, validation, and database query in one cohesive folder:

```text
Features/
└── Orders/
    ├── CreateOrder/
    │   ├── CreateOrderEndpoint.cs
    │   ├── CreateOrderCommand.cs
    │   ├── CreateOrderValidator.cs
    │   └── CreateOrderHandler.cs
    ├── GetOrderById/
    │   ├── GetOrderByIdEndpoint.cs
    │   ├── GetOrderByIdQuery.cs
    │   └── OrderSummaryDto.cs
    └── CancelOrder/
        ├── CancelOrderEndpoint.cs
        └── CancelOrderCommand.cs
```

---

## Section 10 — Modular Monolith Architecture & Boundary Enforcement

### 10.1 Module Encapsulation & Automated Architecture Tests

A **Modular Monolith** organizes a single deployment unit into strictly decoupled modules (e.g., `Billing`, `Catalog`, `Identity`).
Modules communicate exclusively through public interfaces and asynchronous domain events; they never share database tables or reference each other's internal classes.

#### Automated Architecture Rules with NetArchTest:
```csharp
[Fact]
public void DomainLayer_ShouldNotHaveDependencyOnInfrastructure()
{
    var result = Types.InAssembly(typeof(Order).Assembly)
        .That()
        .ResideInNamespace("Domain")
        .ShouldNot()
        .HaveDependencyOn("Infrastructure")
        .GetResult();

    Assert.True(result.IsSuccessful, "Domain layer must not depend on Infrastructure!");
}
```

---

## Section 11 — Functional Design Patterns in Modern C#

### 11.1 Discriminated Unions with OneOf

Instead of throwing exceptions for expected business branches, model outcomes explicitly:

```csharp
public sealed class PaymentProcessor
{
    public OneOf<PaymentSuccess, InsufficientFunds, GatewayTimeout> Process(PaymentRequest request)
    {
        if (request.Amount > 10000) return new InsufficientFunds("Limit exceeded");
        return new PaymentSuccess(Guid.NewGuid());
    }
}

// Consumer handles outcomes exhaustively:
var result = processor.Process(request);
result.Switch(
    success => Console.WriteLine($"Paid: {success.TxId}"),
    insufficientFunds => Console.WriteLine($"Declined: {insufficientFunds.Reason}"),
    timeout => Console.WriteLine("Retry later")
);
```

---

## Section 12 — Senior Scenarios, Codebase Refactoring & Capstone

### 12.1 Refactoring an Over-Engineered Enterprise Codebase

You are brought in as a Staff Engineer to review a microservice that processes 2,000 HTTP requests per second. The code has:
1. `IGenericRepository<T>` on top of EF Core.
2. MediatR commands for simple single-row database queries.
3. 5 horizontal layers for every feature.
4. Latency is high, and developer velocity has ground to a halt.

#### Senior Remediation Plan:
1. **Flatten Read Paths:** Remove MediatR and repository layers for queries. Execute read-only queries directly in Minimal API endpoints using EF Core `AsNoTracking()` projections or Dapper.
2. **Eliminate Generic Repositories:** Expose focused aggregate root repositories only where complex multi-entity domain invariants require encapsulation.
3. **Migrate to Vertical Slices:** Co-locate feature commands, handlers, and endpoints to reduce cognitive friction and build times.

---

# Part III — Interview Readiness

## 1. Mid-Level vs Senior-Level Patterns Comparison

| Topic | Mid-Level Candidate Response | Senior / Staff-Level Candidate Response |
|---|---|---|
| **Design Patterns** | "Patterns are best-practice templates that should be applied to make code extensible." | "Patterns are documented solutions to recurring design tensions. Every pattern introduces a trade-off—typically trading indirection and cognitive load for runtime extensibility. A senior engineer knows when *not* to use a pattern." |
| **Singleton Pattern** | "Singleton ensures a class has only one instance using a private constructor and a static `Instance` property." | "Static singletons are an anti-pattern because they introduce global mutable state, tightly couple consumers to concrete types, and complicate unit testing. In enterprise .NET, we use container-managed singletons (`AddSingleton<T>()`) behind injected interfaces." |
| **Repository Pattern with EF Core** | "Always create a generic `IRepository<T>` on top of `DbContext` so you can swap out Entity Framework for another database." | "A generic repository on top of EF Core is an anti-pattern. `DbSet<T>` is already a repository and `DbContext` is a unit of work. Abstraction for the sake of hypothetically replacing an ORM is a YAGNI violation. Repositories are only justified when encapsulating complex aggregate roots and domain invariants." |
| **Clean Architecture vs Vertical Slice** | "Clean Architecture is always the gold standard because it separates Domain, Application, and Infrastructure layers." | "Clean Architecture excels at isolating pure, long-lived domain invariants from external technologies. However, for many enterprise apps, horizontal layering causes high developer friction and shotgun surgery. Vertical Slice Architecture organizes code around business features, maximizing cohesion within slices." |
| **MediatR** | "MediatR decouples controllers from business logic and makes code clean." | "MediatR provides in-process messaging and pipeline behaviors, but it can easily become an architectural crutch. It obscures call hierarchies from static analysis, introduces heap allocations, and often turns controllers into dumb pass-throughs while centralizing procedural logic in handlers." |

---

## 2. Rapid-Fire Revision Sheet (50 Senior-Level Truths)

1. A design pattern is a solution to a problem within a context, balancing competing design forces.
2. The Abstract Factory creates families of related objects; the Factory Method delegates instantiation of a single object to subclasses or delegates.
3. The Builder pattern constructs complex objects with strict invariant enforcement, preventing partially initialized instances.
4. Static GoF singletons create hidden dependencies and test isolation problems; container-managed singletons (`AddSingleton`) preserve testability.
5. `Microsoft.Extensions.ObjectPool` reduces GC allocation churn by recycling expensive memory buffers and state objects.
6. The Adapter pattern translates an incompatible interface into one expected by clients, frequently used in Anti-Corruption Layers.
7. The Decorator pattern adds behavior dynamically by wrapping instances of the same interface, adhering strictly to the Open/Closed Principle.
8. Scrutor enables automated decoration in ASP.NET Core DI via `services.Decorate<TInterface, TDecorator>()`.
9. The Facade pattern provides a simplified, high-level interface to a complex subsystem, preventing subsystem leakage.
10. The Composite pattern enables clients to treat individual objects and hierarchies of objects identically.
11. The Proxy pattern controls access to an underlying object, providing lazy initialization (virtual proxy) or access control (protection proxy).
12. The Strategy pattern encapsulates interchangeable algorithms, replacing rigid conditional branching with polymorphic dispatch.
13. The Chain of Responsibility pattern passes requests along a pipeline of handlers, forming the architectural basis of ASP.NET Core middleware.
14. The Command pattern encapsulates an action as an object, enabling undo/redo queues, transactional outbox logging, and deferred execution.
15. The Mediator pattern replaces many-to-many relationships with centralized communication, decoupling senders from receivers.
16. The State pattern encapsulates state-dependent behaviors into separate classes, eliminating massive switch statements in entities.
17. The Specification pattern encapsulates query predicates and business rules, enabling reuse across both memory and EF Core query translation.
18. Dependency Injection is an architectural technique to realize Inversion of Control and the Dependency Inversion Principle.
19. The Composition Root is the centralized startup location (`Program.cs`) where the entire application dependency graph is constructed.
20. The Service Locator anti-pattern injects `IServiceProvider` into classes, obscuring dependencies and preventing static analysis.
21. Keyed Services in .NET 8 allow registering multiple implementations of an interface using strings or enum keys.
22. `AddOptionsWithValidateOnStart` validates strongly-typed configuration settings at application startup rather than at first access.
23. EF Core's `DbSet<T>` is already an in-memory repository; generic repositories wrapping EF Core frequently add useless indirection.
24. Aggregate Repositories should only be created for Aggregate Roots in Domain-Driven Design to enforce invariant boundaries.
25. The Result pattern (`Result<T, TError>`) treats expected business failures as typed return values, avoiding expensive exception handling.
26. Domain Events represent significant business occurrences within an aggregate, decoupled from immediate persistence side effects.
27. In-process CQRS separates write mutations (Commands) from read operations (Queries) to optimize each path independently.
28. Queries in CQRS can bypass domain models and repositories entirely, querying the database directly using Dapper or compiled EF projections.
29. MediatR pipeline behaviors (`IPipelineBehavior`) execute cross-cutting concerns (validation, logging, telemetry) in a clean chain of responsibility.
30. Overusing MediatR obscures code navigation in IDEs, complicates debugging, and introduces heap allocation overhead on hot paths.
31. The Dependency Rule in Clean Architecture mandates that source code dependencies must point strictly inward toward domain policies.
32. The Domain Core in Clean Architecture must have zero dependencies on external frameworks, databases, or UI packages.
33. Ports in Hexagonal Architecture are interfaces defined in the application core; Adapters are concrete implementations in infrastructure.
34. Vertical Slice Architecture organizes code by business features rather than technical layers, maximizing functional cohesion.
35. In Vertical Slice Architecture, code duplication across slices is preferred over premature, coupled shared abstractions.
36. A Modular Monolith partitions an application into independent business modules within a single deployment artifact.
37. Modules in a Modular Monolith should communicate exclusively via public interface contracts or asynchronous events.
38. NetArchTest enforces architectural boundaries in automated CI tests, preventing unauthorized cross-layer or cross-module references.
39. The `internal` access modifier combined with `[InternalsVisibleTo]` preserves module boundary encapsulation in C#.
40. Modern C# records provide structural value equality, shallow immutability, and clean non-destructive mutation via `with` expressions.
41. Discriminated unions modeled via libraries like `OneOf` enforce compile-time exhaustive checking for domain outcomes.
42. Monadic railway-oriented programming composes operations using `Bind`, `Map`, and `Tap` without nesting `if` checks.
43. Refactoring over-engineered code requires identifying useless abstractions, flattening read paths, and removing redundant layers.
44. The Factory pattern should not be introduced unless object creation involves complex invariants or polymorphic selection.
45. In-memory caching should be implemented via the Decorator pattern rather than embedding cache checks inside core domain repositories.
46. The Template Method pattern defines an algorithm's skeleton in an abstract class, deferring specific steps to subclasses.
47. The Observer pattern defines a one-to-many dependency where object state changes notify observers (the foundation of reactive extensions).
48. Options validation source generators in .NET 8 validate configuration at compile time, reducing startup overhead.
49. Domain models should never depend on CQRS command or query DTOs; mapping should occur in the application layer.
50. Architectural simplicity (KISS/YAGNI) should always be the default stance; patterns are introduced only when justified by concrete forces.

---

## 3. Self-Assessment Rubric

| Dimension | Needs Work (Junior) | Developing (Mid-Level) | Senior-Ready | Strong Senior / Staff-Level |
|---|---|---|---|---|
| **Pattern Understanding** | Memorizes code snippets; forces patterns into every problem. | Understands GoF pattern intents; implements Factory, Strategy, and Decorator. | Articulates design forces and consequences; knows when to reject patterns; prevents over-engineering. | Designs custom architectural frameworks; balances indirection against cognitive load and runtime allocation costs. |
| **Dependency Injection** | Uses Service Locator; injects `IServiceProvider` everywhere. | Configures standard services in `Program.cs`; understands lifetimes. | Uses Keyed Services, Options validation, and Decorator assembly scanning with Scrutor; avoids captive dependencies. | Establishes pure composition roots; designs modular DI container abstractions across enterprise plugin architectures. |
| **Architectural Organization** | Dumps code into a single project or builds rigid 7-layer abstractions. | Implements standard Clean Architecture (Core, Application, Infrastructure). | Compares Clean Architecture vs Vertical Slice trade-offs; implements in-process CQRS with pipeline behaviors. | Architectures Modular Monoliths; enforces layer boundaries via NetArchTest in CI; formulates legacy migration roadmaps. |
| **Enterprise Persistence Patterns** | Wraps EF Core in generic repositories; claims it makes switching DBs easy. | Uses EF Core `DbContext` and specialized repositories appropriately. | Defends the repository vs EF Core debate with architectural authority; models aggregates and domain events cleanly. | Designs CQRS read paths bypassing ORM overhead; optimizes persistence architectures for high-throughput scaling. |
| **Modern C# Idioms** | Uses legacy procedural patterns and exceptions for control flow. | Uses records and basic pattern matching in domain classes. | Employs functional patterns (Result, Discriminated Unions via OneOf, railway-oriented pipelines) idiomatically. | Establishes domain modeling standards; enforces zero-allocation design patterns on high-throughput microservices. |

---

# Part IV — References

1. **Foundational Design Pattern Literature:**
   - Gamma, E., Helm, R., Johnson, R., & Vlissides, J. *Design Patterns: Elements of Reusable Object-Oriented Software* (GoF). Addison-Wesley, 1994.
   - Fowler, Martin. *Patterns of Enterprise Application Architecture* (PoEAA). Addison-Wesley, 2002.
   - Martin, Robert C. *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall, 2017.
   - Evans, Eric. *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley, 2003.
2. **Modern Architectural Resources:**
   - Bogard, Jimmy. "Vertical Slice Architecture". *Jimmy Bogard's Blog*, 2018.
   - Seemann, M., & van Deursen, S. *Dependency Injection Principles, Practices, and Patterns*. Manning, 2019.
   - Microsoft Learn: [Architecting Modern Web Applications with ASP.NET Core and Azure](https://learn.microsoft.com/dotnet/architecture/modern-web-apps-azure/)
   - Microsoft Learn: [Dependency Injection in .NET](https://learn.microsoft.com/dotnet/core/extensions/dependency-injection)
