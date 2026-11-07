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
- 13.1 Capstone Scenario: End-to-end architectural design of a mission-critical public payment processing API handling \$10M daily volume with strict idempotency, rate limiting, and zero-downtime contract deprecation.

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

#### HTTP Status Code Taxonomy (RFC 9110)

| Range | Code | Semantic Meaning & Production Guidance |
|---|---|---|
| **2xx Success** | `200 OK` | Request succeeded; payload contains representation of target resource or action result. |
| | `201 Created` | New resource created. **Must** include `Location: /v1/orders/{id}` header. |
| | `202 Accepted` | Request validated and queued for asynchronous processing; include `Location` to status monitor resource. |
| | `204 No Content` | Succeeded with empty response body (common for `DELETE` or `PUT` when client already holds state). |
| **3xx Redirection** | `301` / `308` | Moved Permanently (`308` strictly forbids changing HTTP method from `POST` to `GET`; `301` historically allowed it). |
| | `302` / `307` | Found / Temporary Redirect (`307` preserves original HTTP method and body). |
| | `304 Not Modified` | Conditional `GET`/`HEAD` (`If-None-Match`) matched current `ETag`; no body transmitted. |
| **4xx Client Error** | `400 Bad Request` | Malformed syntax, invalid JSON framing, or missing required query/header parameter. |
| | `401 Unauthorized` | **Unauthenticated** — missing, expired, or cryptographically invalid credentials (`WWW-Authenticate` header required). |
| | `403 Forbidden` | **Unauthorized** — identity is known, but principal lacks permission/scope or fails BOLA ownership check. |
| | `404 Not Found` | Resource does not exist (or deliberately masked `403` to prevent tenant resource enumeration). |
| | `409 Conflict` | State conflict (e.g., duplicate business key, order already cancelled, or idempotency key currently in-flight). |
| | `412 Precondition Failed` | Optimistic concurrency failure (`If-Match` ETag did not match current database row version). |
| | `422 Unprocessable Content` | Syntactically valid JSON, but fails domain validation invariants (RFC 9110 / WebDAV origin). |
| | `429 Too Many Requests` | Rate limit or quota exceeded; always include `Retry-After` (delta-seconds or HTTP-date). |
| **5xx Server Error** | `500 Internal Server Error` | Unhandled fault in server code; never leak stack traces or SQL text in production. |
| | `502 Bad Gateway` | Reverse proxy / API gateway received an invalid response from an upstream server. |
| | `503 Service Unavailable` | Server overloaded, in maintenance mode, or circuit breaker open; include `Retry-After`. |
| | `504 Gateway Timeout` | Upstream dependency failed to respond within the gateway's configured timeout window. |

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

#### Cache-Control Directives & Strong vs Weak Validators
- **`Cache-Control: private, max-age=60, must-revalidate`**: Only the end-user browser may cache; shared CDN/reverse-proxy caches (Cloudflare, YARP) must not store it.
- **`Cache-Control: public, s-maxage=300, stale-while-revalidate=30`**: Shared CDN caches may serve the representation for 300s and asynchronously refresh stale content in the background for 30s without blocking client requests.
- **`Cache-Control: no-store`**: Strictly forbids writing the response to any volatile or non-volatile cache (mandatory for sensitive PII/PCI responses).
- **`Cache-Control: no-cache`**: Allows caching the representation, but forces the client/CDN to revalidate with the origin server via `If-None-Match` before serving it.
- **Strong ETag (`"v4-a9f83b"`) vs Weak ETag (`W/"v4-a9f83b"`)**: A strong ETag guarantees byte-for-byte identity (including compression/encoding), required for byte-range requests and `If-Match` concurrency checks. A weak ETag indicates semantic equivalence only and **cannot** be used with `If-Match` according to RFC 9110.

---

### 1.3 HTTP/1.1 vs HTTP/2 vs HTTP/3 (QUIC) & TLS 1.3 Handshake Mechanics

#### Head-of-Line (HoL) Blocking: Application Layer vs Transport Layer

```text
HTTP/1.1 (TCP) — Application-Layer HoL Blocking:
[Conn 1] === Req 1 (Slow 500ms) ===>[blocks Req 2]===>[Req 2]
(Workaround: Browsers open 6 parallel TCP connections per origin, multiplying TLS handshakes & TCP slow-start)

HTTP/2 (Single TCP Connection) — Binary Framing & Stream Multiplexing:
[TCP Conn] --[Frame: Stream 1][Frame: Stream 3][Frame: Stream 1][Frame: Stream 2]-->
(Problem: If 1 TCP packet is dropped on the network, the OS kernel stalls ALL HTTP/2 streams until TCP retransmission completes!)

HTTP/3 (QUIC over UDP) — Independent Stream Loss Recovery:
[UDP Socket] ==(QUIC Stream 1: Packet Lost -> Only Stream 1 waits)==
             ==(QUIC Stream 2: Delivered immediately to application!)==
             ==(QUIC Stream 3: Delivered immediately to application!)==
```

| Protocol Feature | HTTP/1.1 (RFC 9112) | HTTP/2 (RFC 9113) | HTTP/3 (RFC 9114) |
|---|---|---|---|
| **Underlying Transport** | TCP | TCP (single persistent connection) | **QUIC over UDP** |
| **Wire Framing** | Newline-delimited ASCII text | Binary frames (`HEADERS`, `DATA`, `RST_STREAM`, `WINDOW_CONTROL`) | QUIC binary frames in encrypted UDP datagrams |
| **Multiplexing** | No (pipelining broken in practice; requires connection pools) | Yes (interleaved streams over 1 TCP connection) | Yes (native independent streams in QUIC) |
| **HTTP HoL Blocking** | **Yes** — slow response blocks subsequent requests on same socket | **Solved** via stream multiplexing | **Solved** via QUIC streams |
| **Transport (TCP) HoL Blocking** | Yes | **Yes** — single lost TCP segment stalls all multiplexed streams | **Solved** — packet loss only stalls the affected QUIC stream |
| **Header Compression** | None (redundant cookies/headers sent verbatim) | **HPACK** (static + dynamic lookup tables + Huffman coding) | **QPACK** (adapted for out-of-order UDP delivery without HoL blocking) |
| **Connection Migration** | No (IP change drops TCP 4-tuple) | No | **Yes** via 64-bit **Connection ID** (seamless Wi-Fi $\to$ 5G handoff) |
| **TLS Handshake** | TCP (1 RTT) + TLS 1.2 (2 RTT) = **3 RTT** (or 2 RTT with TLS 1.3) | TCP + TLS 1.3 ALPN `h2` = **2 RTT** ($\approx 1$ RTT TCP + 1 RTT TLS) | Integrated QUIC + TLS 1.3 = **1-RTT** cold start, **0-RTT** resumption |

#### TLS 1.3 Handshake & 0-RTT Replay Danger
In TLS 1.2, establishing a secure session required 2 full network round-trips after the TCP 3-way handshake. **TLS 1.3 (RFC 8446)** deprecates legacy cipher suites (RSA key transport, CBC mode, SHA-1), mandates **Perfect Forward Secrecy (PFS)** via ephemeral Diffie-Hellman (`X25519` or `P-256`), and embeds the key share inside the initial `ClientHello`, completing the handshake in **1-RTT**.
- **QUIC 0-RTT Early Data:** When resuming a previous session using a Pre-Shared Key (PSK), HTTP/3 clients can send encrypted application data in the very first packet (`0-RTT`).
- **Senior Security Warning:** If an attacker captures and replays a `0-RTT` UDP packet, the server will execute it twice. Therefore, **never allow non-idempotent requests (`POST`) in 0-RTT early data**; Kestrel and Cloudflare reject 0-RTT upgrades with **`425 Too Early`** when replay risk exists.

---

### Section 1 Review: Interview Questions & Practice Exercises

#### Interview Questions

1. **Q: Why is `PUT` considered idempotent while `PATCH` is not, and under what conditions can a `PATCH` endpoint be made idempotent?**
   - **Model Answer:** By RFC 9110, `PUT` replaces the entire target resource representation with the enclosed payload ($f(x) = s$); applying that replacement 1 or 100 times results in the exact same resource state. `PATCH` describes a set of instructions to modify a resource. If a JSON Patch document contains `[{ "op": "add", "path": "/balance", "value": 10 }]` or increments a counter, executing it twice mutates the state twice. However, `PATCH` *can* be made idempotent if restricted to **JSON Merge Patch (RFC 7396)** setting absolute field values (e.g., `{"status": "Shipped"}`) combined with an `If-Match` ETag header so concurrent or duplicate applications against a stale version fail deterministically with `412 Precondition Failed`.

2. **Q: HTTP/2 introduced stream multiplexing to solve Head-of-Line (HoL) blocking. Why can switching from 6 HTTP/1.1 connections to 1 HTTP/2 connection actually *degrade* throughput on a lossy 2% packet-loss mobile network, and how does HTTP/3 solve this?**
   - **Model Answer:** HTTP/2 solves *application-layer* HoL blocking by interleaving frames from multiple streams over a single TCP connection. However, the OS kernel's TCP stack knows nothing about HTTP/2 streams—it only sees a single contiguous byte sequence. When a single TCP packet is dropped on a lossy link, the kernel holds back all subsequent out-of-order TCP segments in the receive buffer until the missing segment is retransmitted, stalling *every* active HTTP/2 stream simultaneously. Furthermore, a single TCP connection experiences multiplicative congestion window (`cwnd`) reduction across all streams upon packet loss, whereas 6 HTTP/1.1 connections only throttled $1/6$th of traffic. HTTP/3 replaces TCP with **QUIC over UDP**, moving stream awareness into the transport layer so a dropped UDP datagram only delays the specific stream whose bytes were in that packet.

3. **Q: Explain the semantic difference between `401 Unauthorized` and `403 Forbidden`, and when a Senior Engineer should deliberately return `404 Not Found` instead of `403 Forbidden`.**
   - **Model Answer:** Despite its historical name, `401 Unauthorized` means **unauthenticated**—the caller has not provided valid identity credentials (or the JWT is expired/tampered), and the server must include a `WWW-Authenticate` challenge header. `403 Forbidden` means **unauthorized**—the caller's identity is authenticated, but their scopes, roles, or tenant policies prohibit access, and re-authenticating will not help. In multi-tenant APIs (e.g., `GET /v1/invoices/{id}`), returning `403 Forbidden` when Tenant A requests Tenant B's invoice ID leaks the existence of that resource (an enumeration oracle). Returning `404 Not Found` when the query `WHERE Id = @id AND TenantId = @callerTenantId` returns zero rows masks cross-tenant existence completely.

#### Practice Exercises

1. **Exercise 1 — Optimistic Concurrency ETag Flow in Minimal APIs:** Implement a `PUT /api/v1/inventory/{sku}` endpoint in ASP.NET Core that reads the `If-Match` request header, compares it against a PostgreSQL `xmin` or SQL Server `rowversion` converted to base64 ETag, returns `428 Precondition Required` if `If-Match` is missing, and returns `412 Precondition Failed` if the row was concurrently updated.
2. **Exercise 2 — Kestrel HTTP/3 Configuration:** Configure Kestrel in .NET 9 to listen on port 5001 with `HttpProtocols.Http1AndHttp2AndHttp3`, inspect the `Alt-Svc: h3=":5001"; ma=86400` response header using `curl --http3`, and verify QUIC stream multiplexing in Wireshark.

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

### 2.2 Richardson Maturity Model, Resource URI Design & Asynchronous Operations (`202 Accepted`)

#### The Richardson Maturity Model (RMM)

| RMM Level | Name | Characteristics | Enterprise Reality Check |
|---|---|---|---|
| **Level 0** | **The Swamp of POX** | Single URI (`/api/service`), single HTTP method (`POST`), payload encodes RPC method name (`{"action": "getOrder", "id": 101}`). | Legacy SOAP/XML-RPC or anti-pattern REST wrappers. |
| **Level 1** | **Resources** | Distinct URIs per domain entity (`/orders/101`, `/customers/42`), but still tunnels operations through `POST` (`/orders/101/update`). | Improves routing, but breaks HTTP caching and idempotency guarantees. |
| **Level 2** | **HTTP Verbs & Status Codes** | Standard HTTP methods (`GET`, `POST`, `PUT`, `DELETE`) paired with granular RFC 9110 status codes (`201`, `409`, `412`, `422`). | **The pragmatic industry sweet spot** for 95% of production OpenAPI services. |
| **Level 3** | **Hypermedia Controls (HATEOAS)** | Responses embed hypermedia links (`_links`) advertising valid state transitions dynamically based on domain state. | Useful for state-driven workflows (e.g., Stripe/PayPal payment links) so clients don't hardcode state machines. |

#### Modeling Non-CRUD State Transitions as Sub-Resources
Beginner engineers often struggle when an action doesn't fit `Create/Read/Update/Delete` (e.g., cancelling an order, issuing a refund, or locking a user account).
- **Anti-Pattern (RPC Query Parameter):** `GET /api/v1/orders/101?action=cancel` (Violates `GET` safety; web crawlers or pre-fetchers will cancel orders!).
- **Pragmatic REST Pattern 1 (State Resource Collection):** Model the domain event as a sub-resource creation: `POST /api/v1/orders/101/cancellation` or `POST /api/v1/orders/101/refunds` (returns `201 Created` with the refund resource).
- **Pragmatic REST Pattern 2 (Controller Action Verb Sub-URI):** When no subordinate entity exists, Microsoft & Google REST Guidelines permit a clear action verb at the leaf of the URI: `POST /api/v1/orders/101:cancel` or `POST /api/v1/orders/101/cancel`.

#### Asynchronous Long-Running Operations (`202 Accepted` Polling Pattern)
When an operation takes longer than ~2–5 seconds (e.g., generating a 500,000-row financial audit export, provisioning cloud infrastructure, or running a batch reconciliation), holding an HTTP connection open risks **API Gateway timeouts (`504 Gateway Timeout` at 29–60s)** and exhausts connection pools.

```text
Client                                   API Server                        Background Worker
  |                                          |                                     |
  |--- POST /v1/reports/exports ------------>|                                     |
  |                                          |-- 1. Create Operation Row (Pending) |
  |                                          |-- 2. Enqueue to Service Bus ------->|
  |<-- 202 Accepted -------------------------|                                     |
  |    Location: /v1/operations/op_99a1      |                                     |-- 3. Generate PDF/CSV
  |    Retry-After: 5                        |                                     |-- 4. Upload to Blob
  |                                          |                                     |-- 5. Mark Completed
  |--- GET /v1/operations/op_99a1 ---------->|                                     |
  |<-- 200 OK { "status": "Running",         |                                     |
  |             "percentComplete": 45 }      |                                     |
  |    Retry-After: 5                        |                                     |
  |                                          |                                     |
  |--- GET /v1/operations/op_99a1 ---------->|                                     |
  |<-- 200 OK (or 303 See Other) ------------|                                     |
  |    { "status": "Succeeded",              |                                     |
  |      "resourceLocation": "/v1/exports/e1"|                                     |
  |    }                                     |                                     |
```

```csharp
public sealed record AsyncOperationStatus(
    string OperationId,
    string Status,          // "Pending" | "Running" | "Succeeded" | "Failed"
    int? PercentComplete,
    string? ResourceUrl,
    ProblemDetails? Error);

app.MapPost("/api/v1/reports/exports", async (
    ExportRequest request,
    IOperationTracker tracker,
    ChannelWriter<ExportJob> queue,
    HttpContext http) =>
{
    string opId = $"op_{Guid.NewGuid():N}";
    await tracker.CreatePendingAsync(opId, http.RequestAborted);
    await queue.WriteAsync(new ExportJob(opId, request), http.RequestAborted);

    http.Response.Headers.RetryAfter = "5";
    return TypedResults.Accepted($"/api/v1/operations/{opId}",
        new AsyncOperationStatus(opId, "Pending", 0, null, null));
});

app.MapGet("/api/v1/operations/{opId}", async (
    string opId,
    IOperationTracker tracker,
    HttpContext http) =>
{
    var status = await tracker.GetStatusAsync(opId, http.RequestAborted);
    if (status is null) return Results.NotFound();

    if (status.Status is "Pending" or "Running")
    {
        http.Response.Headers.RetryAfter = "5";
    }

    return Results.Ok(status);
});
```

---

### Section 2 Review: Interview Questions & Practice Exercises

#### Interview Questions

1. **Q: Why is a single-column cursor like `WHERE CreatedAt < @CursorDate` broken in production keyset pagination, and how do you fix it?**
   - **Model Answer:** Timestamps (`CreatedAt`) are not guaranteed to be unique when multiple rows are inserted within the same millisecond or clock tick. If 5 orders share the exact timestamp `10:00:00.123Z` and the page boundary cuts after the 2nd order, using strictly `< @CursorDate` on the next page will permanently skip the remaining 3 orders with that timestamp, whereas using `<= @CursorDate` will return duplicate rows already shown on page 1. The fix is a **composite tie-breaker cursor** combining the sort column with a guaranteed unique monotonic column: `WHERE (CreatedAt < @CursorDate) OR (CreatedAt = @CursorDate AND OrderId < @CursorId) ORDER BY CreatedAt DESC, OrderId DESC`, backed by a composite database index on `(CreatedAt DESC, OrderId DESC)`.

2. **Q: Compare the `202 Accepted` status polling pattern against Webhooks for long-running asynchronous API operations. When should you provide both?**
   - **Model Answer:** `202 Accepted` with a `Location: /v1/operations/{id}` header and `Retry-After` works universally for browsers, mobile apps, and clients behind NAT/firewalls that cannot expose public HTTPS endpoints. However, polling wastes bandwidth if intervals are too aggressive or adds latency if intervals are too wide. Webhooks push completion events immediately to a registered server URL with zero wasted polls, making them superior for server-to-server B2B integrations. Enterprise APIs (like Stripe or Azure ARM) expose **both**: `202 Accepted` polling for immediate UI progress bars and signed Webhooks for reliable backend state reconciliation.

#### Practice Exercises

1. **Exercise 1 — Opaque Base64Url Cursor Encoder:** Write a C# generic `CursorToken<TKey1, TKey2>` struct that serializes `(DateTimeOffset CreatedAt, Guid Id)` into a URL-safe Base64 string, signs or validates its structure, and returns `400 Bad Request` ProblemDetails if a client tampers with the cursor string.
2. **Exercise 2 — HATEOAS Order State Machine:** Implement an `OrderResponseDto` generator that emits `_links` containing `cancel` and `pay` links when `Status == OrderStatus.Pending`, only `refund` when `Status == OrderStatus.Paid`, and only `self` when `Status == OrderStatus.Cancelled`.

---

## Section 3 — Standardized Error Handling & Problem Details (RFC 9457)

### 3.1 RFC 9457 Problem Details Specification & Registration

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

### 3.2 Centralized Exception Mapping with `IExceptionHandler` (.NET 8/9)

In .NET 8+, `IExceptionHandler` replaces ad-hoc try/catch middleware by chaining strongly-typed exception handlers into the built-in `UseExceptionHandler()` pipeline and writing responses via `IProblemDetailsService` with content negotiation (`application/problem+json`).

```csharp
using System.Diagnostics;
using Microsoft.AspNetCore.Diagnostics;
using Microsoft.AspNetCore.Mvc;

public sealed class GlobalDomainExceptionHandler(
    IProblemDetailsService problemDetailsService,
    ILogger<GlobalDomainExceptionHandler> logger,
    IHostEnvironment environment) : IExceptionHandler
{
    public async ValueTask<bool> TryHandleAsync(
        HttpContext httpContext,
        Exception exception,
        CancellationToken cancellationToken)
    {
        var (statusCode, typeUri, title, detail, errorCode, validationErrors) = exception switch
        {
            DomainValidationException valEx => (
                StatusCodes.Status422UnprocessableEntity,
                "https://api.company.com/errors/validation-failed",
                "Domain Validation Failed",
                valEx.Message,
                "DOMAIN_VALIDATION_ERROR",
                valEx.Errors),

            ConcurrencyConflictException concEx => (
                StatusCodes.Status409Conflict,
                "https://api.company.com/errors/concurrency-conflict",
                "Resource State Conflict",
                concEx.Message,
                "CONCURRENCY_CONFLICT",
                null),

            ResourceNotFoundException notFoundEx => (
                StatusCodes.Status404NotFound,
                "https://api.company.com/errors/resource-not-found",
                "Resource Not Found",
                notFoundEx.Message,
                "RESOURCE_NOT_FOUND",
                null),

            _ => (
                StatusCodes.Status500InternalServerError,
                "https://api.company.com/errors/internal-server-error",
                "An unexpected fault occurred",
                environment.IsDevelopment()
                    ? exception.ToString()
                    : "An internal error occurred. Reference the traceId when contacting support.",
                "INTERNAL_ERROR",
                null)
        };

        if (statusCode == StatusCodes.Status500InternalServerError)
        {
            logger.LogError(exception, "Unhandled exception on {Method} {Path}",
                httpContext.Request.Method, httpContext.Request.Path);
        }
        else
        {
            logger.LogWarning("Domain exception {ErrorCode} ({StatusCode}) on {Method} {Path}: {Message}",
                errorCode, statusCode, httpContext.Request.Method, httpContext.Request.Path, exception.Message);
        }

        httpContext.Response.StatusCode = statusCode;

        var problemDetails = new ProblemDetails
        {
            Status = statusCode,
            Type = typeUri,
            Title = title,
            Detail = detail,
            Instance = $"{httpContext.Request.Method} {httpContext.Request.Path}"
        };

        problemDetails.Extensions["traceId"] = Activity.Current?.Id ?? httpContext.TraceIdentifier;
        problemDetails.Extensions["errorCode"] = errorCode;
        problemDetails.Extensions["timestamp"] = DateTimeOffset.UtcNow;

        if (validationErrors is not null)
        {
            problemDetails.Extensions["errors"] = validationErrors;
        }

        return await problemDetailsService.TryWriteAsync(new ProblemDetailsContext
        {
            HttpContext = httpContext,
            Exception = exception,
            ProblemDetails = problemDetails
        });
    }
}
```

---

### Section 3 Review: Interview Questions & Practice Exercises

#### Interview Questions

1. **Q: What did RFC 9457 improve over RFC 7807 for Problem Details, and why should client SDKs branch on `type` or `errorCode` rather than `title` or `detail`?**
   - **Model Answer:** RFC 9457 obsoleted RFC 7807 by clarifying how multiple problems should be represented via typed extension members, formalizing the URI registry for problem types, and advising against coupling human-readable `detail` strings to programmatic logic. Client code must never regex-parse `detail` (which may change phrasing or be localized via `Accept-Language`). Instead, clients must branch on the immutable `type` URI (`https://api.company.com/errors/insufficient-funds`) or a structured machine-readable extension (`errorCode: "FUNDS_004"`).

2. **Q: When designing error handling in a high-throughput .NET API, when should you use the Result pattern (`Result<T, DomainError>`) vs throwing exceptions caught by `IExceptionHandler`?**
   - **Model Answer:** Throwing and unwinding the stack in .NET incurs significant CPU and allocation overhead ($\approx 5\text{--}20\ \mu\text{s}$ per exception) to capture stack frames. Expected business outcomes—such as invalid user input, insufficient balance, or duplicate email registration—should be modeled via the **Result Pattern** and mapped directly to `TypedResults.Problem(...)` or `TypedResults.UnprocessableEntity(...)` without throwing exceptions. `IExceptionHandler` serves as the safety net for truly exceptional infrastructure failures (deadlocks, network drops, unexpected invariant breaches) ensuring no unhandled exception ever escapes without an RFC 9457 envelope and `traceId`.

#### Practice Exercises

1. **Exercise 1 — Multi-Error Validation ProblemDetails:** Extend `GlobalDomainExceptionHandler` so that when a request fails multiple field validations (e.g., invalid IBAN and negative transfer amount), it populates `extensions["errors"]` as a `Dictionary<string, string[]>` matching ASP.NET Core's `HttpValidationProblemDetails` schema.
2. **Exercise 2 — Information Disclosure Audit:** Write an integration test using `WebApplicationFactory<Program>` in `"Production"` environment mode that triggers a `SqlException` and asserts the HTTP 500 `ProblemDetails` response contains `traceId` but zero SQL table names or stack trace strings.

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
