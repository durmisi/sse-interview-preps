# Module 10 — Code Reviews & Engineering Standards

**Senior Software Engineer Academy · Module 10 of 12**

> **Learning objective:** Master the art, science, psychology, and organizational leadership of code reviews and engineering standards. Develop senior-level proficiency in conducting structured, high-impact code reviews: prioritizing architectural invariants, security vulnerabilities (OWASP), concurrency deadlocks, and performance pitfalls over cosmetic syntax. Master authoring atomic pull requests, giving constructive feedback with Conventional Comments, resolving technical disagreements, automating standards via `.editorconfig` and Roslyn analyzers, and reviewing architectural RFCs.
>
> **Audience:** Experienced C#/.NET engineers preparing for Senior, Lead, and Staff technical interviews. Real-world pull request experience is assumed; empirical research on review effectiveness, secure code review methodology, and team quality culture are taught with rigorous precision.
>
> **Version note:** Tooling and standards reference modern .NET (.NET 8 LTS and .NET 9), C# 12/13 nullable reference types, Roslyn analyzers, `dotnet format`, Git branch protection, and Conventional Comments.

## How to use this module

Every section in Part II provides comprehensive senior-level instruction:
1. **Review Science & Methodology:** Empirical review research (Bacchelli & Bird), cognitive limits, and the 6-stage review hierarchy.
2. **C#/.NET Production Checklists:** Concurrency traps, async hazards, security vulnerabilities, and memory leaks.
3. **Enterprise Production Scenarios:** Flawed PR walkthroughs, PR deadlock disputes, and resolving reviewer bikeshedding.
4. **Trade-offs, Alternatives & Failure Modes:** When async PR reviews fail and pair programming is superior; balancing review speed with thoroughness.
5. **What a Senior Engineer Is Expected to Know:** Mid-level vs Senior/Staff code review standards.
6. **Interview Questions with Model Answers:** Real interview questions with structured, senior-level responses.
7. **Practical Exercises:** Full code review simulations with seeded enterprise defects.

## Progress tracker

| Section | Topic | Status |
|---|---|---|
| Section 1 | The Purpose, Psychology & Science of Code Review | Complete |
| Section 2 | Authoring Great Pull Requests & Atomic Changes | Complete |
| Section 3 | Review Methodology & Cognitive Prioritization Hierarchy | Complete |
| Section 4 | Correctness, Concurrency & Reliability Review in C# | Complete |
| Section 5 | Design, Maintainability & Architectural Boundary Review | Complete |
| Section 6 | Secure Code Review & OWASP Top 10 for .NET | Complete |
| Section 7 | Performance, Memory & Scalability Review | Complete |
| Section 8 | Test Suite Review & Verification Quality | Complete |
| Section 9 | Giving Constructive Feedback & Conventional Comments | Complete |
| Section 10 | Receiving Feedback, Disagreements & Escalation Protocols | Complete |
| Section 11 | Engineering Standards, Tooling & Automated Quality Gates | Complete |
| Section 12 | Documentation Standards & RFC Design Reviews | Complete |
| Section 13 | Senior Scenarios & Capstone PR Review Walkthrough | Complete |

**Current position:** Full curriculum complete. Ready for self-study, exercises, and interview drills.

## Module boundaries

- **This module owns:** Pull request authoring, review methodology, feedback psychology, secure code review, .NET correctness auditing, automated analyzers (`.editorconfig`, Roslyn), and engineering documentation standards.
- **Related topics owned by other modules:**
  - Object-oriented mechanics, SOLID principles, and clean code heuristics → Module 01
  - Memory allocations, GC pauses, and CoreCLR concurrency primitives → Module 03
  - In-process design patterns, CQRS, and Clean Architecture dependencies → Module 04
  - Relational database indexing, SQL tuning, and transactions → Module 05
  - HTTP protocols, REST conventions, and API security → Module 06
  - Test taxonomy, unit/integration testing, and Testcontainers → Module 09
  - CI/CD build pipelines, automated PR verification, and Git workflows → Module 11
  - Team leadership, mentoring, and technical communication → Module 12

---

# Part I — Complete Curriculum

## Section 1 — The Purpose, Psychology & Science of Code Review
- 1.1 The Primary Goals of Code Review: Defect detection vs Knowledge sharing vs Team design alignment vs Mentoring; Empirical research (Bacchelli & Bird, ICSE 2013; Microsoft/Google studies): finding that the greatest business value of review is knowledge transfer, collective ownership, and maintainability.
- 1.2 Cognitive Limits of Reviewers: The SmartBear/Cisco study on review effectiveness: defect density drops precipitously when reviewing more than 400 lines of code (LOC) at a time, or reviewing for longer than 60 consecutive minutes.
- 1.3 What Code Reviews Are NOT For: Catching formatting and style discrepancies (must be 100% automated); asserting personal stylistic preferences; exerting gatekeeper dominance.

## Section 2 — Authoring Great Pull Requests & Atomic Changes
- 2.1 The Small PR Imperative: Why PRs under 250 LOC receive significantly deeper reviews and ship with vastly fewer production defects.
- 2.2 Stacked Pull Requests (Branch Stacking): Decomposing large, multi-day features into sequential, independent reviewable slices.
- 2.3 The Anatomy of an Exemplary PR Description: The 6 essential elements: Context/Why, What changed, How it was tested, UI Screenshots/Recordings, Migration/Rollback considerations, Risk assessment.
- 2.4 Author Pre-Flight Hygiene: Performing a disciplined self-review in the diff viewer before requesting review; squashing messy "WIP" commits; linking work items.

## Section 3 — Review Methodology & Cognitive Prioritization Hierarchy
- 3.1 The 6-Level Review Hierarchy:
  - Level 1: Architecture, Business Context & Invariants (P0).
  - Level 2: Correctness, Concurrency & Reliability (P0).
  - Level 3: Security & Data Privacy (P0).
  - Level 4: Performance, Scalability & Resource Disposal (P1).
  - Level 5: Test Quality & Observability (P1).
  - Level 6: Readability, Naming & Style (P2).
- 3.2 Review Latency & Team SLAs: Why slow PR turnaround destroys team throughput; establishing 4-hour to 24-hour team review SLAs.
- 3.3 Synchronous vs Asynchronous Reviews: When pairing or a 15-minute live screen-share is vastly superior to endless asynchronous comment ping-pong.

## Section 4 — Correctness, Concurrency & Reliability Review in C#
- 4.1 Concurrency Traps: Capturing mutable state across threads, non-thread-safe collections (`Dictionary<TKey, TValue>` accessed concurrently), race conditions in counters (missing `Interlocked`).
- 4.2 Resource Disposal: Missing `using` / `Dispose()` on unmanaged handles, streams, and database connections; missing `await using` on `IAsyncDisposable`.
- 4.3 Asynchronous Pitfalls: Sync-over-async (`.Result`, `.Wait()`, `.GetAwaiter().GetResult()`) risking ThreadPool starvation; `async void` crashing the process; forgetting to propagate `CancellationToken`.
- 4.4 Nullability & Invariants: Suppressing Nullable Reference Types with `!` without runtime validation; passing raw `null` into domain models.
- 4.5 Numeric & Time Pitfalls: Using `double` or `float` for financial currency instead of `decimal`; using `DateTime.Now` instead of `DateTimeOffset.UtcNow` or `TimeProvider`.

## Section 5 — Design, Maintainability & Architectural Boundary Review
- 5.1 Encapsulation Review: Detecting Anemic Domain Models with public property setters; verifying domain invariants are protected by methods.
- 5.2 Dependency & Coupling Review: Checking for circular references, leaky abstractions (`IQueryable<T>` returned across boundaries), and compliance with the Dependency Rule.
- 5.3 Third-Party Dependency Audit: Scrutinizing newly introduced NuGet packages: maintenance activity, licensing (MIT/Apache vs GPL/AGPL), vulnerability history, and transitive dependency bloat.

## Section 6 — Secure Code Review & OWASP Top 10 for .NET
- 6.1 Injection Vulnerabilities: Detecting SQL injection in raw SQL or Dapper string interpolations (`$"SELECT * FROM Users WHERE Name = '{name}'"` vs parameterized queries).
- 6.2 Broken Object Level Authorization (BOLA/IDOR): Verifying every query filters by the authenticated user's `TenantId` or `UserId`.
- 6.3 Mass Assignment (Over-Posting): Ensuring endpoints bind to strict DTOs rather than directly updating EF Core database entities.
- 6.4 Sensitive Data Exposure: Preventing plain-text passwords, tokens, API keys, or credit cards from being logged in Serilog / Application Insights.

## Section 7 — Performance, Memory & Scalability Review
- 7.1 Allocation Hot-Paths: Unnecessary string concatenation in loops; closure captures in high-frequency LINQ lambdas; boxing value types.
- 7.2 Database Query Scrutiny: Detecting N+1 query patterns; unindexed queries; missing `AsNoTracking()` on read-only EF Core queries.
- 7.3 Unbounded Collections: Endpoints returning unpaginated database tables (`context.Orders.ToListAsync()`); missing size bounds on in-memory caches.

## Section 8 — Test Suite Review & Verification Quality
- 8.1 Evaluating Test Assertions: Rejecting tests that assert non-null without verifying actual business state; checking for over-mocking.
- 8.2 Test Determinism: Flagging tests that use `Thread.Sleep()`, connect to shared mutable staging databases, or rely on system clocks.

## Section 9 — Giving Constructive Feedback & Conventional Comments
- 9.1 The Conventional Comments Framework:
  - `issue (blocking):` Must be resolved before merge.
  - `suggestion:` Concrete alternative proposed; author has discretion.
  - `question:` Seeking clarification or architectural context.
  - `nit:` Trivial cleanup; non-blocking.
  - `praise:` Highlighting elegant, clean, or well-tested implementations.
- 9.2 The Psychology of Critique: Phrasing comments as inquiries and trade-offs rather than absolute demands; fostering psychological safety.
- 9.3 Combating Bikeshedding (Parkinson's Law of Triviality): Intervening when reviewers spend 80% of comments debating variable names or whitespace.

## Section 10 — Receiving Feedback, Disagreements & Escalation Protocols
- 10.1 Ego Depersonalization: "You are not your code"; receiving critique as an opportunity for system improvement.
- 10.2 The 3-Comment Rule: If an asynchronous discussion exceeds 3 back-and-forth exchanges without resolution, immediately jump on a 5-minute huddle.
- 10.3 Disagree and Commit: When to compromise gracefully; escalating true architectural standoffs to the Lead/Staff Engineer via Architecture Decision Records (ADRs).

## Section 11 — Engineering Standards, Tooling & Automated Quality Gates
- 11.1 `.editorconfig` as Team Law: Codifying formatting, naming conventions, and Roslyn diagnostic severities in source control.
- 11.2 Treating Warnings as Errors: `<TreatWarningsAsErrors>true</TreatWarningsAsErrors>` in `.csproj` / `Directory.Build.props`.
- 11.3 Automated Formatting & Static Analysis in CI: Running `dotnet format --verify-no-changes`, SonarQube, and CodeQL security analyzers on PR builds.
- 11.4 CODEOWNERS & Branch Protection: Enforcing required senior reviewers on core domain and infrastructure paths.

## Section 12 — Documentation Standards & RFC Design Reviews
- 12.1 Living Documentation: Self-documenting code, clean README files, and XML docs for public APIs.
- 12.2 Reviewing Request for Comments (RFCs): Evaluating high-level design documents *before* a single line of code is written.

## Section 13 — Senior Scenarios & Capstone PR Review Walkthrough
- 13.1 Capstone Scenario: End-to-end review of a complex enterprise C# Pull Request with 10 hidden defects across security, concurrency, performance, and domain invariants.

---

# Part II — Lessons

## Section 1 — The Purpose, Psychology & Science of Code Review

### 1.1 The Science of Code Review: Empirical Findings

The landmark study by Alberto Bacchelli and Christian Bird (*Expectations, Outcomes, and Challenges of Modern Code Review*, ICSE 2013) surveyed engineers at Microsoft across hundreds of teams:
- **Finding 1:** While developers believe the primary purpose of code review is finding defects, in practice, **finding bugs accounts for a minority of review value**.
- **Finding 2:** The highest value outcomes of modern code review are:
  1. **Knowledge Transfer:** Educating teammates on system internals and architectural patterns.
  2. **Alternative Solutions:** Discovering cleaner, more maintainable design approaches.
  3. **Shared Code Ownership:** Eliminating single points of failure (bus factor).
  4. **Maintainability & Readability:** Ensuring code can be understood and maintained by someone else 2 years later.

### 1.2 Cognitive Limits: The 400-Line Rule

Research conducted across Cisco and SmartBear systems proved:
- Reviewers examining **fewer than 200–400 lines of code** at a time find roughly **70–90% of defects**.
- As review size exceeds **500–1,000 lines of code**, defect density drops to near zero!
- Beyond 400 lines, reviewers experience **cognitive exhaustion**, switching from deep analytical scrutiny to superficial rubber-stamping ("Looks good to me / LGTM").
*Senior Engineering Rule:* **Never submit a 2,000-line pull request. Break it into atomic, reviewable stacked branches.**

---

## Section 3 — Review Methodology & Cognitive Prioritization Hierarchy

### 3.1 The 6-Level Review Hierarchy

When reviewing a pull request, follow a top-down cognitive hierarchy. Never start by commenting on variable names!

```text
[ LEVEL 1: Architecture & Invariants (P0) ]
  Does this solve the business problem? Are domain invariants protected? Does it violate clean architecture boundaries?
       |
[ LEVEL 2: Correctness & Concurrency (P0) ]
  Are there race conditions? Deadlocks? Async sync-over-async? Unhandled edge cases?
       |
[ LEVEL 3: Security & Data Privacy (P0) ]
  Is there BOLA/IDOR? SQL Injection? Unsanitized inputs? PII logged in plain text?
       |
[ LEVEL 4: Performance & Resource Safety (P1) ]
  Are there N+1 queries? Missing using/Dispose? Unbounded collections? Hot-path allocations?
       |
[ LEVEL 5: Test Verification & Observability (P1) ]
  Do tests assert real behavior or just implementation details? Are logs and metrics structured?
       |
[ LEVEL 6: Readability & Naming (P2) ]
  Are names intention-revealing? Is nesting flat? (Note: Formatting must be automated away by tooling!)
```

---

## Section 6 — Secure Code Review & OWASP Top 10 for .NET

### 6.1 Spotting Vulnerabilities in PR Diffs

#### 1. SQL Injection via String Interpolation
```csharp
// FLAWED PR DIFF
// Reviewer must FLAG IMMEDIATELY as Blocking Security Issue!
public async Task<List<User>> SearchUsersAsync(string searchTerm)
{
    // DANGER: Raw SQL interpolation allows SQL Injection!
    // An attacker passing "admin'; DROP TABLE Users;--" executes arbitrary SQL!
    return await _db.Database
        .SqlQueryRaw<User>($"SELECT * FROM Users WHERE Name LIKE '%{searchTerm}%'")
        .ToListAsync();
}

// SECURED REPLACEMENT: Parameterized query
public async Task<List<User>> SearchUsersAsync(string searchTerm)
{
    return await _db.Users
        .Where(u => EF.Functions.Like(u.Name, $"%{searchTerm}%"))
        .AsNoTracking()
        .ToListAsync();
}
```

#### 2. Mass Assignment (Over-Posting)
```csharp
// FLAWED PR DIFF: Endpoint binds directly to database entity!
app.MapPut("/api/users/{id}", async (Guid id, User updatedUser, AppDbContext db) =>
{
    // DANGER: Attacker includes JSON payload: { "IsAdmin": true, "AccountBalance": 1000000 }
    // The entity updates ALL properties including sensitive administrative fields!
    db.Users.Update(updatedUser);
    await db.SaveChangesAsync();
    return Results.Ok();
});

// SECURED REPLACEMENT: Bind to explicit, validated DTO
app.MapPut("/api/users/{id}", async (Guid id, UpdateUserProfileDto dto, AppDbContext db) =>
{
    var user = await db.Users.FindAsync(id);
    if (user is null) return Results.NotFound();

    user.UpdateProfile(dto.DisplayName, dto.PhoneNumber); // Explicit domain method!
    await db.SaveChangesAsync();
    return Results.Ok();
});
```

---

## Section 9 — Giving Constructive Feedback & Conventional Comments

### 9.1 The Conventional Comments Framework

Ambiguous review comments ("Why did you do this?", "This is bad") trigger defensive reactions and waste time.
The **Conventional Comments** specification standardizes review labels:

```text
format: <label> [decorations]: <subject>

[discussion]
```

- **`issue (blocking):`** A critical defect, security vulnerability, or invariant violation that must be resolved prior to merging.
  *Example:* `issue (blocking): Calling .Result on this task will cause ThreadPool starvation under load. Please await the task asynchronously.`
- **`suggestion:`** Proposing a cleaner or more idiomatic alternative.
  *Example:* `suggestion: We can use C# 12 collection expressions here: var list = []; instead of new List<string>().`
- **`question:`** Seeking clarification without implying the code is wrong.
  *Example:* `question: I see we disabled tracking on this query. Do we anticipate mutating these entities later in the request?`
- **`nit:`** Trivial cosmetic comment; explicitly non-blocking.
  *Example:* `nit: Parameter name 'usr' could be renamed to 'user' for consistency with our naming conventions.`
- **`praise:`** Commending exceptional engineering.
  *Example:* `praise: This benchmark comparing the Span parsing against Regex is fantastic. Clear, verifiable data!`

---

## Section 13 — Senior Scenarios & Capstone PR Review Walkthrough

### 13.1 Capstone Scenario: Auditing a Flawed Enterprise PR

```csharp
// PULL REQUEST SUBMISSION: ProcessPaymentHandler.cs
public class ProcessPaymentHandler
{
    private static List<PaymentRecord> _recentPayments = new List<PaymentRecord>(); // Bug 1: Unbounded static list (Memory Leak)
    private readonly AppDbContext _context;

    public ProcessPaymentHandler(AppDbContext context) => _context = context;

    public async Task Handle(Guid orderId, decimal amount, string userEmail)
    {
        // Bug 2: Missing CancellationToken propagation
        var order = _context.Orders.Include(o => o.Lines).FirstOrDefault(o => o.Id == orderId); // Bug 3: Synchronous FirstOrDefault blocks thread!

        if (order != null)
        {
            // Bug 4: Invariant violation: Mutating status directly (Anemic model)
            order.Status = "Paid";
            order.PaidAmount = amount;

            // Bug 5: Concurrency race condition on non-thread-safe collection!
            _recentPayments.Add(new PaymentRecord { OrderId = orderId, Amount = amount });

            // Bug 6: Socket exhaustion: new HttpClient instantiated per request!
            using var client = new HttpClient();
            var response = client.PostAsync("https://gateway.internal/charge", new StringContent("amount=" + amount)).Result; // Bug 7: Sync-over-async .Result deadlock!

            // Bug 8: Logging sensitive data in plain text!
            Console.WriteLine($"Processed payment for user: {userEmail} with card amount: {amount}");

            await _context.SaveChangesAsync();
        }
    }
}
```

#### Senior Model Review Response:
1. `issue (blocking):` Line 18 calls `client.PostAsync(...).Result`. This is a sync-over-async call that blocks a ThreadPool thread and risks deadlocks and starvation under peak load. Please refactor to `await client.PostAsync(...)`.
2. `issue (blocking):` Line 17 creates `new HttpClient()`. This causes socket exhaustion. Please inject `IHttpClientFactory` or a typed client.
3. `issue (blocking):` Line 14 appends to `static List<PaymentRecord> _recentPayments`. `List<T>` is not thread-safe and will throw `IndexOutOfRangeException` or corrupt memory under concurrent requests. Furthermore, this list grows unbounded, creating a permanent memory leak.
4. `issue (blocking):` Line 9 calls `.FirstOrDefault()` synchronously on the database context. Please use `await _context.Orders.FirstOrDefaultAsync(..., ct)`.
5. `issue (blocking):` Line 21 logs `userEmail` and payment details to standard console output. Please use structured logging with `ILogger` and ensure sensitive customer PII is sanitized.
6. `suggestion:` Line 11 mutates `order.Status = "Paid"` directly. Consider encapsulating this in a domain method `order.MarkAsPaid(amount)` to enforce business invariants.

---

# Part III — Interview Readiness

## 1. Mid-Level vs Senior-Level Code Review Comparison

| Topic | Mid-Level Reviewer Behavior | Senior / Staff-Level Reviewer Behavior |
|---|---|---|
| **Review Focus** | Spends 80% of comments on variable names, formatting, and stylistic quirks (bikeshedding). | Focuses on P0 architectural boundaries, domain invariant protection, race conditions, security vulnerabilities, and memory leaks. |
| **Feedback Tone** | Uses blunt, prescriptive commands ("Change this", "Wrong pattern"). | Uses the Conventional Comments framework (`issue:`, `suggestion:`, `question:`, `praise:`); explains the *why* and cites trade-offs. |
| **Review Size** | Attempts to review 2,500-line PRs in one sitting, eventually skimming and typing "LGTM". | Enforces the 400-line rule; guides authors on branch stacking; requests live pairing sessions for large, ambiguous architectural features. |
| **Disagreements** | Engages in endless back-and-forth comment debates across multiple days. | Enforces the 3-Comment Rule: after 3 exchanges, hops on a 5-minute huddle; documents architectural decisions in ADRs; practices "Disagree and Commit". |
| **Tooling & Standards** | Manually reviews code against personal preferences. | Automates formatting and static analysis via `.editorconfig`, Roslyn analyzers, and CI quality gates; automates nits away so humans review architecture. |

---

## 2. Rapid-Fire Revision Sheet (50 Senior-Level Truths)

1. Empirical research (Bacchelli & Bird) proves that code review's greatest value is knowledge transfer and maintainability, not defect detection.
2. Defect detection density drops sharply when reviewing pull requests larger than 400 lines of code.
3. Reviewer fatigue sets in after 60 consecutive minutes of reviewing; taking breaks restores defect-finding efficacy.
4. Style and formatting debates must be automated away using `.editorconfig` and `dotnet format` in CI pipelines.
5. Large features should be submitted as Stacked Pull Requests (independent, reviewable atomic branches).
6. An exemplary PR description details the business context (Why), what changed, testing evidence, and rollback plans.
7. Authors should perform a disciplined self-review in the diff viewer before assigning teammates to review.
8. The 6-stage review hierarchy prioritizes Architecture $	o$ Correctness $	o$ Security $	o$ Performance $	o$ Tests $	o$ Readability.
9. Long PR turnaround latency creates merge conflicts and destroys team deployment frequency.
10. The Conventional Comments specification categorizes feedback: `issue (blocking)`, `suggestion`, `question`, `nit`, `praise`.
11. Constructive code reviews frequently include praise for well-designed, clean, or thoroughly tested code.
12. Bikeshedding (Parkinson's Law of Triviality) is the tendency to spend disproportionate time debating trivial details.
13. If an asynchronous PR discussion exceeds 3 back-and-forth comments, hold a 5-minute synchronous huddle.
14. "Disagree and Commit" enables teams to maintain velocity without getting stalled in subjective stalemates.
15. Capturing mutable state across asynchronous operations creates subtle multi-threaded race conditions.
16. `List<T>` and `Dictionary<TKey, TValue>` are not thread-safe; concurrent access corrupts internal pointer arrays.
17. Missing `Dispose()` on unmanaged handles, streams, and database connections causes memory leaks and handle exhaustion.
18. Sync-over-async (`.Result`, `.Wait()`) blocks ThreadPool worker threads, leading directly to ThreadPool starvation under load.
19. Methods declared `async void` crash the entire host process if an unhandled exception occurs; always return `async Task`.
20. Asynchronous methods must accept and propagate a `CancellationToken` to downstream I/O operations.
21. Suppressing Nullable Reference Types with `!` without runtime validation masks potential `NullReferenceException` crashes.
22. Financial currency values must always use `decimal` in C#, never `double` or `float` due to binary floating-point rounding errors.
23. System timestamps must be modeled using `DateTimeOffset.UtcNow` or `TimeProvider` to prevent server timezone bugs.
24. Anemic domain models expose public property setters, allowing external code to violate business invariants.
25. Rich domain models encapsulate state, exposing business methods that enforce invariants via guard clauses.
26. Returning `IQueryable<T>` from a repository leaks EF Core SQL provider capabilities and DbContext lifetimes across layers.
27. Newly introduced NuGet packages must be audited for active maintenance, license compliance (avoid AGPL), and security CVEs.
28. Raw SQL string interpolation (`$"SELECT * FROM Users WHERE Name = '{name}'"`) creates critical SQL Injection vulnerabilities.
29. Parameterized queries and EF Core LINQ methods automatically sanitize inputs, preventing SQL injection.
30. Broken Object Level Authorization (BOLA/IDOR) occurs when endpoints accept an ID without verifying the user owns the resource.
31. Mass Assignment (Over-posting) occurs when endpoints bind directly to database entities rather than strict request DTOs.
32. Sensitive PII, passwords, and tokens must never be written to application logs or console output.
33. String concatenation inside loops creates quadratic $O(n^2)$ memory copying; use `StringBuilder` or string interpolation.
34. Closure captures in high-frequency LINQ lambdas allocate compiler-generated Display Classes on the managed heap.
35. The N+1 query problem occurs when an application executes 1 initial query followed by $N$ secondary queries for related entities.
36. Read-only EF Core queries must include `AsNoTracking()` to avoid unnecessary Change Tracker allocation overhead.
37. Database endpoints must enforce pagination; returning unpaginated tables risks OutOfMemory exceptions as datasets grow.
38. Unit tests must assert observable domain behavior rather than verifying private internal implementation calls.
39. Over-mocked tests that verify every internal collaborator call break during refactoring even when code works perfectly.
40. Tests that rely on `Thread.Sleep()` or shared mutable staging databases introduce flakiness and must be rejected.
41. `<TreatWarningsAsErrors>true</TreatWarningsAsErrors>` ensures that compiler warnings break the build, preventing code decay.
42. Roslyn security analyzers (e.g. `Microsoft.CodeAnalysis.NetAnalyzers`) catch common memory and security defects in the IDE.
43. Pre-commit Git hooks (via Husky.Net) format staged files and run linters before code can be committed locally.
44. The `CODEOWNERS` file enforces mandatory senior reviewer approval for critical architectural and infrastructure paths.
45. Living documentation ensures README files and architecture diagrams evolve in the same Git repository as source code.
46. Architecture Decision Records (ADRs) document the context, decision, consequences, and trade-offs of significant choices.
47. Request for Comments (RFC) design documents align team architecture *before* engineers write code, preventing massive PR rewrites.
48. In code reviews, the phrase "In my opinion" should be backed by empirical data, profiling evidence, or documented standards.
49. A senior reviewer acts as a force multiplier, elevating team engineering maturity through educational critique.
50. High-performing engineering organizations maintain a blameless culture that separates personal ego from technical code quality.

---

## 3. Self-Assessment Rubric

| Dimension | Needs Work (Junior) | Developing (Mid-Level) | Senior-Ready | Strong Senior / Staff-Level |
|---|---|---|---|---|
| **Review Methodology & Focus** | Focuses exclusively on syntax and formatting; misses major bugs. | Reviews for basic logic and unit test coverage; catches obvious errors. | Follows the 6-stage hierarchy (Architecture $	o$ Correctness $	o$ Security $	o$ Performance); enforces the 400-line rule. | Identifies deep system-wide architectural flaws; prevents leaky abstractions; balances review depth with team delivery SLAs. |
| **Correctness & Concurrency Audit** | Misses race conditions; ignores sync-over-async and resource leaks. | Catches missing `Dispose()` calls and basic nullability warnings. | Spots subtle concurrency deadlocks, non-thread-safe collections, unpropagated cancellation tokens, and floating-point errors. | Diagnoses ThreadPool starvation risks, memory retention leaks, and complex asynchronous state machine traps. |
| **Secure Code Review** | Unaware of OWASP API Top 10; allows raw SQL string interpolation. | Identifies basic SQL injection and hardcoded passwords in diffs. | Audits diffs for BOLA/IDOR, mass assignment, SSRF, and sensitive data logging; verifies authentication boundaries. | Formulates organizational secure coding standards; integrates SAST analyzers (CodeQL) into CI/CD quality gates. |
| **Feedback Communication** | Gives vague or aggressive comments; debates formatting endlessly. | Provides helpful comments; explains why a change is requested. | Uses Conventional Comments (`issue:`, `suggestion:`, `praise:`); fosters psychological safety; halts bikeshedding. | Mentors junior and mid-level engineers through reviews; defuses technical disputes; practices "Disagree and Commit". |
| **Standards & Governance** | Manually checks style; ignores compiler warnings. | Configures basic `.editorconfig` files; runs formatters locally. | Enforces `<TreatWarningsAsErrors>`, Roslyn analyzers, and `CODEOWNERS`; automates quality gates in CI. | Authors organizational RFC processes; establishes ADR decision workflows; drives continuous engineering standard upgrades. |

---

# Part IV — References

1. **Empirical Code Review Research:**
   - Bacchelli, A., & Bird, C. "Expectations, Outcomes, and Challenges of Modern Code Review". *Proceedings of the 35th International Conference on Software Engineering (ICSE)*, 2013.
   - Rigby, P. C., & Bird, C. "Convergent Contemporary Software Peer Review Practices". *ACM FSE*, 2013.
   - Sadowski, C., Söderberg, E., Church, L., Sipko, M., & Bacchelli, A. "Modern Code Review: A Case Study at Google". *IEEE Software*, 2018.
2. **Industry Review Standards:**
   - [Google Engineering Practices: Code Review Developer Guide](https://google.github.io/eng-practices/review/)
   - [Conventional Comments Specification](https://conventionalcomments.org/)
   - [OWASP Code Review Guide](https://owasp.org/www-project-code-review-guide/)
   - [Microsoft Learn: .NET Code Analysis and Roslyn Analyzers](https://learn.microsoft.com/dotnet/fundamentals/code-analysis/overview)
