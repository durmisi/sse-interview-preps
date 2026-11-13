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

#### Start with a Transition Table, Not a Class Hierarchy

| Current state | Command | Guard | Next state |
|---|---|---|---|
| Draft | Submit | At least one valid line | Submitted |
| Submitted | Ship | Payment and reservation confirmed | Shipped |
| Draft or Submitted | Cancel | Fulfillment has not started | Cancelled |
| Shipped | Cancel | Not allowed; use a separate returns workflow | Unchanged |

The table forces decisions about forbidden transitions and repeated commands before implementation. A small enum plus one cohesive transition function may be clearer than a class per state. State objects earn their cost when behavior varies substantially across states, not merely because a `Status` property exists.

The pattern also does not resolve concurrent transitions. Two callers can load the same Submitted order and separately approve Ship and Cancel. Persist the transition with a concurrency check, then reload and reevaluate a conflicting command. Decide explicitly whether a repeated Submit is a harmless no-op, a returned prior result, or an error.

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

### 4.4 Command, Mediator, Observer & State Patterns in Modern C#

#### Custom Lightweight Mediator & Command Pipeline with `IPipelineBehavior<TRequest, TResponse>`
Understanding how an in-process **Command** and **Mediator** pipeline works under the hood demystifies libraries like MediatR and Wolverine. A request is modeled as an immutable **Command** object (`IRequest<TResponse>`), dispatched through a reverse-folded chain of `IPipelineBehavior<TRequest, TResponse>` wrappers (Chain of Responsibility) before reaching the single `IRequestHandler<TRequest, TResponse>`.

```csharp
public interface IRequest<out TResponse>;

public interface IRequestHandler<in TRequest, TResponse>
    where TRequest : IRequest<TResponse>
{
    Task<TResponse> HandleAsync(TRequest request, CancellationToken ct);
}

public delegate Task<TResponse> RequestHandlerContinuation<TResponse>();

public interface IPipelineBehavior<in TRequest, TResponse>
    where TRequest : notnull
{
    Task<TResponse> HandleAsync(
        TRequest request,
        RequestHandlerContinuation<TResponse> next,
        CancellationToken ct);
}

// Lightweight Russian-Doll Pipeline Executor
public sealed class LightweightCommandBus(IServiceProvider serviceProvider)
{
    public Task<TResponse> SendAsync<TRequest, TResponse>(TRequest request, CancellationToken ct)
        where TRequest : IRequest<TResponse>
    {
        var handler = serviceProvider.GetRequiredService<IRequestHandler<TRequest, TResponse>>();
        var behaviors = serviceProvider.GetServices<IPipelineBehavior<TRequest, TResponse>>().Reverse();

        RequestHandlerContinuation<TResponse> pipeline = () => handler.HandleAsync(request, ct);

        foreach (var behavior in behaviors)
        {
            var currentBehavior = behavior;
            var nextContinuation = pipeline;
            pipeline = () => currentBehavior.HandleAsync(request, nextContinuation, ct);
        }

        return pipeline();
    }
}
```

#### Observer Pattern & Why Classic C# `event` Leaks Memory (The Lapsed Listener Problem)
The **Observer Pattern** establishes a one-to-many pub/sub dependency where a *Subject* notifies registered *Observers* of state changes.
In C#, the `event` keyword compiles into a multicast delegate field on the publisher (`Subject`). When a subscriber executes `publisher.PriceChanged += OnPriceChanged;`, the publisher's internal invocation list stores a **strong GC reference** (`new EventHandler(subscriberInstance, methodPtr)`) pointing directly to the subscriber!

```text
[GC Root] ---> [Singleton Publisher] --(Strong Delegate Ref)--> [Scoped/Transient Subscriber] (LEAKED!)
```

- **The Lapsed Listener Trap:** If the **Publisher** has a longer lifetime than the **Subscriber** (e.g., a `Singleton` cache or event aggregator publishing C# `event` notifications to `Scoped` or `Transient` components), and the subscriber forgets to unsubscribe (`-=`) in `Dispose()`, the garbage collector **can never collect the subscriber**. Over thousands of requests, the heap fills with zombie subscribers and every event invocation gets progressively slower ($O(N)$ dead handlers).
- **Modern .NET Remedies:**
  1. Prefer `System.Threading.Channels.Channel<T>` or `IObservable<T>` (`IDisposable` subscription tokens) over raw C# `event` fields in backend services.
  2. In desktop/UI scenarios (WPF/MAUI), use `WeakEventManager<TEventSource, TEventArgs>` so the publisher holds a `WeakReference` to the listener.

#### Modern C# Pattern-Matching State Machine
When state transitions do not require polymorphic dependency injection per state, modern C# tuple switch expressions express a deterministic **Finite State Machine (FSM)** in a single, auditable table with compile-time exhaustiveness checking:

```csharp
public enum SubscriptionState { Trial, Active, PastDue, Suspended, Cancelled }
public enum SubscriptionTrigger { PayInvoice, PaymentFailed, GracePeriodExpired, CancelRequest }

public static class SubscriptionStateMachine
{
    public static SubscriptionState Transition(SubscriptionState current, SubscriptionTrigger trigger) =>
        (current, trigger) switch
        {
            (SubscriptionState.Trial,     SubscriptionTrigger.PayInvoice)         => SubscriptionState.Active,
            (SubscriptionState.Trial,     SubscriptionTrigger.GracePeriodExpired) => SubscriptionState.Cancelled,
            (SubscriptionState.Active,    SubscriptionTrigger.PayInvoice)         => SubscriptionState.Active,
            (SubscriptionState.Active,    SubscriptionTrigger.PaymentFailed)      => SubscriptionState.PastDue,
            (SubscriptionState.PastDue,   SubscriptionTrigger.PayInvoice)         => SubscriptionState.Active,
            (SubscriptionState.PastDue,   SubscriptionTrigger.GracePeriodExpired) => SubscriptionState.Suspended,
            (SubscriptionState.Suspended, SubscriptionTrigger.PayInvoice)         => SubscriptionState.Active,
            (_,                           SubscriptionTrigger.CancelRequest)      => SubscriptionState.Cancelled,
            _ => throw new InvalidOperationException(
                $"Illegal state transition: cannot apply trigger '{trigger}' while in state '{current}'.")
        };
}
```

---

### Section 4 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: When you inject `IEnumerable<IDiscountStrategy>` into `DiscountCalculator`, what is the performance pitfall if there are 25 strategies and each strategy injects heavy dependencies?**
> **Model Answer:**
> Resolving `IEnumerable<IDiscountStrategy>` causes the DI container to **instantiate all 25 concrete strategy classes** and their entire transitive dependency graphs on every single scope/resolution, even though `strategies.FirstOrDefault(s => s.Tier == tier)` only uses **one** of them and discards the other 24!
> Additionally, scanning the list linearly is $O(N)$.
> **Senior Fix:**
> 1. In .NET 8+, register strategies as **Keyed Services** (`builder.Services.AddKeyedScoped<IDiscountStrategy, VipDiscountStrategy>(CustomerTier.Vip)`) and resolve only the single matching strategy via `IServiceProvider.GetRequiredKeyedService<IDiscountStrategy>(tier)` inside a factory delegate.
> 2. If strategies are stateless (`Singleton`), index them once at startup into a `FrozenDictionary<CustomerTier, IDiscountStrategy>` for $O(1)$ zero-allocation lookup.

**Q2: Compare the classic OOP State Pattern (`IOrderState` classes) against a C# tuple-switch State Machine (`(state, trigger) switch`). When should you choose each?**
> **Model Answer:**
> - **Tuple-Switch State Machine:** Best when transitions are pure rules over enum/record states and you want to see the **entire transition matrix in one place** on a single screen. It has zero heap allocations and guarantees exhaustiveness at compile time.
> - **OOP Polymorphic State Pattern (`IOrderState`):** Best when *each state has rich, distinct behavior across 5+ methods* or carries state-specific data (e.g., `ShippedState` requires a `TrackingNumber` and `ShippedAtUtc`, whereas `DraftState` does not). Using a discriminated union record hierarchy (`abstract record OrderState` with `sealed record DraftState`, `sealed record ShippedState(string TrackingNo)`) combines the best of both worlds.

**Q3: Explain how the Lapsed Listener memory leak occurs in .NET and how you diagnose and fix it in production.**
> **Model Answer:**
> A Lapsed Listener leak occurs when a short-lived object (`Scoped` or `Transient`) subscribes to a standard C# `event` on a long-lived object (`Singleton`). Because multicast delegates store a strong reference to the target object (`Delegate.Target`), the `Singleton` roots the short-lived subscriber in the GC graph indefinitely unless `publisher.SomeEvent -= handler` is explicitly executed.
> In production, a `dotnet-gcdump` or WinDbg `!dumpheap -stat` / `!gcroot` analysis reveals tens of thousands of live instances of the short-lived service all rooted by an `EventHandler[]` invocation array inside the singleton. The fix is either strict `IDisposable` unsubscription or replacing in-memory events with `Channel<T>` or scoped message dispatch.

#### Practice Exercises

1. **Zero-Allocation Strategy Lookup:** Refactor `DiscountCalculator` from Section 4.1 to use `FrozenDictionary<CustomerTier, IDiscountStrategy>` (.NET 8 `System.Collections.Frozen`) initialized once, and write a test asserting that registering two strategies for the same `CustomerTier` throws an explicit startup configuration exception rather than silently picking the first or last.
2. **Pipeline Short-Circuiting:** Add an `IdempotencyBehavior<TRequest, TResponse>` to `LightweightCommandBus` (Section 4.4) that checks an `IDistributedCache` for `IIdempotentCommand.RequestId`. Verify that when a duplicate `RequestId` arrives, the behavior returns the cached `TResponse` directly and **never invokes** `next()`.

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

### 5.3 Keyed Services (`.AddKeyedScoped`), Open Generics & Why Service Locator Is an Anti-Pattern

#### Open Generic Registration (`typeof(IPipelineBehavior<,>)`)
When an abstraction is generic across dozens of command or entity types (e.g., `IValidator<T>`, `IPipelineBehavior<TRequest, TResponse>`, or `IEventHandler<TEvent>`), registering each closed generic type manually is brittle. .NET's built-in DI container natively resolves **Open Generics**:

```csharp
// Register open generic once:
builder.Services.AddScoped(typeof(IPipelineBehavior<,>), typeof(LoggingBehavior<,>));
builder.Services.AddScoped(typeof(IPipelineBehavior<,>), typeof(ValidationBehavior<,>));

// When the container resolves IPipelineBehavior<PlaceOrderCommand, Result<OrderId>>,
// it automatically closes the generic type and constructs LoggingBehavior<PlaceOrderCommand, Result<OrderId>>.
```

#### `IOptions<T>` vs `IOptionsSnapshot<T>` vs `IOptionsMonitor<T>`
Choosing the wrong Options interface is a common source of production configuration bugs and Captive Dependency exceptions:

| Interface | DI Lifetime | Reloads on `appsettings.json` Change? | Named Options Support? | Primary Use Case |
|---|---|---|---|---|
| `IOptions<T>` | **Singleton** | **No** (Cached once at app startup) | No | Static startup settings that require a process restart to change. |
| `IOptionsSnapshot<T>` | **Scoped** | **Yes** (Recomputed once per HTTP request scope) | Yes (`Get(name)`) | Scoped request handlers needing consistent config across a single request. **Cannot be injected into a Singleton!** |
| `IOptionsMonitor<T>` | **Singleton** | **Yes** (Live `.CurrentValue` + `.OnChange()` callback) | Yes (`Get(name)`) | Singleton background workers, circuit breakers, or dynamic feature flags. |

> **AOT & Compile-Time `[OptionsValidator]` Source Generator (.NET 8+):**
> Calling `.ValidateDataAnnotations()` uses runtime reflection (`Validator.TryValidateObject`), which is incompatible with Native AOT trimming. In .NET 8+, define a partial validator class decorated with `[OptionsValidator]`:
> ```csharp
> [OptionsValidator]
> public partial class ValidatePaymentGatewayOptions : IValidateOptions<PaymentGatewayOptions>;
> // Register: builder.Services.AddSingleton<IValidateOptions<PaymentGatewayOptions>, ValidatePaymentGatewayOptions>();
> ```

#### Why Service Locator Is an Anti-Pattern (vs Legitimate Factory Use)
Calling `serviceProvider.GetRequiredService<IBillingEngine>()` inside a domain or application method violates the **Explicit Dependencies Principle**:
1. **Dishonest API Contract:** Looking at `public OrderProcessor(IServiceProvider sp)` gives callers and unit tests zero visibility into whether `OrderProcessor` requires 1 dependency or 15 dependencies.
2. **Runtime Bomb:** Missing registrations fail midway through executing a business flow at runtime instead of failing at container validation (`ValidateOnBuild = true` / `ValidateScopes = true`).
3. **The Only Legitimate Exception:** Resolving `IServiceScopeFactory` or `IServiceProvider` *strictly inside a thin infrastructure Factory or Middleware adapter* located at the boundary of the Composition Root.

---

### Section 5 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: What happens if a `Singleton` service injects `IOptionsSnapshot<T>`, and why does ASP.NET Core throw an `InvalidOperationException` in the `Development` environment?**
> **Model Answer:**
> `IOptionsSnapshot<T>` is registered with a **Scoped** lifetime so that configuration changes are bound once per HTTP request and remain consistent throughout that request. Injecting a `Scoped` service into a `Singleton` creates a **Captive Dependency**: the `Singleton` captures the very first request's `IOptionsSnapshot<T>` instance forever, turning it into a stale singleton and holding onto any scoped resources.
> In `Development`, `WebApplication.CreateBuilder` enables `ValidateScopes = true` and `ValidateOnBuild = true` by default on `ServiceProviderOptions`, which inspects the dependency graph at startup and immediately throws `InvalidOperationException: Cannot consume scoped service 'IOptionsSnapshot<...>' from singleton`. The fix is to inject `IOptionsMonitor<T>` (which is a `Singleton` and exposes `.CurrentValue`).

**Q2: Why should you enable `ValidateOnBuild = true` and `ValidateScopes = true` in all environments (or CI integration tests), and what edge cases does `ValidateOnBuild` NOT catch?**
> **Model Answer:**
> `ValidateOnBuild = true` verifies at `builder.Build()` time that every registered descriptor's constructor dependencies can be resolved and have legal lifetimes. However, `ValidateOnBuild` intentionally **cannot validate**:
> 1. **Open Generic Types** (`typeof(IValidator<>)`), because the container does not know which closed type arguments will be requested at runtime.
> 2. **Factory Delegates** (`services.AddScoped<IFoo>(sp => new Foo(sp.GetRequiredService<IBar>()))`), because the lambda body is opaque to static constructor inspection until invoked.
> 3. **Controllers** (unless `.AddControllersAsServices()` is called), because MVC constructs controllers via `IControllerActivator` rather than resolving the controller type directly from the root container.

**Q3: How do you resolve a Keyed Service dynamically when the key (`string` or `enum`) is only known at runtime from an HTTP request header?**
> **Model Answer:**
> Constructor `[FromKeyedServices("key")]` only works for compile-time constant keys. When the key arrives dynamically at runtime (e.g., `X-Payment-Provider: stripe`), inject a narrow factory delegate `Func<string, IPaymentGateway>` registered in the Composition Root:
> ```csharp
> builder.Services.AddScoped<Func<string, IPaymentGateway>>(sp =>
>     providerKey => sp.GetRequiredKeyedService<IPaymentGateway>(providerKey));
> ```
> This keeps `IServiceProvider` confined to `Program.cs` while giving the application service a clean, mockable `Func<string, IPaymentGateway>` dependency.

#### Practice Exercises

1. **Compile-Time Options Validation Drill:** Create a `ResiliencePolicyOptions` class with `[Range(1, 5)] int MaxRetries`, `[Required] string FallbackEndpoint`, and implement a custom `IValidateOptions<ResiliencePolicyOptions>` that cross-validates two properties (e.g., `CircuitBreakerThreshold` must be strictly greater than `MaxRetries`). Register it with `.ValidateOnStart()` and write an xUnit test asserting `OptionsValidationException` is thrown when the host starts with invalid configuration.
2. **Captive Dependency Detector:** Write an xUnit test that loads your application's `IServiceCollection` and builds a `ServiceProvider` with `new ServiceProviderOptions { ValidateOnBuild = true, ValidateScopes = true }` so any future PR introducing a captive dependency or missing registration fails CI immediately.

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

### 6.2 Result Pattern, Value Objects & Domain Events with EF Core `SaveChangesInterceptor`

#### Allocation-Free `Result<TValue, TError>` Pattern
Throwing exceptions for expected domain outcomes (e.g., `DuplicateSku`, `InsufficientCredit`, `CouponExpired`) is an anti-pattern: stack trace capture in .NET costs $\approx 5\text{–}20\,\mu\text{s}$ per throw and treats predictable business rules as non-local `goto` jumps. A `readonly record struct Result<TValue, TError>` lives on the stack with zero heap allocation:

```csharp
public readonly record struct Error(string Code, string Description)
{
    public static readonly Error None = new(string.Empty, string.Empty);
}

public readonly record struct Result<TValue, TError>
{
    private readonly TValue? _value;
    private readonly TError? _error;

    public bool IsSuccess { get; }
    public bool IsFailure => !IsSuccess;

    private Result(TValue value)
    {
        IsSuccess = true;
        _value = value;
        _error = default;
    }

    private Result(TError error)
    {
        IsSuccess = false;
        _value = default;
        _error = error;
    }

    public TValue Value => IsSuccess
        ? _value!
        : throw new InvalidOperationException("Cannot access Value on a failed Result.");

    public TError Error => !IsSuccess
        ? _error!
        : throw new InvalidOperationException("Cannot access Error on a successful Result.");

    public static Result<TValue, TError> Success(TValue value) => new(value);
    public static Result<TValue, TError> Failure(TError error) => new(error);

    public static implicit operator Result<TValue, TError>(TValue value) => Success(value);
    public static implicit operator Result<TValue, TError>(TError error) => Failure(error);
}
```

#### Value Objects: Structural Equality & Self-Validation (`Money`)
A **Value Object** has no conceptual identity (`Id`); it is defined strictly by its structural attributes, is immutable once created, and enforces its domain invariants upon construction:

```csharp
public readonly record struct Money
{
    public decimal Amount { get; }
    public string Currency { get; }

    public Money(decimal amount, string currency)
    {
        if (string.IsNullOrWhiteSpace(currency) || currency.Length != 3)
            throw new ArgumentException("Currency must be a valid 3-letter ISO-4217 code.", nameof(currency));

        Amount = Math.Round(amount, 2, MidpointRounding.ToEven);
        Currency = currency.ToUpperInvariant();
    }

    public static Money operator +(Money left, Money right)
    {
        if (left.Currency != right.Currency)
            throw new InvalidOperationException($"Cannot add {left.Currency} and {right.Currency} without FX conversion.");
        return new Money(left.Amount + right.Amount, left.Currency);
    }
}
```

#### Domain Events & EF Core `SaveChangesInterceptor`
Domain aggregates record **Domain Events** (`IDomainEvent`) in an internal list as state transitions occur, remaining 100% ignorant of databases or message buses. An EF Core `SaveChangesInterceptor` harvests and dispatches these events automatically during unit-of-work persistence:

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Diagnostics;

public interface IDomainEvent
{
    Guid EventId { get; }
    DateTimeOffset OccurredOnUtc { get; }
}

public abstract class AggregateRoot<TId>(TId id) where TId : notnull
{
    private readonly List<IDomainEvent> _domainEvents = [];
    public TId Id { get; protected init; } = id;
    public IReadOnlyCollection<IDomainEvent> DomainEvents => _domainEvents.AsReadOnly();

    protected void RaiseDomainEvent(IDomainEvent domainEvent) => _domainEvents.Add(domainEvent);
    public void ClearDomainEvents() => _domainEvents.Clear();
}

public sealed class DispatchDomainEventsInterceptor(IDomainEventDispatcher dispatcher) : SaveChangesInterceptor
{
    public override async ValueTask<InterceptionResult<int>> SavingChangesAsync(
        DbContextEventData eventData,
        InterceptionResult<int> result,
        CancellationToken ct = default)
    {
        if (eventData.Context is not null)
        {
            await DispatchEventsAsync(eventData.Context, ct);
        }

        return await base.SavingChangesAsync(eventData, result, ct);
    }

    private async Task DispatchEventsAsync(DbContext context, CancellationToken ct)
    {
        // Loop handles cascading domain events raised by handlers during dispatch
        while (true)
        {
            var aggregatesWithEvents = context.ChangeTracker
                .Entries<AggregateRoot<Guid>>()
                .Where(e => e.Entity.DomainEvents.Count != 0)
                .Select(e => e.Entity)
                .ToList();

            if (aggregatesWithEvents.Count == 0) break;

            var events = aggregatesWithEvents.SelectMany(a => a.DomainEvents).ToList();
            aggregatesWithEvents.ForEach(a => a.ClearDomainEvents());

            foreach (var domainEvent in events)
            {
                await dispatcher.PublishAsync(domainEvent, ct);
            }
        }
    }
}
```

---

### 6.3 Repository vs Direct `DbContext` Debate & The Specification Pattern (`Expression<Func<T, bool>>`)

When repositories proliferate into methods like `GetActiveOrdersOverAmountWithCustomerByRegionAsync(...)`, query predicates become duplicated across LINQ-to-Entities queries and in-memory domain validations.
The **Specification Pattern** encapsulates a query predicate (`Expression<Func<T, bool>>`), eager-loading `.Includes`, and sorting rules into a reusable, composable object that EF Core can translate directly into SQL:

```csharp
using System.Linq.Expressions;
using Microsoft.EntityFrameworkCore;

public abstract class Specification<TEntity> where TEntity : class
{
    public Expression<Func<TEntity, bool>> Criteria { get; private set; } = _ => true;
    public List<Expression<Func<TEntity, object>>> Includes { get; } = [];
    public Expression<Func<TEntity, object>>? OrderByDescending { get; private set; }
    public int? Take { get; private set; }
    public bool AsNoTracking { get; protected init; } = true;

    protected void AddCriteria(Expression<Func<TEntity, bool>> criteria) =>
        Criteria = CombineAnd(Criteria, criteria);

    protected void AddInclude(Expression<Func<TEntity, object>> includeExpression) =>
        Includes.Add(includeExpression);

    protected void ApplyOrderByDescending(Expression<Func<TEntity, object>> orderByDescExpression) =>
        OrderByDescending = orderByDescExpression;

    protected void ApplyPaging(int take) => Take = take;

    // Expression-tree parameter rebinding so EF Core translates combined predicates into SQL AND
    private static Expression<Func<TEntity, bool>> CombineAnd(
        Expression<Func<TEntity, bool>> left,
        Expression<Func<TEntity, bool>> right)
    {
        ParameterExpression param = Expression.Parameter(typeof(TEntity), "x");
        Expression leftBody = ReplaceParameterVisitor.Replace(left.Body, left.Parameters[0], param);
        Expression rightBody = ReplaceParameterVisitor.Replace(right.Body, right.Parameters[0], param);
        return Expression.Lambda<Func<TEntity, bool>>(Expression.AndAlso(leftBody, rightBody), param);
    }

    private sealed class ReplaceParameterVisitor(ParameterExpression oldParam, ParameterExpression newParam)
        : ExpressionVisitor
    {
        public static Expression Replace(Expression body, ParameterExpression oldParam, ParameterExpression newParam) =>
            new ReplaceParameterVisitor(oldParam, newParam).Visit(body);

        protected override Expression VisitParameter(ParameterExpression node) =>
            ReferenceEquals(node, oldParam) ? newParam : base.VisitParameter(node);
    }
}

// Concrete Domain Specification: High-Value Overdue Invoices for a Tenant
public sealed class HighValueOverdueInvoicesSpec : Specification<InvoiceEntity>
{
    public HighValueOverdueInvoicesSpec(Guid tenantId, decimal minimumAmount, DateTimeOffset asOfUtc)
    {
        AddCriteria(i => i.TenantId == tenantId && !i.IsPaid);
        AddCriteria(i => i.TotalAmount >= minimumAmount && i.DueDateUtc < asOfUtc);
        AddInclude(i => i.LineItems);
        ApplyOrderByDescending(i => i.TotalAmount);
        ApplyPaging(take: 100);
    }
}

// EF Core Specification Evaluator
public static class SpecificationEvaluator
{
    public static IQueryable<TEntity> GetQuery<TEntity>(
        IQueryable<TEntity> inputQuery,
        Specification<TEntity> spec) where TEntity : class
    {
        IQueryable<TEntity> query = spec.AsNoTracking ? inputQuery.AsNoTracking() : inputQuery;
        query = query.Where(spec.Criteria);
        query = spec.Includes.Aggregate(query, (current, include) => current.Include(include));

        if (spec.OrderByDescending is not null)
            query = query.OrderByDescending(spec.OrderByDescending);

        if (spec.Take is int take)
            query = query.Take(take);

        return query;
    }
}
```

---

### Section 6 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: Why does `Func<TEntity, bool>` inside a repository `.Where(Func<TEntity, bool>)` cause catastrophic production outages with EF Core, whereas `Expression<Func<TEntity, bool>>` does not?**
> **Model Answer:**
> `IQueryable<T>.Where(Expression<Func<T, bool>>)` passes an AST (Abstract Syntax Tree) to EF Core's query provider, which translates the expression tree into a parameterized SQL `WHERE` clause executed by the database engine.
> Conversely, passing `Func<T, bool>` resolves to `IEnumerable<T>.Where(Func<T, bool>)` (LINQ-to-Objects), because `IQueryable<T>` inherits from `IEnumerable<T>` and a compiled delegate is an opaque IL method pointer that EF Core cannot inspect. EF Core therefore executes `SELECT * FROM Table` with **no `WHERE` clause**, pulls millions of rows over the network into app memory, and filters them in C#!

**Q2: Should Domain Events be dispatched inside `SavingChangesAsync` (before `SaveChanges` commits) or `SavedChangesAsync` (after `SaveChanges` commits)?**
> **Model Answer:**
> It depends on whether the handler mutates the **same database transaction** or triggers **external side effects**:
> - **Before Commit (`SavingChangesAsync`):** Ideal for in-process domain handlers that mutate other entities in the same `DbContext` or write **Transactional Outbox** (`OutboxMessage`) rows so state changes and outbox events commit atomically in a single database transaction.
> - **After Commit (`SavedChangesAsync`):** Required if a handler performs immediate non-transactional external I/O (sending an email or publishing directly to RabbitMQ without an Outbox), because dispatching before commit risks sending an external message for a database transaction that subsequently fails and rolls back (a phantom event). In enterprise systems, writing an `OutboxMessage` inside `SavingChangesAsync` is the gold standard.

**Q3: Why should a Repository never return `IQueryable<T>` to application or controller layers?**
> **Model Answer:**
> Returning `IQueryable<T>` creates a **Leaky Abstraction**:
> 1. Callers can append arbitrary `.Where()` clauses that reference unindexed columns or non-translatable C# methods, causing runtime `InvalidOperationException` translation failures far away from the data access layer.
> 2. Deferred execution means the SQL query actually executes outside the repository—potentially after the `DbContext` scope or stopwatch timer in the repository has already completed.
> 3. Unit testing `IQueryable<T>` over in-memory lists (`AsQueryable()`) gives false confidence because LINQ-to-Objects accepts C# expressions and null semantics that fail in SQL Server/PostgreSQL.

#### Practice Exercises

1. **Composable Specification Builder:** Extend `Specification<TEntity>` in Section 6.3 with an `Or(Specification<TEntity> other)` combinator using `Expression.OrElse` and `ReplaceParameterVisitor`. Write an xUnit test verifying that combining `VipCustomerSpec` OR `HighSpendCustomerSpec` produces a single expression tree with one shared `ParameterExpression`.
2. **Transactional Outbox Interceptor:** Modify `DispatchDomainEventsInterceptor` so that in addition to invoking in-process handlers, it serializes every `IDomainEvent` to JSON and inserts an `OutboxMessage(Guid Id, string Type, string PayloadJson, DateTimeOffset OccurredOnUtc)` into `context.Set<OutboxMessage>()` within the same `SavingChangesAsync` call.

---

## Section 7 — In-Process CQRS & MediatR Pipeline Architecture

### 7.1 Command Query Responsibility Segregation (CQRS)

In-Process CQRS splits operations into two distinct mental models:
1. **Commands:** Mutate state. Return `void`, `Result`, or created IDs. Never return complex query DTOs.
2. **Queries:** Read data without side effects. Return read-only DTOs optimized for the UI. Can bypass domain aggregates and query SQL directly via Dapper for maximum throughput.

**Separate the decisions:** CQRS does not require a mediator, separate processes, separate databases, or event sourcing. These are independent choices. A query handler can project DTOs with EF Core; switching to Dapper is a measured implementation choice, not part of the definition. Similarly, command responses can include useful outcome data without turning the command into a general-purpose query API.

Read-after-write behavior depends on the actual data path. Reading the primary after a committed write avoids asynchronous projection lag; reading a cache or replica can still return stale data even if every handler lives in one process. Promise consistency based on storage and routing, not folder names.

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

**Validation concurrency caveat:** Parallel validation is safe only when validators and their dependencies support concurrent use. Two validators using the same scoped EF Core `DbContext` must not execute database operations concurrently. Run them sequentially or give independent work separate correctly owned contexts; a DI scope does not make its services thread-safe.

#### The Critique of MediatR (Senior Staff Judgment)
While MediatR is ubiquitous, senior engineers recognize its drawbacks:
- It turns explicit code into untraceable "magic" by hiding call sites from static code analysis ("Find Usages" in IDEs fails).
- It introduces heap allocations for request records and handlers on high-throughput paths.
- It can encourage God-handlers where developers dump orchestration logic instead of modeling domain aggregates.
- In modern C# with Minimal APIs and direct service injection, MediatR is often an unnecessary layer of indirection.

### 7.2 Pipeline Ordering Is Part of Correctness

Behaviors execute like nested function calls: outer behaviors see the request first and the response last. Specify intended ordering and test it with observable effects rather than assuming registration order is obvious.

| Concern | Decision to make | Failure if left implicit |
|---|---|---|
| Authorization and cache | Authorize access before returning protected cached data; scope keys appropriately | A cache hit bypasses access checks |
| Validation and transaction | Keep pure input validation outside the transaction; enforce race-sensitive rules in storage | Long transactions or check-then-act races |
| Retry and transaction | Retry a safe unit with a fresh transaction and a deliberate state-reset strategy | Reusing failed state or repeating an external charge |
| Metrics and retry | Record logical requests separately from physical attempts | Retries distort success rates and request volume |
| Result and commit | Define which typed outcomes allow commit | A failure result returns normally and accidentally commits staged mutations |

A database rollback cannot undo an email or an HTTP charge. A generic retry behavior must not wrap arbitrary handlers with external side effects and assume transactions make retries safe. See Module 07 for durable messaging and idempotency boundaries.

**Failure-path exercise:** Have a handler stage an entity change and return a business failure without throwing. Verify that your transaction behavior follows the declared commit policy. Also test validation short-circuiting, cancellation, and a retry that must not duplicate an external effect.

---

### Section 7 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: How do you design a `ValidationBehavior<TRequest, TResponse>` in MediatR that returns a typed `Result<TValue, Error>` instead of throwing a `ValidationException`?**
> **Model Answer:**
> Throwing `ValidationException` for invalid user input violates the Result pattern and forces exception-handling middleware to catch control-flow exceptions. Instead, constrain `TResponse` to implement an `IResult` factory interface (or C# 11 `static abstract` member `TResponse.FromValidationErrors(Error[] errors)`):
> ```csharp
> public interface IValidationFailureFactory<out TResponse>
> {
>     static abstract TResponse CreateValidationFailure(IReadOnlyList<Error> errors);
> }
> ```
> When `ValidationBehavior<TRequest, TResponse>` detects validation failures and `TResponse : IValidationFailureFactory<TResponse>`, it directly calls `return TResponse.CreateValidationFailure(errors);` without throwing an exception or allocating a stack trace!

**Q2: Explain the difference between In-Process CQRS and Distributed Event-Driven CQRS. When does a team make the mistake of conflating them?**
> **Model Answer:**
> - **In-Process CQRS** separates read models (`IQueryHandler` projecting directly from SQL via Dapper/`AsNoTracking`) from write models (`ICommandHandler` loading rich DDD aggregates via EF Core) **over the same relational database** within a single process. It has zero eventual consistency lag and low operational complexity.
> - **Distributed CQRS** physically separates the Write Store (e.g., PostgreSQL or EventStoreDB) from a denormalized Read Store (e.g., Elasticsearch or Redis) synchronized asynchronously via message brokers.
> Teams frequently make the mistake of assuming "CQRS requires separate databases, Kafka, and eventual consistency" when 95% of enterprise bottlenecks are solved simply by separating the code paths (In-Process CQRS) so read queries stop hydrating 15-table EF Core entity graphs.

**Q3: Give a 60-second whiteboarding script explaining how In-Process CQRS and Clean Architecture dependency arrows interact.**
> **Model Answer (The 60-Second Whiteboarding Script):**
> *"Let me draw four concentric rings—or three vertical boxes pointing inward. At the center is **Domain**: pure C# Aggregates, Value Objects, and Domain Events with zero NuGet packages. Surrounding it is **Application**: our Use Cases, split via CQRS into Commands and Queries, plus Port interfaces like `IPaymentGateway`. Outside sits **Infrastructure** (EF Core, Dapper, Stripe SDK) and **Presentation** (ASP.NET Core Minimal APIs).*
> *Every source-code project reference arrow points **strictly inward** toward Domain. Presentation references Application; Infrastructure references Application and Domain; Application references only Domain. At runtime, Infrastructure implements Application's Port interfaces via Dependency Inversion, while Query Handlers in Application use fast read-only projections and Command Handlers orchestrate Domain Aggregates."*

#### Practice Exercises

1. **Zero-Exception Validation Pipeline:** Implement `ValidationBehavior<TRequest, TResponse>` using C# 11 `static abstract` interface members (`IValidationResult<TResponse>`) so that any `Result<T, Error[]>` returned from a command handler is automatically populated with validation errors without throwing `ValidationException`.
2. **Transaction Pipeline Behavior with Execution Strategy:** Write a `TransactionBehavior<TCommand, TResponse>` that only wraps requests implementing `ICommand<TResponse>` (skipping `IQuery<TResponse>`) using `dbContext.Database.CreateExecutionStrategy().ExecuteAsync(...)` and `BeginTransactionAsync()`.

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

### 8.2 Ports & Adapters (Hexagonal) Mechanics & The 60-Second Whiteboarding Script

#### Reconciling Clean, Onion, and Hexagonal (Ports & Adapters)
Alistar Cockburn's **Hexagonal Architecture (Ports & Adapters)**, Jeffrey Palermo's **Onion Architecture**, and Robert C. Martin's **Clean Architecture** are variations of the exact same foundational principle: **Dependency Inversion at Architectural Boundaries**.

- **Primary / Driving Adapters (Left Side of Hexagon):** Entry points that *drive* the application—ASP.NET Core Controllers, Minimal APIs, gRPC services, Service Bus consumers, CLI runners. They call **Inbound Ports** (Application Use Cases / Command Handlers).
- **Secondary / Driven Adapters (Right Side of Hexagon):** Infrastructure implementations that are *driven by* the application—PostgreSQL EF Core repositories, Stripe HTTP clients, Redis caches, SMTP senders. They implement **Outbound Ports** (interfaces owned by the Application/Domain core).

```text
 [Driving Adapters]          [Application Core]           [Driven Adapters]
+------------------+     +------------------------+     +--------------------+
| Minimal API /    | --> | Inbound Port           |     | SqlOrderRepository |
| gRPC Endpoint    |     | (PlaceOrderUseCase)    |     | (EF Core / Npgsql) |
+------------------+     |           |            |     +--------------------+
                         |           v            |               ^
+------------------+     |    [Domain Aggregate]  |               | (Implements)
| ServiceBus       | --> |           |            |               |
| Queue Consumer   |     |           v            |     +--------------------+
+------------------+     | Outbound Port          | <-- | StripePayment      |
                         | (IOrderRepo, IPayment) |     | GatewayAdapter     |
                         +------------------------+     +--------------------+
```

#### The 60-Second Whiteboarding Script for Drawing Clean Architecture Dependency Arrows
When asked in a system design or architecture interview to diagram how a .NET solution is structured:
1. **Draw the Core First (0–15s):** Draw `MyService.Domain` at the center. State clearly: *"This `.csproj` has zero `<PackageReference>` tags—only pure C# entities, value objects, domain exceptions, and domain events."*
2. **Draw the Application Ring (15–30s):** Draw `MyService.Application` around `Domain` with a compile-time arrow `Application` $\to$ `Domain`. State: *"Application defines the use cases (commands/queries) and declares outbound Port interfaces (`IPaymentGateway`, `IOrderRepository`)."*
3. **Draw Infrastructure & Web on the Outside (30–45s):** Draw `MyService.Infrastructure` and `MyService.Api` on the outer ring. Draw compile-time arrows pointing **inward** (`Infrastructure` $\to$ `Application`; `Api` $\to$ `Application`).
4. **Explain the Runtime vs Compile-Time Inversion (45–60s):** Draw a dashed runtime control-flow arrow from `Application` out to `Infrastructure`, and explain: *"At runtime, `PlaceOrderHandler` invokes `StripePaymentGateway` in Infrastructure, but at compile time `Infrastructure` references `Application` to implement `IPaymentGateway`. That Dependency Inversion keeps our core testable in isolation without spinning up Docker or SQL."*

---

### Section 8 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: If the Domain and Application layers cannot reference `Microsoft.EntityFrameworkCore`, where do you put EF Core `IEntityTypeConfiguration<T>` classes, and how do you map private collection fields on Domain Aggregates?**
> **Model Answer:**
> `IEntityTypeConfiguration<Order>` lives strictly inside the **Infrastructure** project (e.g., `Infrastructure/Persistence/Configurations/OrderConfiguration.cs`), which references both `Domain` and `Microsoft.EntityFrameworkCore`.
> In the `Domain` project, the `Order` aggregate exposes `public IReadOnlyCollection<OrderLine> Lines => _lines.AsReadOnly();` backed by `private readonly List<OrderLine> _lines = [];` along with a `private Order() { }` parameterless constructor for EF materialization. Inside `OrderConfiguration`, EF Core 8+ maps the backing field cleanly via `builder.Navigation(o => o.Lines).UsePropertyAccessMode(PropertyAccessMode.Field);` without requiring a single `[Key]` or `[ForeignKey]` attribute in the `Domain` assembly.

**Q2: Where should the Composition Root (`AddScoped`, `AddDbContext`) live when `Api` should not directly instantiate internal `Infrastructure` classes?**
> **Model Answer:**
> Each outer layer exposes a single public `IServiceCollection` extension method—`AddApplicationServices()` in `Application` and `AddInfrastructureServices(IConfiguration)` in `Infrastructure`—while keeping all concrete repository and adapter classes `internal sealed` inside `Infrastructure`.
> The `Api` project (`Program.cs`) acts as the **Composition Root**, referencing `Infrastructure` solely to invoke `builder.Services.AddInfrastructureServices(builder.Configuration)` at startup. To prevent developers from accidentally referencing `Infrastructure` types inside `Api` endpoints, mark concrete classes in `Infrastructure` as `internal`.

**Q3: When is full 4-project Clean Architecture the WRONG choice for a .NET service?**
> **Model Answer:**
> Full 4-project Clean Architecture is overkill when:
> 1. **CRUD / Data-Driven Microservices:** If 90% of endpoints simply validate a payload and read/write rows to a database with minimal domain invariants, separating Domain, Application, Infrastructure, and Api creates pure pass-through ceremony ("Lasagna Architecture").
> 2. **Small Single-Bounded-Context Services:** Splitting a 3,000-line service across 4 `.csproj` files slows MSBuild compilation and forces 5-file edits for every column addition. A single-project **Vertical Slice Architecture** is far more productive.

#### Practice Exercises

1. **Pure Domain Persistence Mapping:** Create an `Order` aggregate root in a class library with zero NuGet packages containing a strongly-typed `readonly record struct OrderId(Guid Value)`, a `Money` value object, and a private `List<OrderLine> _lines`. In a separate `Infrastructure` class library, write the complete `IEntityTypeConfiguration<Order>` using EF Core 8 Complex Types (`ComplexProperty`) for `Money` and value converters for `OrderId`.
2. **Whiteboard Drill:** Practice delivering the 60-Second Clean Architecture Whiteboarding Script aloud while drawing the compile-time vs runtime arrows until you can explain the Dependency Inversion seam clearly in under 60 seconds.

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

### 9.2 End-to-End Vertical Slice Implementation in C# 12

In Vertical Slice Architecture (popularized by Jimmy Bogard), **high cohesion within a feature slice** supersedes artificial horizontal layer separation. Instead of jumping across 6 projects to trace a single HTTP `POST /api/orders` call, an entire feature can live in a single cohesive file (`Features/Orders/PlaceOrder.cs`) using `static class` scoping:

```csharp
// File: Features/Orders/PlaceOrder.cs
using FluentValidation;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.HttpResults;
using Microsoft.AspNetCore.Routing;
using Microsoft.EntityFrameworkCore;

namespace Ordering.Api.Features.Orders;

public static class PlaceOrder
{
    // 1. Request / Command Contract (Scoped to this slice)
    public sealed record Command(
        Guid CustomerId,
        string Currency,
        IReadOnlyList<OrderLineDto> Lines);

    public sealed record OrderLineDto(string Sku, int Quantity, decimal UnitPrice);

    public sealed record Response(Guid OrderId, decimal TotalAmount, DateTimeOffset CreatedAtUtc);

    // 2. Slice-Specific Input Validator
    public sealed class Validator : AbstractValidator<Command>
    {
        public Validator()
        {
            RuleFor(x => x.CustomerId).NotEmpty();
            RuleFor(x => x.Currency).Length(3);
            RuleFor(x => x.Lines).NotEmpty();
            RuleForEach(x => x.Lines).ChildRules(line =>
            {
                line.RuleFor(l => l.Sku).NotEmpty().MaximumLength(32);
                line.RuleFor(l => l.Quantity).GreaterThan(0);
                line.RuleFor(l => l.UnitPrice).GreaterThan(0m);
            });
        }
    }

    // 3. Minimal API Endpoint Registration
    public static void MapEndpoint(IEndpointRouteBuilder app)
    {
        app.MapPost("/api/orders", HandleAsync)
           .WithName("PlaceOrder")
           .WithTags("Orders");
    }

    // 4. Handler (No MediatR ceremony required — direct DI into Minimal API handler)
    public static async Task<Results<Created<Response>, ValidationProblem, Conflict<string>>> HandleAsync(
        Command command,
        IValidator<Command> validator,
        OrderingDbContext dbContext,
        TimeProvider timeProvider,
        CancellationToken ct)
    {
        var validation = await validator.ValidateAsync(command, ct);
        if (!validation.IsValid)
        {
            return TypedResults.ValidationProblem(validation.ToDictionary());
        }

        bool hasSuspendedAccount = await dbContext.Customers
            .AsNoTracking()
            .AnyAsync(c => c.Id == command.CustomerId && c.IsSuspended, ct);

        if (hasSuspendedAccount)
        {
            return TypedResults.Conflict("Customer account is suspended and cannot place new orders.");
        }

        // Delegate invariant enforcement to the rich Domain Aggregate
        var order = Order.Create(
            command.CustomerId,
            command.Currency,
            command.Lines.Select(l => new OrderLine(l.Sku, l.Quantity, l.UnitPrice)).ToList(),
            timeProvider.GetUtcNow());

        dbContext.Orders.Add(order);
        await dbContext.SaveChangesAsync(ct);

        var response = new Response(order.Id, order.TotalAmount, order.CreatedAtUtc);
        return TypedResults.Created($"/api/orders/{order.Id}", response);
    }
}
```

#### Sizing Slices & The "Duplication vs Coupling" Rule
- **Never share Request/Response DTOs or Validators across slices.** Even if `CreateOrder` and `UpdateOrderDraft` look 90% identical today, coupling them into a shared `UpsertOrderDto` reintroduces horizontal fragility as soon as their business rules diverge.
- **Where Shared Logic Belongs:** True domain invariants (e.g., `Order.Create(...)`, `Order.Cancel(...)`, `Money` arithmetic) are pushed down into rich **Domain Aggregates and Value Objects**, not copy-pasted across slice handlers.

---

### Section 9 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: If Vertical Slice Architecture discourages shared service layers between slices, how do you prevent two slices (`PlaceOrder` and `ApplyPromoCode`) from duplicating core business rules?**
> **Model Answer:**
> Vertical Slice Architecture eliminates **shared orchestration layers** (`OrderService`, `GenericRepository`), **not** the shared **Domain Model**. When two slices share a genuine domain invariant (such as calculating order totals or enforcing credit limits), you refactor by **pushing behavior down into the Domain Entity, Aggregate Root, or Value Object** (`order.ApplyCoupon(coupon)`).
> Duplication is preferred *only* for slice-specific DTOs, query projections, and input validators, where coupling two features together for incidental structural similarity causes fragile cross-feature regressions.

**Q2: Why do many senior .NET architects combine Vertical Slice Architecture with Minimal APIs and drop MediatR entirely?**
> **Model Answer:**
> Historically, MVC Controllers became bloated `500`-line classes holding 12 endpoints, so teams introduced MediatR to split each controller action into an isolated `IRequestHandler` class.
> In .NET 8/9 Minimal APIs, each endpoint (`PlaceOrder.HandleAsync`) is already a standalone method in its own feature file with first-class DI parameter binding, `IEndpointFilter` pipelines (replacing `IPipelineBehavior`), and compile-time `TypedResults` OpenAPI generation. Adding MediatR on top of a single-file Minimal API slice just adds an extra `Send()` hop, heap allocation, and broken IDE "Go To Implementation" with zero architectural benefit.

#### Practice Exercises

1. **Read-Slice Optimization:** Implement a `GetOrderSummary.cs` vertical slice alongside `PlaceOrder.cs` that uses an EF Core `.AsNoTracking().Where(...).Select(...)` projection (or Dapper query) to return `Results<Ok<OrderSummaryResponse>, NotFound>` in a single file without touching the `Order` aggregate's write methods.
2. **Endpoint Filter Pipeline:** Replace `ValidationBehavior<TRequest, TResponse>` with an ASP.NET Core `IEndpointFilter` (`ValidationEndpointFilter<TRequest>`) and attach it to a route group so every vertical slice in the group automatically validates its request payload before entering `HandleAsync`.

---

## Section 10 — Modular Monolith Architecture & Boundary Enforcement

### 10.1 Module Encapsulation & Automated Architecture Tests

A **Modular Monolith** organizes a single deployment unit into strictly decoupled modules (e.g., `Billing`, `Catalog`, `Identity`).
Modules communicate exclusively through public interfaces and asynchronous domain events; they never share database tables or reference each other's internal classes.

**Boundary policy versus universal rule:** The strict isolation used here is a deliberate design option, particularly useful when teams or modules need independent evolution. A modular monolith can also use explicit synchronous contracts. Sharing a database server is not the same as sharing ownership of every table. If reporting uses approved cross-schema views, document that exception instead of pretending the dependency does not exist.

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

### 10.2 Enforcing Module Boundaries with `ArchUnitNET` & In-Process Integration Events

#### Physical & Logical Module Isolation
In a Modular Monolith, each module (`Catalog`, `Ordering`, `Billing`) owns:
1. **Its own internal implementation assembly** (`Modules.Ordering.Internal.csproj`) where all entities, `DbContext`, and handlers are marked `internal sealed` (exposing internals only to `Modules.Ordering.UnitTests` via `[assembly: InternalsVisibleTo("Modules.Ordering.UnitTests")]`).
2. **Its own public contract assembly** (`Modules.Ordering.Contracts.csproj`) containing only public Integration Event records (`OrderPlacedIntegrationEvent`) and narrow module facade interfaces (`IOrderingModuleContract`) if synchronous queries are strictly necessary.
3. **Its own database schema** (`ordering.orders` vs `billing.invoices` in PostgreSQL/SQL Server) with **zero cross-schema foreign keys or SQL `JOIN`s**.

#### Enforcing Module Isolation in CI with `ArchUnitNET`
Relying on human code reviews to prevent a developer from adding a project reference or namespace import between `Billing` and `Catalog` always fails under deadline pressure. `ArchUnitNET` verifies module isolation on every pull request:

```csharp
using ArchUnitNET.Domain;
using ArchUnitNET.Loader;
using ArchUnitNET.xUnit;
using Xunit;
using static ArchUnitNET.Fluent.ArchRuleDefinition;

public sealed class ModularMonolithArchitectureTests
{
    private static readonly Architecture SystemArchitecture = new ArchLoader()
        .LoadAssemblies(
            typeof(OrderingModuleMarker).Assembly,
            typeof(BillingModuleMarker).Assembly,
            typeof(CatalogModuleMarker).Assembly)
        .Build();

    private readonly IObjectProvider<IType> _orderingInternalTypes =
        Types().That().ResideInNamespace("Enterprise.Modules.Ordering.*", useRegularExpressions: true)
               .And().DoNotResideInNamespace("Enterprise.Modules.Ordering.Contracts")
               .As("Ordering Internal Module");

    private readonly IObjectProvider<IType> _billingModuleTypes =
        Types().That().ResideInNamespace("Enterprise.Modules.Billing.*", useRegularExpressions: true)
               .As("Billing Module");

    [Fact]
    public void BillingModule_MustNotDependOn_OrderingInternalTypes()
    {
        // Billing may ONLY reference Enterprise.Modules.Ordering.Contracts
        IArchRule rule = Types().That().Are(_billingModuleTypes)
            .Should().NotDependOnAny(_orderingInternalTypes)
            .Because("Modules in a Modular Monolith must communicate strictly via public Contracts or Integration Events.");

        rule.Check(SystemArchitecture);
    }

    [Fact]
    public void DomainEntities_MustBeSealedOrAbstract_AndHavePrivateParameterlessConstructor()
    {
        IArchRule rule = Classes().That().AssignTo(typeof(AggregateRoot<>))
            .And().AreNotAbstract()
            .Should().BeSealed()
            .Because("Concrete Aggregate Roots must be sealed to protect invariant encapsulation.");

        rule.Check(SystemArchitecture);
    }
}
```

#### In-Process Integration Event Bus (Eventual Consistency Across Modules)
When `Ordering` completes an order, it does **not** inject `BillingDbContext`. Instead, `Ordering` persists an `OutboxMessage` in the `ordering` schema, and a background worker publishes `OrderPlacedIntegrationEvent` to an in-process `Channel<T>` (or MassTransit In-Memory/RabbitMQ transport) consumed asynchronously by `Billing`:

```csharp
// In Modules.Ordering.Contracts:
public sealed record OrderPlacedIntegrationEvent(
    Guid EventId,
    Guid OrderId,
    Guid CustomerId,
    decimal TotalAmount,
    string Currency,
    DateTimeOffset OccurredAtUtc);

// In Modules.Billing.Internal (Idempotent Consumer):
internal sealed class OrderPlacedBillingConsumer(BillingDbContext billingDb)
{
    public async Task ConsumeAsync(OrderPlacedIntegrationEvent evt, CancellationToken ct)
    {
        // Idempotency guard (Inbox pattern)
        if (await billingDb.ProcessedEvents.AnyAsync(e => e.EventId == evt.EventId, ct))
            return;

        var invoice = Invoice.CreateForOrder(evt.OrderId, evt.CustomerId, evt.TotalAmount, evt.Currency);
        billingDb.Invoices.Add(invoice);
        billingDb.ProcessedEvents.Add(new ProcessedIntegrationEvent(evt.EventId, DateTimeOffset.UtcNow));

        await billingDb.SaveChangesAsync(ct);
    }
}
```

**Concurrency requirement for the inbox example:** `AnyAsync` is only a fast duplicate check, not a lock. Concurrent deliveries can both see no existing marker. Make the event identifier unique in the inbox and commit the marker with the invoice in one transaction. Handle the specific duplicate-key outcome as a duplicate only after confirming the earlier processing committed; do not classify every `DbUpdateException` as success. Add a unique business key such as OrderId if the domain permits only one invoice per order, independently of event IDs.

#### What Architecture Tests Cannot Prove

Static dependency tests can reject a forbidden assembly reference, but they cannot reliably identify table names embedded in SQL strings, reflection-based calls, an HTTP call back into the same application, or an event schema that leaks another module's internals. A green architecture test is evidence about the rule it checks, not proof of independence.

Combine compiler visibility and dependency tests with contract review, database permissions where appropriate, and integration tests of real use cases. A useful change test is: "Can Billing alter its private storage model without rebuilding Catalog's business assumptions?" A shared `Common` library containing every module's entities usually defeats that goal even when project references look tidy.

**Completion check:** For one proposed boundary, identify its public contract, state owner, failure semantics, and enforcement mechanism. Explain one restriction that the compiler catches and one that requires a runtime test or operational control.

---

### Section 10 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: Why is a Modular Monolith almost always superior to Microservices for a new or mid-sized enterprise product, and what ensures a Modular Monolith doesn't decay into a "Big Ball of Mud"?**
> **Model Answer:**
> Microservices introduce massive distributed systems taxes from day one: network serialization latency, distributed tracing complexity, partial failure cascades, multi-repo CI/CD coordination, and distributed saga orchestration. If a team cannot maintain clean module boundaries in a single process, splitting it across network boundaries simply produces a **Distributed Monolith**—the worst of both worlds.
> A Modular Monolith keeps deployment, debugging, and refactoring single-process while enforcing logical autonomy through three hard guardrails:
> 1. **Compiler Visibility:** `internal` classes + separate `.Contracts` assemblies.
> 2. **CI Fitness Functions:** `ArchUnitNET` / `NetArchTest` rules failing the build on unauthorized cross-module dependencies.
> 3. **Database Schema Isolation:** Separate `DbContext` per module (`ordering.*`, `billing.*`) with distinct connection strings or schema permissions prohibiting cross-module SQL joins.

**Q2: How do you handle a UI screen that needs to display Order details alongside Catalog product thumbnails and Billing invoice statuses in a Modular Monolith where cross-module SQL `JOIN`s are forbidden?**
> **Model Answer:**
> There are three architectural patterns, ordered from simplest to most scalable:
> 1. **API / Gateway Composition (In-Memory Join):** An API composition endpoint queries `Ordering`, `Catalog`, and `Billing` via their read contracts in parallel (`Task.WhenAll` over separate connections) and merges the small page of 20 items in memory by `OrderId` / `Sku`.
> 2. **Local Read-Model Cache (Event-Carried State Transfer):** The `Ordering` module subscribes to `ProductUpdatedIntegrationEvent` and `InvoicePaidIntegrationEvent` and maintains a local denormalized read table (`ordering.order_summary_view`) within its own schema.
> 3. **Dedicated Reporting / Read Schema:** For complex analytical grids filtering across modules simultaneously, replicate or project events into a read-only reporting view owned by a dedicated `Reporting` module.

#### Practice Exercises

1. **ArchUnitNET Boundary Suite:** Write an `ArchUnitNET` test that dynamically discovers all top-level module namespaces under `Enterprise.Modules.<ModuleName>` and asserts that no module `A` references any type in `Enterprise.Modules.<ModuleB>.Internal`.
2. **Schema-Isolated DbContext Migration:** Configure two `DbContext` classes (`OrderingDbContext` using `modelBuilder.HasDefaultSchema("ordering")` and `BillingDbContext` using `modelBuilder.HasDefaultSchema("billing")`) sharing a single PostgreSQL database connection string, each maintaining its own isolated `__EFMigrationsHistory` table inside its respective schema.

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

### 11.2 Railway-Oriented Programming (Monadic `Bind`, `Map`, `Tap`, `Match` Extensions in C#)

**Railway-Oriented Programming (ROP)** (coined by Scott Wlaschin) treats a business workflow as a two-track railway: a **Success Track** and a **Failure Track**.
Every step in the pipeline accepts a value on the Success track; if a step fails, the pipeline switches to the Failure track and bypasses all subsequent steps until the terminal `Match()` method translates the outcome into an HTTP response.

```text
Success Track:  [ValidateInput] ---> [CalculatePricing] ---> [PersistOrder] ---> [201 Created]
                      |                     |                      |
Failure Track:        +-------------------->+--------------------->+-----------> [400 / 422 Problem]
```

#### Complete Async & Sync Monadic Extensions (`Bind`, `Map`, `Tap`, `Match`)
```csharp
public static class ResultExtensions
{
    // MAP (Functor): Transforms TIn -> TOut when on the Success track
    public static Result<TOut, TError> Map<TIn, TOut, TError>(
        this Result<TIn, TError> result,
        Func<TIn, TOut> mapper) =>
        result.IsSuccess
            ? Result<TOut, TError>.Success(mapper(result.Value))
            : Result<TOut, TError>.Failure(result.Error);

    // BIND (Monad / FlatMap): Chains a fallible operation TIn -> Result<TOut, TError>
    public static Result<TOut, TError> Bind<TIn, TOut, TError>(
        this Result<TIn, TError> result,
        Func<TIn, Result<TOut, TError>> binder) =>
        result.IsSuccess
            ? binder(result.Value)
            : Result<TOut, TError>.Failure(result.Error);

    // ASYNC BIND: Chains an async fallible operation Task<Result<TIn, TError>> -> Task<Result<TOut, TError>>
    public static async Task<Result<TOut, TError>> BindAsync<TIn, TOut, TError>(
        this Result<TIn, TError> result,
        Func<TIn, Task<Result<TOut, TError>>> asyncBinder) =>
        result.IsSuccess
            ? await asyncBinder(result.Value)
            : Result<TOut, TError>.Failure(result.Error);

    // TAP: Executes a side-effect (logging, metrics) on the Success track without altering the value
    public static async Task<Result<TValue, TError>> TapAsync<TValue, TError>(
        this Task<Result<TValue, TError>> resultTask,
        Func<TValue, Task> sideEffect)
    {
        var result = await resultTask;
        if (result.IsSuccess)
        {
            await sideEffect(result.Value);
        }
        return result;
    }

    // MATCH: Terminal fold that forces exhaustive handling of both tracks
    public static async Task<TOut> MatchAsync<TValue, TError, TOut>(
        this Task<Result<TValue, TError>> resultTask,
        Func<TValue, TOut> onSuccess,
        Func<TError, TOut> onFailure)
    {
        var result = await resultTask;
        return result.IsSuccess ? onSuccess(result.Value) : onFailure(result.Error);
    }
}

// End-to-End Functional Pipeline (Zero nested if/try blocks):
public sealed class CheckoutWorkflow(
    IPricingPolicy pricing,
    IOrderRepository repository,
    IAuditLogger audit)
{
    public Task<IResult> ExecuteAsync(CheckoutRequest request, CancellationToken ct) =>
        ValidateRequest(request)
            .Bind(validReq => pricing.QuoteOrder(validReq))
            .BindAsync(quotedOrder => repository.SaveOrderAsync(quotedOrder, ct))
            .TapAsync(savedOrder => audit.LogOrderCreatedAsync(savedOrder.Id, ct))
            .MatchAsync(
                onSuccess: order => Results.Created($"/api/orders/{order.Id}", new { order.Id, order.Total.Amount }),
                onFailure: error => Results.UnprocessableEntity(new { error.Code, error.Description }));

    private static Result<CheckoutRequest, Error> ValidateRequest(CheckoutRequest req) =>
        req.Items.Count == 0
            ? new Error("Order.Empty", "An order must contain at least one item.")
            : req;
}
```

---

### Section 11 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: Explain the difference between `Map` and `Bind` in a functional `Result<T, TError>` pipeline.**
> **Model Answer:**
> - **`Map` (Functor projection):** Takes a function `Func<TIn, TOut>` that **cannot fail** (returns a plain `TOut` value) and wraps its output back into `Result<TOut, TError>`. If you passed a function returning `Result<TOut, TError>` into `Map`, you would get a nested `Result<Result<TOut, TError>, TError>`.
> - **`Bind` (Monadic bind / `SelectMany` in LINQ):** Takes a function `Func<TIn, Result<TOut, TError>>` that **can fail**, flattening the result so the pipeline stays a single-level `Result<TOut, TError>`.

**Q2: When does Railway-Oriented Programming become an anti-pattern in C#?**
> **Model Answer:**
> ROP becomes an anti-pattern when teams force **every trivial local expression** or **truly exceptional infrastructure failure** into `Bind`/`Map` chains:
> 1. **Closure Allocations & Debugging Friction:** Deeply nested lambda chains allocate delegate closures on the heap when capturing local variables, and stepping through 12 chained extension methods in a debugger is harder than reading 4 lines of guard-clause early returns.
> 2. **Swallowing Infrastructure Exceptions:** Unexpected infrastructure crashes (`OutOfMemoryException`, `DbUpdateConcurrencyException`, deadlocks, network socket drops) are **not** business validation errors; catching `Exception` inside `Bind` and turning them into HTTP `400 Bad Request` masks 500-level production outages and prevents transaction rollback middleware from firing.

#### Practice Exercises

1. **LINQ Query Comprehension Syntax for `Result<T, TError>`:** Implement `Select` and `SelectMany` extension methods on `Result<TValue, TError>` so developers can write multi-step railway pipelines using native C# LINQ syntax (`from valid in Validate(req) from quote in Quote(valid) select quote`) without closure nesting.
2. **Exhaustive Discriminated Union Hierarchy:** Model a `ShippingQuoteResult` in pure C# 12 without external NuGet packages using an `abstract record ShippingQuoteResult` with private constructor and nested `sealed record Quoted(Money Cost, int EstimatedDays)`, `sealed record EmbargoedCountry(string IsoCode)`, and `sealed record HazmatRestricted(string Sku)`.

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

### 12.2 Refactoring Walkthrough: Untangling a 2,500-Line `OrderManager` God Class

A classic senior/staff coding and design interview scenario presents a legacy `OrderManager` "God Class" that mixes validation, discount branching, tax calculation, SQL persistence, credit card charging, caching, and email notifications in a single 2,500-line procedural method.

#### BEFORE: The Legacy `OrderManager` God Class (Anti-Pattern)
```csharp
// ANTI-PATTERN: Violates SRP, OCP, DIP; untestable without live SQL, Stripe, and SMTP servers
public class OrderManager
{
    public async Task<Guid> ProcessOrderAsync(OrderDto dto, string customerTier, string paymentProvider)
    {
        using var db = new AppDbContext(); // Hidden dependency (new is glue)

        // 1. Inline procedural discount branching (Violates OCP)
        decimal discount = 0m;
        if (customerTier == "VIP") discount = dto.Total * 0.20m;
        else if (customerTier == "Partner") discount = dto.Total * 0.15m;
        else if (customerTier == "Employee") discount = dto.Total * 0.30m;

        decimal finalAmount = dto.Total - discount;

        // 2. Inline payment gateway branching + hardcoded HTTP calls
        if (paymentProvider == "Stripe")
        {
            using var http = new HttpClient(); // Socket exhaustion bug!
            var resp = await http.PostAsJsonAsync("https://api.stripe.com/v1/charges", new { finalAmount });
            resp.EnsureSuccessStatusCode();
        }
        else if (paymentProvider == "Adyen")
        {
            // 150 lines of Adyen XML/JSON plumbing...
        }

        // 3. Anemic entity mutation
        var entity = new OrderEntity
        {
            Id = Guid.NewGuid(),
            CustomerId = dto.CustomerId,
            TotalAmount = finalAmount,
            Status = "Paid",
            CreatedAt = DateTime.Now // Non-deterministic local clock!
        };
        db.Orders.Add(entity);
        await db.SaveChangesAsync();

        // 4. Synchronous side-effects after DB commit (partial failure risk!)
        using var smtp = new SmtpClient("smtp.corp.local");
        await smtp.SendMailAsync("noreply@corp.local", dto.CustomerEmail, "Order Confirmed", $"Order {entity.Id}");

        return entity.Id;
    }
}
```

#### AFTER: Decomposed Architecture (Rich Aggregate + Strategy + Keyed Adapter + Domain Events)
We systematically untangle `OrderManager` along four clean architectural seams:
1. **Rich Domain Aggregate (`Order`):** Owns invariant enforcement and raises `OrderPaidDomainEvent` (which the `SaveChangesInterceptor` persists to the Transactional Outbox, eliminating synchronous `SmtpClient` calls on the request thread).
2. **Strategy Pattern (`IDiscountStrategy`):** Extracts tier pricing rules into open/closed strategies.
3. **Keyed Port & Adapter (`IPaymentGateway`):** Replaces `new HttpClient()` and `if (paymentProvider == ...)` with Keyed Services backed by `IHttpClientFactory` resilience pipelines.
4. **Decorator (`IdempotentOrderPlacementDecorator`):** Extracts cross-cutting idempotency/telemetry out of the business workflow.

```csharp
// 1. Rich Domain Aggregate (Encapsulates State & Raises Domain Events)
public sealed class Order : AggregateRoot<Guid>
{
    public Guid CustomerId { get; private init; }
    public Money Total { get; private set; }
    public string PaymentReference { get; private set; }
    public DateTimeOffset PaidAtUtc { get; private init; }

    private Order(Guid id, Guid customerId, Money total, string paymentReference, DateTimeOffset paidAtUtc)
        : base(id)
    {
        CustomerId = customerId;
        Total = total;
        PaymentReference = paymentReference;
        PaidAtUtc = paidAtUtc;
    }

    public static Order CreatePaid(
        Guid customerId,
        Money grossTotal,
        Money discount,
        string paymentReference,
        DateTimeOffset nowUtc)
    {
        var netTotal = new Money(Math.Max(0m, grossTotal.Amount - discount.Amount), grossTotal.Currency);
        var order = new Order(Guid.NewGuid(), customerId, netTotal, paymentReference, nowUtc);

        // Side effects (Email, Analytics, Loyalty points) are decoupled via Domain Event!
        order.RaiseDomainEvent(new OrderPaidDomainEvent(
            Guid.NewGuid(), order.Id, customerId, netTotal, nowUtc));

        return order;
    }
}

// 2. Clean, Focused Use-Case Handler (< 30 lines, 100% unit-testable)
public sealed class PlacePaidOrderHandler(
    DiscountCalculator discountCalculator,
    Func<string, IPaymentGateway> paymentGatewayFactory,
    IOrderRepository orderRepository,
    TimeProvider timeProvider)
{
    public async Task<Result<Guid, Error>> HandleAsync(PlaceOrderCommand cmd, CancellationToken ct)
    {
        Money discount = discountCalculator.ApplyDiscount(cmd.CustomerTier, cmd.GrossTotal);
        Money netPayable = new(cmd.GrossTotal.Amount - discount.Amount, cmd.GrossTotal.Currency);

        IPaymentGateway gateway = paymentGatewayFactory(cmd.PaymentProviderKey);
        Result<string, Error> chargeResult = await gateway.ChargeAsync(cmd.CustomerId, netPayable, ct);
        if (chargeResult.IsFailure)
        {
            return chargeResult.Error;
        }

        var order = Order.CreatePaid(
            cmd.CustomerId,
            cmd.GrossTotal,
            discount,
            chargeResult.Value,
            timeProvider.GetUtcNow());

        await orderRepository.AddAsync(order, ct);
        return order.Id;
    }
}
```

---

### Section 12 Review: Interview Questions & Practice Exercises

#### Interview Questions & Model Answers

**Q1: When untangling a 2,500-line legacy God class in production that has zero unit tests, how do you refactor it safely without breaking live traffic?**
> **Model Answer:**
> Never attempt a "Big Bang" rewrite on untested legacy code. Follow Michael Feathers' *Working Effectively with Legacy Code* and the **Strangler Fig** sequence:
> 1. **Establish Characterization Tests (Golden Master):** Capture real production request/response payloads and assert the exact outputs and database state mutations using Testcontainers before changing a single line of logic.
> 2. **Extract Seams without Changing Behavior:** Replace inline `new HttpClient()`, `new AppDbContext()`, and `DateTime.Now` with constructor-injected interfaces (`TimeProvider`, `IPaymentGateway`) defaulted or registered in DI.
> 3. **Sprout & Strangle:** Extract one cohesive responsibility at a time (first the stateless `IDiscountStrategy`, then the `SmtpClient` side-effect into an Outbox event handler) behind a feature flag or shadow-mode comparison before deleting the legacy branch.

**Q2: In an executive or Architecture Review Board (ARB) meeting, how do you defend choosing a Modular Monolith with Vertical Slices over a 12-microservice Clean Architecture proposal?**
> **Model Answer:**
> Frame the argument around **Total Cost of Ownership (TCO), Deployment Velocity, and Change Locality**:
> - **Change Locality:** With Vertical Slices inside a Modular Monolith, 90% of product features touch a single folder in a single repository and deploy atomically.
> - **Operational Efficiency:** We avoid running 12 separate Kubernetes deployments, 12 database clusters, and distributed network sagas while our domain boundaries are still evolving.
> - **Guaranteed Extraction Path:** Because `ArchUnitNET` enforces strict module isolation (`Ordering`, `Billing`, `Catalog`) and each module owns an isolated database schema and communicates via `IntegrationEvents`, any single module that genuinely needs independent horizontal scaling later can be extracted into a standalone microservice in days by swapping the in-process event bus for RabbitMQ/Service Bus.

#### Practice Exercises

1. **God-Class Decomposition Kata:** Take the legacy `OrderManager.ProcessOrderAsync` snippet from Section 12.2 and write 3 unit tests for `PlacePaidOrderHandler` using fake in-memory implementations of `IPaymentGateway`, `IOrderRepository`, and `FakeTimeProvider` (`Microsoft.Extensions.TimeProvider.Testing`), verifying 100% deterministic execution in $< 5\text{ ms}$.
2. **Capstone Architecture Blueprint:** Design the folder structure, `.csproj` dependency graph, and `ArchUnitNET` test suite for a Multi-Tenant Enterprise Billing Engine containing three modules (`Subscriptions`, `UsageMetering`, `Invoicing`), where `UsageMetering` ingests $5{,}000\text{ events/sec}$ via an `ObjectPool`-backed Vertical Slice and publishes hourly rollup integration events to `Invoicing`.

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
