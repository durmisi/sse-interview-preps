# Module 06 — API Design & Integrations

**Senior Software Engineer Academy · Module 06 of 12**

> **Learning objective:** Master enterprise API engineering across the full integration lifecycle: HTTP RFC 9110 protocol semantics, RESTful resource modeling, OpenAPI contract evolution, standardized Problem Details (RFC 9457), OAuth 2.0 / OIDC security architecture, OWASP API Security Top 10 defense, API-level idempotency keys, secure webhook processing, and resilient third-party integrations with Polly v8 and `IHttpClientFactory`.
>
> **Audience:** Experienced C#/.NET engineers preparing for Senior, Lead, and Staff technical interviews. Real-world API gateway, microservice communication, and third-party SaaS integration experience is assumed; protocol RFCs, cryptographic token validation, and distributed tracing are taught with exact technical rigor.
>
> **Version note:** Code examples target modern .NET (.NET 8 LTS and .NET 9) with C# 12/13, ASP.NET Core Minimal APIs, `Microsoft.Extensions.Http.Resilience` (Polly v8), and .NET 9 native OpenAPI generation.

## How to use this module

Every section in Part II provides comprehensive senior-level instruction:
1. **Protocol Standards & RFC Mechanics:** RFC 9110, RFC 9457, RFC 6749, RFC 7636, and W3C Trace Context.
2. **C#/.NET Production Implementation:** Production-grade Minimal APIs, custom endpoint filters, HMAC signature verifiers, and resilience pipelines.
3. **Enterprise Production Scenarios:** Diagnosing socket exhaustion, BOLA security breaches, replay attacks, and breaking contract changes.
4. **Trade-offs, Alternatives & Failure Modes:** When REST fails and gRPC or WebSockets are required; offset vs keyset pagination trade-offs.
5. **What a Senior Engineer Is Expected to Know:** Mid-level vs Senior/Staff API architecture.
6. **Interview Questions with Model Answers:** Real interview questions with structured, senior-level responses.
7. **Practical Exercises:** Security audits, contract design drills, and webhook verification implementations.

## Progress tracker

| Section | Topic | Status |
|---|---|---|
| Section 1 | HTTP Protocol Semantics & RFC 9110 Mastery | Complete |
| Section 2 | RESTful Resource Modeling & Richardson Maturity Model | Complete |
| Section 3 | Standardized Error Handling & Problem Details (RFC 9457) | Complete |
| Section 4 | API Contracts, OpenAPI & Versioning Strategies | Complete |
| Section 5 | High-Performance ASP.NET Core Minimal APIs Engineering | Complete |
| Section 6 | Alternative API Styles: gRPC, GraphQL & Real-Time | Complete |
| Section 7 | Identity, Authentication & OAuth 2.0 / OIDC Architecture | Complete |
| Section 8 | API Security & OWASP API Security Top 10 (2023) | Complete |
| Section 9 | Idempotency at the API Boundary & Request Deduplication | Complete |
| Section 10 | Webhooks Architecture & Cryptographic Signature Verification | Complete |
| Section 11 | Resilient Third-Party Integrations & `IHttpClientFactory` | Complete |
| Section 12 | Observability, Distributed Tracing & W3C Trace Context | Complete |
| Section 13 | Senior Scenarios, API Governance & Capstone | Complete |

**Current position:** Full curriculum complete. Ready for self-study, exercises, and interview drills.

## Module boundaries

- **This module owns:** HTTP protocol semantics, REST resource modeling, Minimal APIs, OAuth 2.0, OIDC, JWTs, OWASP API security, idempotency keys, webhooks, Polly HTTP resilience, and W3C distributed trace propagation.
- **Related topics owned by other modules:**
  - In-process design patterns, CQRS, and Clean Architecture → Module 04
  - Database persistence, EF Core mapping, and SQL query performance → Module 05
  - Asynchronous state machines, ThreadPool, and Kestrel socket internals → Module 03
  - Distributed messaging (Service Bus, Kafka), Sagas, and Outbox pattern → Module 07
  - High-level system design, global API gateways, and rate limiting architectures → Module 08

---

# Part I — Complete Curriculum

## Section 1 — HTTP Protocol Semantics & RFC 9110 Mastery
- 1.1 Method Semantics: Safe methods (GET, HEAD, OPTIONS) vs Idempotent methods (PUT, DELETE, GET) vs Non-idempotent (POST, PATCH).
- 1.2 Status Code Taxonomy: 2xx Success (200, 201, 202, 204), 3xx Redirection (301, 302, 304 Not Modified), 4xx Client Errors (400, 401, 403, 404, 409 Conflict, 412, 422, 429), 5xx Server Errors (500, 502 Bad Gateway, 503 Service Unavailable, 504 Gateway Timeout).
- 1.3 HTTP Caching & Conditional Requests: `Cache-Control` directives (public, private, no-cache, no-store, max-age, must-revalidate); Validators: strong vs weak `ETag`; conditional headers (`If-None-Match`, `If-Match`) for optimistic concurrency.
- 1.4 Transport Evolution: HTTP/1.1 (head-of-line blocking, persistent connections) vs HTTP/2 (binary framing, multiplexing, stream prioritization) vs HTTP/3 (QUIC, UDP-based, zero-RTT handshakes).

## Section 2 — RESTful Resource Modeling & Richardson Maturity Model
- 2.1 Richardson Maturity Model: Level 0 (The Swamp of POX / RPC), Level 1 (Individual Resources), Level 2 (HTTP Verbs), Level 3 (HATEOAS / Hypermedia).
- 2.2 URI Design & Hierarchy: Nouns over verbs; plural collections (`/api/v1/orders/{id}/lines`); sub-resources vs top-level filters.
- 2.3 Pagination Mechanics: Offset-based pagination (`page=2&limit=50`) and its performance degradation on large datasets; Keyset / Cursor-based pagination (`cursor=eyJpZCI6MTAxfQ==`) ensuring $O(1)$ database seeks and consistency during real-time writes.
- 2.4 Asynchronous Long-Running Operations: Handling operations that exceed gateway timeouts; returning `202 Accepted` with a `Location: /api/v1/operations/{id}` polling header.

## Section 3 — Standardized Error Handling & Problem Details (RFC 9457)
- 3.1 Problem Details Specification: `type`, `title`, `status`, `detail`, `instance`, and custom extensions (`traceId`, `errors`).
- 3.2 ASP.NET Core Implementation: Centralized exception-to-ProblemDetails mapping via `IProblemDetailsService` and `AddProblemDetails()`.

## Section 4 — API Contracts, OpenAPI & Versioning Strategies
- 4.1 OpenAPI 3.1 Specifications: Schema definitions, request bodies, response schemas; Design-First vs Code-First trade-offs.
- 4.2 Versioning Paradigms: URI Path (`/v1/orders`), Query String (`?api-version=1.0`), Custom Header (`X-API-Version: 1.0`), Accept/Media Type Header (`Accept: application/vnd.company.order.v1+json`).
- 4.3 Breaking vs Non-Breaking Changes: Backward compatibility rules; API deprecation protocols using `Sunset` and `Deprecation` HTTP response headers.

## Section 5 — High-Performance ASP.NET Core Minimal APIs Engineering
- 5.1 Minimal APIs Architecture: Direct endpoint mapping without Controller reflection overhead; Route Groups with shared security and validation.
- 5.2 Endpoint Filters: Cross-cutting execution pipelines (`AddEndpointFilter`) for validation, logging, and performance metrics.
- 5.3 Strongly Typed Results: `TypedResults` returning compile-time verified response types (`Results<Ok<OrderDto>, NotFound, BadRequest<ProblemDetails>>`).

## Section 6 — Alternative API Styles: gRPC, GraphQL & Real-Time
- 6.1 gRPC & Protocol Buffers: Contract-first `.proto` IDL, binary serialization speed, bidirectional streaming; when gRPC is ideal for inter-service microservice backbones.
- 6.2 GraphQL Trade-Offs: Client-specified queries avoiding over-fetching; the N+1 problem in GraphQL resolvers; DataLoader caching in HotChocolate.
- 6.3 Real-Time Communications: WebSockets (full-duplex) vs Server-Sent Events (SSE - unidirectional text stream for AI tokens) vs SignalR.

## Section 7 — Identity, Authentication & OAuth 2.0 / OIDC Architecture
- 7.1 Authentication vs Authorization: Proving who you are vs what you are permitted to do.
- 7.2 OAuth 2.0 Grant Types: Authorization Code Flow with PKCE (RFC 7636) for SPAs and mobile; Client Credentials Flow for server-to-server microservices; why Implicit Grant and Resource Owner Password Credentials (ROPC) are deprecated.
- 7.3 OpenID Connect (OIDC): Identity layer on top of OAuth 2.0; ID Token (for client) vs Access Token (for API resource server); UserInfo endpoint.
- 7.4 JWT Architecture & Cryptographic Validation: Header (alg, typ, kid), Payload (claims), Signature; Asymmetric signing (RS256, ES256) with public key JWKS endpoints vs symmetric (HS256); validating `iss`, `aud`, `exp`, `nbf`; Backend-for-Frontend (BFF) pattern for securing SPAs against token theft.

## Section 8 — API Security & OWASP API Security Top 10 (2023)
- 8.1 API1: Broken Object Level Authorization (BOLA / IDOR): The #1 API vulnerability; accessing another tenant's data by guessing IDs; enforcing ownership checks in domain services.
- 8.2 API2: Broken Authentication & API3: Broken Object Property Level Authorization (Mass Assignment / Over-posting attacks).
- 8.3 API4: Unrestricted Resource Consumption: Implementing multi-tier rate limiting and payload size limits.
- 8.4 API7: Server-Side Request Forgery (SSRF): Sanitizing outbound webhook URLs and preventing access to internal metadata IP addresses (`169.254.169.254`).

## Section 9 — Idempotency at the API Boundary & Request Deduplication
- 9.1 The Idempotency Problem: Network timeouts on `POST` requests causing clients to retry, resulting in duplicate financial charges.
- 9.2 The `Idempotency-Key` Protocol: Request fingerprinting, distributed locking in Redis during execution, caching the exact HTTP response payload for deterministic replay.

## Section 10 — Webhooks Architecture & Cryptographic Signature Verification
- 10.1 Webhook Producer Design: Event schemas, retries with exponential backoff and jitter, dead-lettering failed subscriber endpoints.
- 10.2 Cryptographic Signing: HMAC-SHA256 signatures (`X-Signature-256`), shared secrets, timestamp inclusion to prevent replay attacks.
- 10.3 Safe Consumer Ingestion: Verifying signatures in constant time, enqueuing immediately to a message broker (Azure Service Bus), and returning 200 OK within 200ms.

## Section 11 — Resilient Third-Party Integrations & `IHttpClientFactory`
- 11.1 The Socket Exhaustion Trap: Why `new HttpClient()` creates thousands of lingering `TIME_WAIT` sockets; DNS staleness in naive singleton clients.
- 11.2 `IHttpClientFactory` Internals: `HttpMessageHandler` pooling (2-minute default lifetime), named and typed clients.
- 11.3 Polly v8 Resilience Pipelines: `Microsoft.Extensions.Http.Resilience`; combining timeouts, exponential backoff retries with jitter, circuit breakers, and rate limiters.

## Section 12 — Observability, Distributed Tracing & W3C Trace Context
- 12.1 Distributed Tracing Standards: The W3C `traceparent` header (`version-trace_id-parent_id-trace_flags`); propagating trace context across HTTP boundaries.
- 12.2 OpenTelemetry in ASP.NET Core: .NET `Activity` and `ActivitySource`; correlating HTTP logs, database queries, and downstream calls under a unified Trace ID.

## Section 13 — Senior Scenarios, API Governance & Capstone
- 13.1 Capstone Scenario: End-to-end architectural design of a mission-critical public payment processing API handling $10M daily volume with strict idempotency, rate limiting, and zero-downtime contract deprecation.

---

# Part II — Lessons

## Section 1 — HTTP Protocol Semantics & RFC 9110 Mastery

### 1.1 Method Safety and Idempotency

Understanding method semantics according to RFC 9110 is foundational for designing reliable distributed APIs:

| HTTP Method | Safe? | Idempotent? | Cacheable? | RFC 9110 Semantic Meaning |
|---|---|---|---|---|
| **GET** | **Yes** | **Yes** | **Yes** | Transfer a current representation of the target resource. Must have zero observable side effects. |
| **HEAD** | **Yes** | **Yes** | **Yes** | Identical to GET, but server must not transfer the response body. Used to check metadata/ETag. |
| **POST** | No | **No** | Conditional | Perform resource-specific processing (create child resource, submit form, execute command). |
| **PUT** | No | **Yes** | No | Replace all current representations of the target resource with the request state. Calling $N$ times produces identical state. |
| **PATCH** | No | **No** | Conditional | Apply partial modifications to a resource (JSON Patch / JSON Merge Patch). |
| **DELETE** | No | **Yes** | No | Remove all current representations of the target resource. Deleting an already-deleted resource returns 200 or 204. |
| **OPTIONS**| **Yes** | **Yes** | No | Query communication capabilities available for the target URI (used heavily in CORS pre-flight). |

---

### 1.2 HTTP Caching and Conditional Requests (ETags)

To prevent the **Lost Update Problem** in concurrent REST APIs without holding database locks:
1. When a client reads a resource (`GET /orders/101`), the server returns an `ETag` header containing an entity hash:
   ```http
   HTTP/1.1 200 OK
   ETag: "v4-a9f83b"
   ```
2. When the client submits an update (`PUT /orders/101`), it includes the `If-Match` header:
   ```http
   PUT /orders/101 HTTP/1.1
   If-Match: "v4-a9f83b"
   ```
3. If another user modified the order in the interim, its ETag changed to `"v5-bb123"`. The server detects the mismatch and rejects the update with **`412 Precondition Failed`**, completely preventing accidental data overwrites!

---

## Section 2 — RESTful Resource Modeling & Richardson Maturity Model

### 2.1 Keyset / Cursor Pagination vs Offset Pagination

#### The Offset Pagination Problem (`?page=1000&limit=50`):
In SQL, `OFFSET 50000 ROWS FETCH NEXT 50 ROWS ONLY` forces the database engine to scan and discard 50,000 index rows before returning 50. As page numbers increase, latency degrades quadratically to dozens of seconds. Furthermore, if new records are inserted while a user navigates, records shift across pages, causing users to see duplicate items or miss rows entirely.

#### The Keyset / Cursor Pagination Solution:
Instead of page numbers, the client passes an opaque cursor representing the unique sort key of the last item seen (`?cursor=2024-11-01T10:00:00Z_101`):
```sql
SELECT TOP (50) OrderId, CreatedAt, TotalAmount
FROM Orders
WHERE (CreatedAt < @CursorDate) OR (CreatedAt = @CursorDate AND OrderId < @CursorId)
ORDER BY CreatedAt DESC, OrderId DESC;
```
*Result:* Always executes an instantaneous $O(1)$ index seek regardless of whether the user is on row 50 or row 50,000,000!

---

## Section 3 — Standardized Error Handling & Problem Details (RFC 9457)

```csharp
// Program.cs: Centralized Problem Details in ASP.NET Core 8+
builder.Services.AddProblemDetails(options =>
{
    options.CustomizeProblemDetails = context =>
    {
        context.ProblemDetails.Instance = $"{context.HttpContext.Request.Method} {context.HttpContext.Request.Path}";
        context.ProblemDetails.Extensions["traceId"] = Activity.Current?.Id ?? context.HttpContext.TraceIdentifier;
    };
});
```

#### Standard RFC 9457 JSON Response:
```json
{
  "type": "https://api.company.com/errors/insufficient-funds",
  "title": "Insufficient Funds",
  "status": 400,
  "detail": "Your account balance of $45.00 cannot cover the transaction fee of $100.00.",
  "instance": "POST /api/v1/transfers",
  "traceId": "00-4bf92f3577b34da6a3ce929d0e0e4736-00f067aa0ba902b7-01",
  "errorCode": "FUNDS_004"
}
```

---

## Section 7 — Identity, Authentication & OAuth 2.0 / OIDC Architecture

### 7.1 OAuth 2.0 Authorization Code Flow with PKCE (RFC 7636)

The standard for single-page apps (React/Angular) and mobile apps:
1. **Code Verifier & Code Challenge:** The client creates a cryptographically random secret string (the `code_verifier`) and hashes it using SHA-256 (the `code_challenge`).
2. **Authorization Request:** Client redirects user to Identity Provider (`/authorize`) with `code_challenge` and `code_challenge_method=S256`.
3. **Authorization Code:** User logs in; IdP redirects back to client with a short-lived `authorization_code`.
4. **Token Exchange:** Client posts the `authorization_code` AND the unhashed `code_verifier` directly to the `/token` endpoint.
5. **IdP Verification:** The IdP hashes the received `code_verifier` and verifies it matches the original `code_challenge`.
*Why PKCE Matters:* Even if an attacker intercepts the authorization code via URL hijacking, they cannot exchange it for tokens without possessing the secret `code_verifier`!

---

### 7.2 Backend-for-Frontend (BFF) Pattern for Secure SPAs

Storing access tokens in browser memory (Local Storage / Session Storage) exposes tokens to Cross-Site Scripting (XSS) theft.
The **BFF Pattern** deploys a lightweight server-side backend (e.g., in ASP.NET Core with Yarp reverse proxy):
- The browser authenticates via an encrypted, `SameSite=Strict`, `HttpOnly`, `Secure` cookie.
- The BFF server holds the OAuth tokens securely in server-side session memory.
- When the browser calls an API, the BFF intercepts the cookie, attaches the Bearer JWT to the header, and proxies the request to downstream microservices.

---

## Section 8 — API Security & OWASP API Security Top 10 (2023)

### 8.1 API1: Broken Object Level Authorization (BOLA / IDOR)

BOLA occurs when an endpoint accepts an ID from the client and retrieves data without verifying whether the authenticated user owns or has access to that object:

```csharp
// VULNERABLE TO BOLA (IDOR)
app.MapGet("/api/v1/invoices/{id}", async (Guid id, AppDbContext db) =>
{
    // Attacker can simply change id=101 to id=102 and read ANY tenant's financial data!
    var invoice = await db.Invoices.FindAsync(id);
    return invoice is not null ? Results.Ok(invoice) : Results.NotFound();
});

// SECURED: Ownership verified against authenticated User context
app.MapGet("/api/v1/invoices/{id}", async (Guid id, ClaimsPrincipal user, AppDbContext db) =>
{
    var tenantId = user.GetTenantId(); // Extracted from verified JWT claim

    var invoice = await db.Invoices
        .FirstOrDefaultAsync(i => i.Id == id && i.TenantId == tenantId); // ENFORCE BOUNDARY!

    return invoice is not null ? Results.Ok(invoice) : Results.NotFound();
});
```

---

## Section 9 — Idempotency at the API Boundary & Request Deduplication

### 9.1 Idempotency Key Architecture for Financial POST Requests

```text
Client                   API Gateway / Endpoint                  Redis / Database
  |                                |                                   |
  |--- POST /payments ------------>|                                   |
  |    Idempotency-Key: K-8812     |--- SETNX idempotency:K-8812 ----->|
  |                                |    (Acquire Distributed Lock)     |
  |                                |<-- OK (Lock Acquired) ------------|
  |                                |                                   |
  |                                |-- Execute Payment Processing -----|
  |                                |                                   |
  |                                |--- Store Cached HTTP Response --->|
  |                                |    Status: 200, Body: { ... }     |
  |<-- 200 OK (Payment Processed) -|                                   |
  |                                |                                   |
  |=== (Network Drop / Retry) =====|                                   |
  |--- POST /payments ------------>|                                   |
  |    Idempotency-Key: K-8812     |--- SETNX idempotency:K-8812 ----->|
  |                                |<-- FAIL (Key Already Exists!) ----|
  |                                |--- Read Cached Response --------->|
  |                                |<-- Return Cached HTTP 200 --------|
  |<-- 200 OK (Replayed Response) -|                                   |
```

---

## Section 10 — Webhooks Architecture & Cryptographic Signature Verification

### 10.1 Verifying HMAC-SHA256 Signatures in Constant Time

```csharp
public static bool VerifyWebhookSignature(string payload, string signatureHeader, string secret)
{
    byte[] keyBytes = Encoding.UTF8.GetBytes(secret);
    byte[] payloadBytes = Encoding.UTF8.GetBytes(payload);

    using var hmac = new HMACSHA256(keyBytes);
    byte[] computedHash = hmac.ComputeHash(payloadBytes);
    string expectedSignature = Convert.ToHexString(computedHash);

    // CRITICAL SECURITY RULE: Use CryptographicOperations.FixedTimeEquals!
    // Standard string == comparison leaks timing information, allowing attackers to forge signatures byte-by-byte!
    byte[] expectedBytes = Encoding.UTF8.GetBytes(expectedSignature);
    byte[] actualBytes = Encoding.UTF8.GetBytes(signatureHeader);

    return CryptographicOperations.FixedTimeEquals(expectedBytes, actualBytes);
}
```

---

## Section 11 — Resilient Third-Party Integrations & `IHttpClientFactory`

### 11.1 Polly v8 Resilience Pipeline Integration

```csharp
// Program.cs: Registering a standard resilience pipeline with Polly v8
builder.Services.AddHttpClient<IStripePaymentClient, StripePaymentClient>(client =>
{
    client.BaseAddress = new Uri("https://api.stripe.com/v1/");
})
.AddStandardResilienceHandler(options =>
{
    // Configure Exponential Backoff with Jitter:
    options.Retry.MaxRetryAttempts = 3;
    options.Retry.BackoffType = DelayBackoffType.Exponential;
    options.Retry.UseJitter = true; // Prevents thundering herd on downstream API

    // Configure Circuit Breaker:
    options.CircuitBreaker.SamplingDuration = TimeSpan.FromSeconds(30);
    options.CircuitBreaker.FailureRatio = 0.5; // Trip if 50% of requests fail

    // Configure Request Timeout:
    options.TotalRequestTimeout.Timeout = TimeSpan.FromSeconds(10);
});
```

---

# Part III — Interview Readiness

## 1. Mid-Level vs Senior-Level API Design Comparison

| Topic | Mid-Level Candidate Response | Senior / Staff-Level Candidate Response |
|---|---|---|
| **Pagination** | "Use `page` and `pageSize` parameters with SQL `OFFSET` and `FETCH NEXT`." | "Offset pagination degrades to $O(n)$ scan times and skips/duplicates rows during live writes. For high-volume endpoints, we implement Keyset/Cursor pagination using indexed monotonic columns, ensuring $O(1)$ database seeks and stable pages." |
| **API Versioning** | "Put `/v1/` and `/v2/` in the URL path." | "URI versioning is common and pragmatic, but represents new resource schemas rather than variations. We evaluate URI path vs Accept header versioning, enforce backward-compatible schema expansion, and establish deprecation protocols using `Sunset` and `Deprecation` HTTP headers." |
| **Idempotency** | "Make all your endpoints use `PUT` instead of `POST`." | "`PUT` is idempotent by definition because it replaces the entire target resource state, but it is unsuitable for operations like charging payments. For non-idempotent `POST` commands, we implement an `Idempotency-Key` protocol with distributed locking in Redis and cached response replay." |
| **API Security** | "Validate JWT tokens on every request and check the user's role." | "Role checks alone are vulnerable to BOLA (Broken Object Level Authorization), the #1 OWASP API vulnerability. We validate object ownership at the domain service layer against tenant claims, secure SPAs via the BFF pattern with `HttpOnly` cookies, and sanitize against SSRF." |
| **Third-Party Integrations** | "Instantiate an `HttpClient` inside a using block and call the API." | "`new HttpClient()` causes socket exhaustion, while naive singletons suffer from DNS staleness. We use `IHttpClientFactory` with handler rotation and configure Polly v8 resilience pipelines with exponential backoff, jitter, circuit breakers, and rate limiters." |

---

## 2. Rapid-Fire Revision Sheet (50 Senior-Level Truths)

1. RFC 9110 defines Safe methods as those with zero observable state mutations (GET, HEAD, OPTIONS).
2. Idempotent methods produce identical system state whether executed once or ten times (GET, PUT, DELETE, HEAD).
3. POST is non-idempotent by specification and is designed for non-reversible processing like submitting orders.
4. Returning HTTP 201 Created must include a `Location` header pointing to the newly generated resource URI.
5. Returning HTTP 202 Accepted indicates an asynchronous request has been validated and queued for background processing.
6. The `ETag` and `If-Match` headers provide optimistic concurrency control in REST APIs, preventing the Lost Update problem.
7. Offset-based pagination causes severe database query degradation on deep pages and shifts rows during concurrent writes.
8. Keyset / Cursor pagination uses indexed sorting columns (e.g. `(CreatedAt, Id)`) to guarantee $O(1)$ index seek performance.
9. RFC 9457 Problem Details defines the standard machine-readable schema for HTTP API error responses.
10. A Problem Details response should include an `instance` URI and a unique `traceId` extension for distributed tracing.
11. In REST URI design, nouns represent collections and resources (`/api/v1/orders`), while verbs represent non-resource actions (`/api/v1/orders/101/cancel`).
12. URI versioning (`/v1/`) is easy to route, but media type versioning (`Accept: application/vnd.company.v1+json`) preserves semantic URI purity.
13. The HTTP `Sunset` header indicates the future date when an API version or endpoint will be permanently decommissioned.
14. Minimal APIs in ASP.NET Core eliminate MVC controller reflection overhead and execute directly on Kestrel endpoint routing.
15. `TypedResults` in Minimal APIs enforce compile-time verification of return types and OpenAPI schema generation.
16. gRPC utilizes Protocol Buffers for compact binary serialization and runs over HTTP/2 for stream multiplexing.
17. In GraphQL, the N+1 problem occurs when resolvers fetch nested relationships independently; DataLoader solves this via batching.
18. Server-Sent Events (SSE) provide a unidirectional, text-based HTTP stream ideal for streaming LLM AI token responses.
19. WebSockets establish a full-duplex TCP connection, ideal for bi-directional gaming and collaborative editing.
20. Authentication verifies identity (who you are); Authorization verifies access permissions (what you can do).
21. The OAuth 2.0 Authorization Code Flow with PKCE (RFC 7636) prevents authorization code interception in SPAs and mobile apps.
22. The Implicit Grant and Resource Owner Password Credentials (ROPC) flows are deprecated and insecure in OAuth 2.1.
23. Client Credentials Grant is the standard flow for machine-to-machine server communication without user context.
24. OpenID Connect (OIDC) is an identity layer on top of OAuth 2.0 that provides an ID Token and a UserInfo endpoint.
25. A JSON Web Token (JWT) consists of three base64url-encoded parts: Header, Payload, and Signature.
26. Asymmetric JWT signing (RS256, ES256) allows APIs to verify signatures using the IdP's public keys via a JWKS endpoint.
27. The Backend-for-Frontend (BFF) pattern prevents token theft by storing tokens on a server and authenticating SPAs via `HttpOnly` cookies.
28. Broken Object Level Authorization (BOLA/IDOR) is the #1 OWASP API vulnerability, where users manipulate IDs to view unauthorized data.
29. To prevent BOLA, endpoints must enforce tenant and user ownership checks inside the domain layer for every query.
30. Mass Assignment (Over-posting) vulnerabilities occur when endpoints bind directly to domain entities rather than strict request DTOs.
31. Server-Side Request Forgery (SSRF) occurs when an API fetches a user-supplied URL without blocking internal IP addresses (e.g. `169.254.169.254`).
32. The `Idempotency-Key` header allows clients to safely retry `POST` requests without creating duplicate charges or records.
33. During idempotency key processing, a distributed lock in Redis prevents concurrent duplicate requests with the same key.
34. The API response of an idempotent request is cached and replayed identically if the client retries with the same key.
35. Webhooks should sign payloads using HMAC-SHA256 and include the signature in an HTTP header (e.g., `X-Signature-256`).
36. Webhook signatures must be verified using `CryptographicOperations.FixedTimeEquals` to prevent side-channel timing attacks.
37. Webhook payloads must include a timestamp to protect consumer endpoints against replay attacks.
38. Safe webhook consumers verify signatures, enqueue payloads directly to a message broker, and return HTTP 200 within 200ms.
39. Creating `new HttpClient()` instances repeatedly exhausts OS TCP socket ports, leaving thousands of sockets in `TIME_WAIT`.
40. Naive singleton `HttpClient` instances fail to update DNS records when an external server's IP address changes.
41. `IHttpClientFactory` pools `HttpMessageHandler` pipelines (default 2-minute lifetime) to solve both socket exhaustion and DNS staleness.
42. Polly v8 (`Microsoft.Extensions.Http.Resilience`) combines timeouts, retries with jitter, and circuit breakers in a unified pipeline.
43. Retries must include randomized jitter to prevent thundering herd spikes on downstream services during recovery.
44. A Circuit Breaker trips to the Open state when a failure threshold is exceeded, failing fast without hitting downstream dependencies.
45. APIs should respond with HTTP 429 Too Many Requests and include a `Retry-After` header when rate limits are exceeded.
46. The W3C `traceparent` header (`00-4bf92f3577b34da6a3ce929d0e0e4736-00f067aa0ba902b7-01`) propagates distributed trace context.
47. OpenTelemetry `ActivitySource` in .NET starts and stops trace spans, propagating context across HTTP headers automatically.
48. In HTTP/2, stream multiplexing eliminates HTTP/1.1 head-of-line blocking at the application protocol layer.
49. In HTTP/3, QUIC runs over UDP to eliminate TCP transport head-of-line blocking caused by dropped packets.
50. An Anti-Corruption Layer (ACL) translates external third-party API models into internal domain aggregates, isolating core logic.

---

## 3. Self-Assessment Rubric

| Dimension | Needs Work (Junior) | Developing (Mid-Level) | Senior-Ready | Strong Senior / Staff-Level |
|---|---|---|---|---|
| **Protocol Semantics & REST** | Uses GET for updates; returns 200 OK for errors; uses offset pagination. | Understands HTTP verbs and status codes; implements basic REST resource URIs. | Enforces RFC 9110 semantics; designs Keyset pagination; uses ETags for optimistic concurrency; applies Problem Details RFC 9457. | Architects zero-downtime contract versioning (Sunset headers); designs asynchronous 202 polling workflows for long tasks. |
| **Authentication & Security** | Stores JWTs in localStorage; vulnerable to BOLA and mass assignment. | Implements basic JWT bearer authentication; checks roles and claims. | Enforces BOLA protection at domain boundaries; architectures OAuth2 PKCE and Client Credentials; implements BFF pattern. | Prevents SSRF on outbound webhooks; designs JWKS key rotation pipelines; audits APIs against OWASP API Top 10. |
| **Integration & Resilience** | Creates `new HttpClient()`; causes socket exhaustion; no retries. | Uses `IHttpClientFactory`; adds basic Polly retry policies. | Configures Polly v8 with jitter, circuit breakers, and rate limiters; handles 429 `Retry-After`; prevents DNS staleness. | Architects Anti-Corruption Layers (ACL); implements idempotency key protocol with Redis distributed locking and response replay. |
| **Webhooks & Streaming** | Compares webhook signatures via `==`; blocks webhook ingestion with slow work. | Verifies HMAC signatures; processes webhooks synchronously. | Uses `CryptographicOperations.FixedTimeEquals`; guards against replay attacks; queues webhooks to brokers immediately. | Designs webhook delivery pipelines with exponential backoff, jitter, dead-lettering, and subscriber rotation. |
| **Observability & Standards** | Uses unstructured console logging; loses correlation across services. | Logs correlation IDs; configures basic Swagger UI. | Propagates W3C `traceparent` headers; instrument APIs with OpenTelemetry `ActivitySource`; defines OpenAPI 3.1 contracts. | Establishes enterprise API governance standards; defines API error taxonomy; monitors P99 latency and error budgets. |

---

# Part IV — References

1. **Official Protocol RFCs:**
   - [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
   - [RFC 9457: Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457)
   - [RFC 6749: The OAuth 2.0 Authorization Framework](https://www.rfc-editor.org/rfc/rfc6749)
   - [RFC 7636: Proof Key for Code Exchange (PKCE)](https://www.rfc-editor.org/rfc/rfc7636)
   - [RFC 7519: JSON Web Token (JWT)](https://www.rfc-editor.org/rfc/rfc7519)
2. **Security & Industry Standards:**
   - [OWASP API Security Top 10 (2023)](https://owasp.org/API-Security/)
   - [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines)
   - [W3C Trace Context Specification](https://www.w3.org/TR/trace-context/)
   - [Microsoft Learn: Resilience in .NET with Polly v8](https://learn.microsoft.com/dotnet/core/resilience/http-resilience)
