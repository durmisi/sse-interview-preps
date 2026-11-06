# Module 11 — DevOps & Engineering Processes

> **Senior Software Engineer Academy** · Advanced Professional Curriculum · Module 11 of 12

---

## Progress Tracker

| Section | Topic | Status |
|---|---|---|
| 1 | DevOps Foundations: CALMS, The Three Ways, DORA Metrics & Team Topologies | Completed |
| 2 | Git Internals & Branching Strategies: Object Model, Rebase vs Merge, Bisect & Trunk-Based Development | Completed |
| 3 | Continuous Integration: Stages, Reproducible Builds, Central Package Management, SBOM & Test Parallelism | Completed |
| 4 | CI/CD Platforms & Secure Automation: GitHub Actions & Azure DevOps YAML, OIDC Workload Identity | Completed |
| 5 | Continuous Delivery & Pipeline Architecture: Build Once Deploy Many, Env Config & DB Migration Gates | Completed |
| 6 | Deployment Strategies: Rolling, Blue-Green, Canary, Feature Flags (Azure App Configuration) & Rollbacks | Completed |
| 7 | Containers & Orchestration: Multi-Stage Docker, Chiseled .NET, Kubernetes AKS Architecture & Probes | Completed |
| 8 | Infrastructure as Code (IaC): Declarative Bicep vs Terraform, State Drift, Managed Identities & GitOps | Completed |
| 9 | Observability Engineering: OpenTelemetry in .NET, Activity/Meter, Azure Monitor, KQL & SLO Burn Alerts | Completed |
| 10 | Incident Management & Operations: On-Call, Severity Levels, Incident Commander & Blameless Postmortems | Completed |
| 11 | DevSecOps & Supply Chain Security: SLSA Framework, Secret/Container Scanning & Branch Protection | Completed |
| 12 | Agile Flow Metrics & Lean Delivery: Scrum Anti-Patterns, Kanban WIP Limits, Cycle Time & CFD | Completed |
| 13 | Enterprise Change Management: Automated Audit Trails, SOC 2 / ISO 27001 Compliance & Modern CAB | Completed |
| 14 | DevOps Capstone: End-to-End GitOps on Azure AKS with Bicep, Canary Rollout & Sev-1 Postmortem | Completed |

---

## Module Boundaries

- **Upstream Dependencies:**
  - [Module 03 — C# & .NET Internals](file:///module_03_dotnet_internals.md): Low-level performance, memory profiling, and ASP.NET Core hosting model running in Linux container environments.
  - [Module 05 — Databases & Data Engineering](file:///module_05_databases_data_engineering.md): Zero-downtime expand/contract schema migrations executed within continuous delivery pipelines.
  - [Module 09 — Testing & Quality Engineering](file:///module_09_testing_quality_engineering.md): Automated test gates, unit, integration, contract, and mutation testing running in CI pipelines.
- **Downstream Dependents:**
  - [Module 12 — Senior Engineering Leadership](file:///module_12_senior_engineering_leadership.md): Incident communication, engineering culture, flow metrics, and capacity estimation.

---

# Part I — Complete Curriculum

### Scope & Senior Expectations
A Senior Software Engineer does not treat CI/CD, deployment, and infrastructure as "someone else's job" (the mythical Ops team). A senior engineer owns code from commit through production monitoring to graceful retirement. You must understand how git objects are hashed on disk, how to write non-root distroless container images, how to configure OIDC workload federations to deploy to Azure without static long-lived credentials, how to interpret OpenTelemetry distributed traces and KQL telemetry, and how to lead blameless postmortems when production fails.

```
+-------------------------------------------------------------------------------------------------------+
|                                     THE MODERN DEVOPS LIFECYCLE                                       |
+-------------------------------------------------------------------------------------------------------+
|  [PLAN & COMMIT]      [CONTINUOUS INTEGRATION]     [CONTINUOUS DELIVERY]      [RUN & OBSERVE]         |
|  - Trunk-Based Git    - Restore (CPM lockfiles)    - Artifact Publishing      - OpenTelemetry         |
|  - Conventional Msg   - Parallel Unit/Integration  - Bicep / Terraform IaC    - App Insights / KQL    |
|  - Pre-commit Hooks   - SAST / Secret Scanning     - Blue/Green or Canary     - Golden Signals & SLOs |
|  - Small PR Batches   - SBOM Generation (CycloneDX)- Azure App Config Flags   - Blameless Postmortems |
+-------------------------------------------------------------------------------------------------------+
```

---

# Part II — Lessons

---

### Section 1: DevOps Foundations: CALMS, The Three Ways, DORA Metrics & Team Topologies

#### 1. Concept & Internal Mechanics
DevOps is an engineering culture and operational model, not a job title or a tools suite.
- **The CALMS Framework**:
  - **Culture**: Shared responsibility between product, engineering, and operations.
  - **Automation**: Continuous integration, testing, provisioning, and delivery.
  - **Lean**: Small batch sizes, minimizing Work-in-Progress (WIP), eliminating waste.
  - **Measurement**: Measuring telemetry, system metrics, and business outcomes.
  - **Sharing**: Knowledge diffusion, cross-functional collaboration, blameless reviews.
- **The Three Ways (Gene Kim / The Phoenix Project)**:
  1. *Flow / Systems Thinking*: Accelerate the flow of value from left to right (Dev to Ops to Customer) by limiting WIP and reducing batch sizes.
  2. *Feedback Loops*: Amplify feedback from right to left (Ops/Prod back to Dev) so defects are detected immediately.
  3. *Continuous Experimentation & Learning*: Fostering psychological safety, taking calculated risks, and institutionalizing knowledge from outages.
- **DORA Core Metrics (DevOps Research and Assessment)**:
  1. **Deployment Frequency (DF)**: How often an organization successfully releases to production (Elite: On-demand, multiple deploys per day).
  2. **Lead Time for Changes (LTTC)**: The time it takes for a commit to reach production (Elite: Under one hour).
  3. **Change Failure Rate (CFR)**: The percentage of deployments causing a failure in production requiring rollback or hotfix (Elite: 0% – 15%).
  4. **Time to Restore Service (TTRS / MTTR)**: How long it takes to restore service when a service incident occurs (Elite: Under one hour).
- **Team Topologies (Skelton & Pais)**:
  - *Stream-Aligned Teams*: Continuous flow of business feature delivery.
  - *Enabling Teams*: Specialists who upskill stream teams in new technologies (e.g., cloud, OTel).
  - *Complicated-Subsystem Teams*: Specialists handling high-math or esoteric domains (e.g., custom rendering engine, crypto).
  - *Platform Teams*: Provide self-service internal developer platforms (IDP) enabling stream-aligned teams to deliver without operational tickets.

#### 2. Why It Matters in Enterprise Software
High DORA metric performance correlates directly with business success, lower burnout, and higher profitability. In legacy enterprises, changes take months because tickets bounce between Dev, QA, Security, CAB (Change Advisory Board), and Ops. Modern platform engineering replaces ticket queues with automated self-service APIs and paved golden paths.

#### 3. Enterprise Scenario: Improving DORA Performance
An enterprise banking system deploys once every 6 weeks with a 38% Change Failure Rate and an average MTTR of 18 hours. The leadership wants to move to weekly deployments.
- *Root Cause*: 6 weeks of batch changes contain 400 merged PRs across 12 teams with zero integration testing prior to staging, and deployments require 14 manual sign-offs.
- *Remediation*:
  1. Mandate trunk-based development with feature flags to reduce batch size from 400 PRs to 1 PR per release.
  2. Automate regression testing in CI using Testcontainers (.NET + real SQL Server) running in parallel under 8 minutes.
  3. Replace manual CAB meetings with automated deployment pipelines gated on code coverage (>80%), green contract tests, and automated policy verification.

#### 4. Senior vs Mid-Level Distinction
- **Mid-Level**: Thinks DevOps means writing a GitHub Actions YAML file or knowing Docker commands. Measures success by "I wrote my code and pushed it to QA."
- **Senior**: Measures end-to-end flow from commit to production telemetry. Understands system bottlenecks (Theory of Constraints), drives DORA metrics, advocates for Platform Engineering to reduce cognitive load on stream teams, and balances deployment frequency against blast radius.

---

### Section 2: Git Internals & Branching Strategies: Object Model, Rebase vs Merge, Bisect & Trunk-Based Development

#### 1. Concept & Internal Mechanics
Git is a content-addressable directed acyclic graph (DAG) storage engine.
- **The Object Model (`.git/objects`)**:
  - Every object is identified by a SHA-1 (or SHA-256) hash: `hash = SHA(type + " " + size + "\0" + content)`.
  - **Blob**: Raw file contents (no filenames, no timestamps, no permissions).
  - **Tree**: Directory listing containing permissions, object types, hashes, and filenames.
  - **Commit**: Points to a root Tree object, parent commit hashes, author/committer timestamps, and commit message.
  - **Annotated Tag**: Object pointing to a specific commit with tagger metadata and cryptographic signature.
- **Index / Staging Area (`.git/index`)**:
  - A binary file listing all file paths in the working tree, their file mode, timestamps, and corresponding blob SHA hashes. `git add` computes the blob hash, writes the object, and updates the index.
- **Merge vs Rebase vs Squash**:
  - `git merge`: Preserves true historical topology by creating a 3-way merge commit with two parents (`HEAD` and merged branch). Non-destructive, but creates tangled "railroad track" history in large teams.
  - `git rebase`: Replays commits from the current branch onto another base commit, creating brand-new commit SHAs. Creates a clean linear history, but rewriting public shared history causes merge conflicts for collaborators.
  - `git merge --squash`: Collapses an entire branch of 20 commits into a single new commit on the target branch. Keeps trunk history atomic and bisectable.
- **Trunk-Based Development vs GitFlow**:
  - *GitFlow*: `develop`, `feature/*`, `release/*`, `hotfix/*`, `main`. Leads to massive merge hell ("merge freezes"), delayed feedback, and high lead time for changes.
  - *Trunk-Based Development*: Developers merge short-lived feature branches (<24 hours lifespan) directly into `main` multiple times a day. Features that are not ready for production are hidden behind feature flags.
- **`git bisect`**:
  - Performs a binary search across commit history to identify the exact commit that introduced a regression in $O(\log N)$ time.
  ```bash
  git bisect start
  git bisect bad HEAD
  git bisect good v2.4.0
  git bisect run dotnet test --filter "FullyQualifiedName=MyApp.Tests.OrderTests.Checkout_Fails"
  ```

#### 2. Why It Matters in Enterprise Software
Large monorepos and enterprise teams with 100+ engineers stall completely under GitFlow. Merge freezes cost hundreds of engineering hours. Trunk-based development coupled with automated CI ensures code is continuously integrated, preventing "divergence debt."

#### 3. Senior vs Mid-Level Distinction
- **Mid-Level**: Terrified of rebasing, relies on Git UI tools without understanding commit DAGs, creates branches that live for 3 weeks, and resolves merge conflicts by blindly accepting one side.
- **Senior**: Operates comfortably with `git rebase -i`, `reflog`, and `bisect run`. Enforces trunk-based development with branch protection rules, squash-and-merge PR policies for atomic trunk commits, and conventional commit specifications for automated SemVer tagging.

---

### Section 3: Continuous Integration: Stages, Reproducible Builds, Central Package Management, SBOM & Test Parallelism

#### 1. Concept & Internal Mechanics
Continuous Integration (CI) is the practice of continuously merging all developer code into a shared mainline multiple times daily, with every commit verified by an automated build, test suite, and static analysis pipeline.

- **Pipeline Stages**:
  ```
  +---------+     +---------+     +---------+     +---------+     +---------+
  | Restore | --> | Compile | --> | Test    | --> | Analyze | --> | Package |
  | & Cache |     | (WarnAs |     | Unit &  |     | SAST &  |     | & SBOM  |
  |         |     |  Error) |     | Integr. |     | Secrets |     | Push    |
  +---------+     +---------+     +---------+     +---------+     +---------+
  ```
- **Central Package Management (CPM) in .NET 8/9**:
  - Eliminates package dependency drift across large multi-project solutions.
  - Defined via `Directory.Packages.props`:
  ```xml
  <Project>
    <PropertyGroup>
      <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
      <CentralPackageTransitivePinningEnabled>true</CentralPackageTransitivePinningEnabled>
    </PropertyGroup>
    <ItemGroup>
      <PackageVersion Include="Microsoft.Extensions.Logging" Version="9.0.0" />
      <PackageVersion Include="OpenTelemetry.Exporter.OpenTelemetryProtocol" Version="1.9.0" />
      <PackageVersion Include="xunit" Version="2.9.2" />
    </ItemGroup>
  </Project>
  ```
- **Reproducible Builds & Deterministic Compilation**:
  - Setting `<Deterministic>true</Deterministic>` ensures that compiling the exact same source code with the same compiler parameters produces byte-for-byte identical PE binaries and PDB symbols regardless of machine path or timestamp.
- **Software Bill of Materials (SBOM)**:
  - Generates a machine-readable inventory of all software components, direct dependencies, transitive packages, and licensing metadata (SPDX or CycloneDX standard).
  - In .NET: `dotnet-sbom-tool` generates standard SPDX 2.2 documents used for compliance and automated vulnerability auditing.

#### 2. Test Parallelism & Pipeline Performance
Slow CI pipelines destroy developer productivity. If CI takes 45 minutes, developers stop running tests locally and context-switch constantly.
- **Optimization Strategies**:
  1. *Restore Caching*: Cache `~/.nuget/packages` keyed by `**/packages.lock.json` or `Directory.Packages.props`.
  2. *Parallel Test Execution*: `dotnet test --maxcpucount:0 --collect:"XPlat Code Coverage" --filter "Category!=Slow"`.
  3. *Test Slicing / Sharding*: GitHub Actions matrix strategies split 5,000 integration tests across 4 parallel runner nodes.

---

### Section 4: CI/CD Platforms & Secure Automation: GitHub Actions & Azure DevOps YAML, OIDC Workload Identity

#### 1. Concept & Internal Mechanics
Modern enterprise automation mandates declarative YAML pipelines stored in source control alongside code.
- **OIDC Federated Workload Identity (No Long-Lived Secrets)**:
  - Storing static service principal client secrets or subscription management passwords in GitHub Actions Secrets is a severe security vulnerability (secrets leak in logs, expire unpredictably, and cannot be rotated without downtime).
  - OpenID Connect (OIDC) lets the CI runner request a temporary, short-lived JSON Web Token (JWT) from GitHub Actions or Azure DevOps. The Azure Active Directory (Entra ID) federated identity credential validates the token's claims (`issuer`, `subject`, `audience`) and issues a temporary Azure access token valid for 60 minutes.

#### 2. GitHub Actions YAML with OIDC and Azure Login
```yaml
name: Build and Deploy API

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

permissions:
  id-token: write  # Required for requesting the OIDC JWT token
  contents: read

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Source
        uses: actions/checkout@v4

      - name: Setup .NET SDK
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '9.0.x'
          cache: true
          cache-dependency-path: '**/packages.lock.json'

      - name: Restore Dependencies
        run: dotnet restore --locked-mode

      - name: Build Solution
        run: dotnet build --no-restore --configuration Release /p:TreatWarningsAsErrors=true

      - name: Run Unit & Integration Tests
        run: dotnet test --no-build --configuration Release --logger "trx;LogFileName=test-results.trx"

      - name: Azure Login via OIDC
        if: github.ref == 'refs/heads/main'
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Deploy Container to Azure Container Apps
        if: github.ref == 'refs/heads/main'
        run: |
          az containerapp update \
            --name order-service \
            --resource-group rg-production \
            --image myregistry.azurecr.io/order-service:${{ github.sha }}
```

---

### Section 5: Continuous Delivery & Pipeline Architecture: Build Once Deploy Many, Env Config & DB Migration Gates

#### 1. Concept & Internal Mechanics
- **The "Build Once, Deploy Many" Principle**:
  - A build artifact (Docker image, ZIP package, NuGet package) must be compiled and packaged **exactly once**.
  - That identical, immutable binary is deployed through Development, Staging, and Production. Rebuilding binaries per environment invalidates testing, risks compiler drift, and breaks reproducibility.
- **Environment Configuration**:
  - Configuration is injected at runtime via environment variables, Kubernetes ConfigMaps, Azure App Configuration, or Azure Key Vault secrets. The code never contains environment-specific branches (`if (env == "prod")`).
- **Database Migration Gates in Pipelines**:
  - Running automated EF Core `context.Database.Migrate()` on application container startup in Kubernetes causes race conditions when multiple replicas spin up simultaneously, risking index corruption and deadlocks.
  - *Senior Practice*: Decouple schema migration from application boot. Execute schema migration as an isolated, pre-deployment step:
    1. Generate idempotent SQL migration script: `dotnet ef migrations script --idempotent --output migration.sql`.
    2. Execute migration script via an isolated pipeline task or Kubernetes `Job` using dedicated elevated credentials.
    3. Deploy the application code only after the database migration succeeds.

---

### Section 6: Deployment Strategies: Rolling, Blue-Green, Canary, Feature Flags & Rollbacks

#### 1. Concept & Comparison Matrix

| Strategy | Architecture | Traffic Shift | Downtime | Resource Cost | Rollback Speed |
|---|---|---|---|---|---|
| **Recreate** | Terminate all old pods, then start new pods | Instant | High (Minutes) | Baseline (1x) | Slow (Re-pull old image) |
| **Rolling Update** | Incrementally replace old pods with new pods (e.g. maxSurge=25%, maxUnavailable=0) | Gradual across replica pool | Zero | Low (+25% capacity) | Medium (Roll back rolling sequence) |
| **Blue-Green** | Two identical production environments. Blue runs live v1; Green is deployed with v2. Router/Load Balancer flips traffic. | Instant (100% switch) | Zero | High (2x full capacity) | Instant (Flip router back to Blue) |
| **Canary** | Route small percentage (e.g. 5%) of live traffic to v2; verify telemetry/error rates; progressively increase to 100%. | Controlled incremental (5% -> 25% -> 100%) | Zero | Low (+10-20% capacity) | Instant (Route 100% back to baseline) |
| **Shadow / Dark Launch** | Production requests are duplicated; response from v2 is discarded. Compares latency and accuracy under real traffic. | Dual-routed read traffic | Zero | Medium (Requires shadow infrastructure) | Zero risk (Live users never see v2) |

#### 2. Feature Flags with Azure App Configuration & .NET
```csharp
// Program.cs
builder.Configuration.AddAzureAppConfiguration(options =>
{
    options.Connect(builder.Configuration["ConnectionStrings:AppConfig"])
           .UseFeatureFlags(featureFlagOptions =>
           {
               featureFlagOptions.CacheExpirationInterval = TimeSpan.FromSeconds(30);
           });
});

builder.Services.AddFeatureManagement()
                .AddFeatureFilter<PercentageFilter>()
                .AddFeatureFilter<TargetingFilter>();

// OrderController.cs
[ApiController]
[Route("orders")]
public class OrderController : ControllerBase
{
    private readonly IFeatureManager _featureManager;

    public OrderController(IFeatureManager featureManager) => _featureManager = featureManager;

    [HttpPost]
    public async Task<IActionResult> PlaceOrder([FromBody] OrderDto dto)
    {
        if (await _featureManager.IsEnabledAsync("UseV2PricingEngine"))
        {
            return Ok(await CalculateV2Price(dto));
        }

        return Ok(await CalculateV1Price(dto));
    }
}
```

---

### Section 7: Containers & Orchestration: Multi-Stage Docker, Chiseled .NET, Kubernetes AKS Architecture & Probes

#### 1. Multi-Stage Distroless / Chiseled Dockerfile
Production images must not include SDKs, compilers, shell binaries (`/bin/sh`, `bash`), or package managers (`apt`, `apk`). Attackers who achieve remote code execution (RCE) cannot download malware if `curl`, `wget`, and shells do not exist.

```dockerfile
# Stage 1: Build & Publish
FROM mcr.microsoft.com/dotnet/sdk:9.0-noble AS build
WORKDIR /src

# Copy CPM and csproj files for optimal layer caching
COPY ["Directory.Packages.props", "."]
COPY ["Directory.Build.props", "."]
COPY ["src/Api/Api.csproj", "src/Api/"]
COPY ["src/Core/Core.csproj", "src/Core/"]
RUN dotnet restore "src/Api/Api.csproj"

# Copy source and compile
COPY . .
WORKDIR "/src/src/Api"
RUN dotnet publish "Api.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore \
    /p:UseAppHost=false

# Stage 2: Final Minimal Runtime (Chiseled Ubuntu - Non-root, no shell, ~100MB)
FROM mcr.microsoft.com/dotnet/aspnet:9.0-noble-chiseled AS final
WORKDIR /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Run as non-root user (app user defined in chiseled base image)
USER $APP_UID
COPY --from=build --chown=$APP_UID:$APP_UID /app/publish .
ENTRYPOINT ["dotnet", "Api.dll"]
```

#### 2. Kubernetes Pod Lifecycle & Health Probes
Misconfiguring Kubernetes probes causes cascading outages during rolling updates.
- **Startup Probe**: Determines if the application has completed initialization (e.g., JIT warmup, EF Core metadata caching). While startup probe runs, liveness and readiness checks are disabled.
- **Liveness Probe**: Determines if the container process is alive and responsive. If it fails, kubelet **kills the container and restarts it**. *Anti-pattern*: Checking database connectivity in a liveness probe! If the database has a momentary outage, Kubernetes kills all API pods simultaneously, causing a catastrophic self-inflicted cascade.
- **Readiness Probe**: Determines if the pod is ready to accept incoming user network traffic. If it fails, Kubernetes **removes the pod's IP from the Service endpoints / load balancer**. Database checks belong here.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-api
spec:
  replicas: 4
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 0
  template:
    spec:
      containers:
      - name: order-api
        image: myacr.azurecr.io/order-api:v1.4.2
        resources:
          requests:
            cpu: "250m"
            memory: "512Mi"
          limits:
            cpu: "1000m"
            memory: "1024Mi"
        startupProbe:
          httpGet:
            path: /health/startup
            port: 8080
          failureThreshold: 30
          periodSeconds: 2
        livenessProbe:
          httpGet:
            path: /health/live
            port: 8080
          initialDelaySeconds: 0
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /health/ready
            port: 8080
          initialDelaySeconds: 0
          periodSeconds: 5
```

---

### Section 8: Infrastructure as Code (IaC): Declarative Bicep vs Terraform, State Drift, Managed Identities & GitOps

#### 1. Concept & Comparison: Bicep vs Terraform
- **Bicep**: Azure-native domain-specific language that transpiles directly into Azure Resource Manager (ARM) JSON templates.
  - *Pros*: First-class day-zero support for all Azure services, no external state file to manage (Azure Resource Graph acts as the live state), no state locking issues, zero cost.
  - *Cons*: Strictly Azure-only.
- **Terraform**: HashiCorp Configuration Language (HCL) targeting cloud-agnostic providers.
  - *Pros*: Multi-cloud (AWS, Azure, GCP, Cloudflare, Datadog in a single workflow).
  - *Cons*: Requires state file management (`.tfstate` in Azure Blob Storage with lease locking), provider synchronization delay for new Azure features.

#### 2. Declarative Azure Bicep Module Example
```bicep
param environmentName string
param location string = resourceGroup().location

// Azure Container Registry with Managed Identity RBAC
resource acr 'Microsoft.ContainerRegistry/registries@2023-07-01' = {
  name: 'acr${uniqueString(resourceGroup().id)}${environmentName}'
  location: location
  sku: {
    name: 'Premium'
  }
  properties: {
    adminUserEnabled: false
  }
}

// User-Assigned Managed Identity for Compute
resource appIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2023-01-31' = {
  name: 'id-orderapp-${environmentName}'
  location: location
}

// Assign AcrPull Role to the Managed Identity
var acrPullRoleId = '7f951dda-4ed3-4680-a7ca-43fe172d538d'
resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  name: guid(acr.id, appIdentity.id, acrPullRoleId)
  scope: acr
  properties: {
    roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', acrPullRoleId)
    principalId: appIdentity.properties.principalId
    principalType: 'ServicePrincipal'
  }
}
```

---

### Section 9: Observability Engineering: OpenTelemetry in .NET, Activity/Meter, Azure Monitor, KQL & SLO Burn Alerts

#### 1. OpenTelemetry (OTel) in Modern .NET 8/9
Observability rests on three pillars: **Metrics**, **Traces**, and **Logs**. OpenTelemetry provides the vendor-neutral industry standard API and SDK.
- `System.Diagnostics.Activity` = OpenTelemetry Span
- `System.Diagnostics.ActivitySource` = OpenTelemetry Tracer
- `System.Diagnostics.Metrics.Meter` = OpenTelemetry Meter
- `System.Diagnostics.Metrics.Counter` / `Histogram` = OpenTelemetry Instruments

```csharp
public static class TelemetryConstants
{
    public const string ServiceName = "OrderProcessingService";
    public static readonly ActivitySource ActivitySource = new(ServiceName, "1.0.0");
    public static readonly Meter Meter = new(ServiceName, "1.0.0");
    public static readonly Counter<long> OrdersCreatedCounter = Meter.CreateCounter<long>(
        "orders.created.count", unit: "{order}", description: "Total orders created");
    public static readonly Histogram<double> OrderProcessingDuration = Meter.CreateHistogram<double>(
        "orders.processing.duration", unit: "ms", description: "Order placement execution time");
}

public class OrderService
{
    public async Task<Guid> PlaceOrderAsync(OrderDto order)
    {
        using var activity = TelemetryConstants.ActivitySource.StartActivity("PlaceOrder");
        activity?.SetTag("customer.id", order.CustomerId);
        activity?.SetTag("order.currency", order.Currency);

        var stopwatch = Stopwatch.StartNew();
        try
        {
            var orderId = await PersistOrderAsync(order);
            TelemetryConstants.OrdersCreatedCounter.Add(1, new KeyValuePair<string, object?>("status", "success"));
            activity?.SetStatus(ActivityStatusCode.Ok);
            return orderId;
        }
        catch (Exception ex)
        {
            activity?.SetStatus(ActivityStatusCode.Error, ex.Message);
            activity?.RecordException(ex);
            TelemetryConstants.OrdersCreatedCounter.Add(1, new KeyValuePair<string, object?>("status", "failure"));
            throw;
        }
        finally
        {
            stopwatch.Stop();
            TelemetryConstants.OrderProcessingDuration.Record(stopwatch.ElapsedMilliseconds);
        }
    }
}
```

#### 2. Kusto Query Language (KQL) for Azure Log Analytics & App Insights
```kql
// Calculate 95th and 99th percentile HTTP latency and failure rate by operation
requests
| where timestamp >= ago(24h)
| summarize 
    TotalRequests = count(),
    FailedRequests = countif(success == false),
    P95LatencyMs = percentile(duration, 95),
    P99LatencyMs = percentile(duration, 99)
    by name, bin(timestamp, 1h)
| extend FailureRatePct = round((FailedRequests * 100.0) / TotalRequests, 2)
| where FailureRatePct > 1.0 or P99LatencyMs > 2000
| order by timestamp desc
```

#### 3. Multi-Window Multi-Burn-Rate SLO Alerts
Traditional threshold alerting ("alert if error rate > 2% over 5 minutes") creates endless false alarms. Google SRE best practice uses **Burn Rate Alerts** tied to your Service Level Objective (SLO):
- If your SLO is 99.9% availability over 30 days, your error budget is 0.1%.
- A burn rate of 14.4 consumes 2% of your 30-day error budget in 1 hour. This triggers a page (wake up on-call).
- A burn rate of 6 consumes 5% of your error budget in 6 hours. This creates a ticket (next business day).

---

### Section 10: Incident Management & Operations: On-Call, Severity Levels, Incident Commander & Blameless Postmortems

#### 1. Severity Classifications & Incident Response
- **Sev-1 (Critical)**: Production outage affecting major user base or direct financial revenue (e.g., checkout offline, database corrupted). Requires immediate 24/7 page, war room assembly, and executive status page updates every 15 minutes.
- **Sev-2 (Major)**: Significant degradation affecting a subset of users with no immediate workaround (e.g., credit card refunds failing, latency 5x normal). Response within 15 minutes.
- **Sev-3 (Minor)**: Degraded functionality with available workaround (e.g., admin reporting slow). Handled during normal business hours.

#### 2. Key Incident Roles
- **Incident Commander (IC)**: Holds single-threaded authority over incident response. Does **not** debug code. The IC assigns tasks, keeps responders focused, prevents executive meddling, and controls communication cadences.
- **Communications Lead**: Updates customer-facing status dashboards and executive leadership.
- **Operations / Technical Lead**: Directs debugging, log analysis, and mitigation steps.

#### 3. Principle: Mitigate First, Debug Later
In a Sev-1 outage, your goal is **time to restore service**, not identifying the root cause. If a deployment caused the issue, **roll back immediately**. If memory is exhausted, restart or scale out immediately. Preserve memory dumps/logs to a secondary volume and restore customer traffic before conducting deep debugging.

#### 4. The Blameless Postmortem Structure
Blame produces fear; fear produces concealment of mistakes. A blameless postmortem investigates system failure modes:
1. **Executive Summary & Impact**: Time of detection, MTTR, customer impact ($ loss, failed requests).
2. **Timeline of Events (UTC)**: Second-by-second timeline from initial change to customer recovery.
3. **Root Cause Analysis (5 Whys)**: Deep dive into technical and organizational contributing factors.
4. **What Went Well / What Went Poorly**: Evaluation of alerts, tooling, documentation, and communication.
5. **Action Items (SMART)**: Concrete tasks with assigned owners and deadlines to eliminate the failure class entirely (e.g., add architectural guardrails, automated circuit breakers).

---

### Section 11: DevSecOps & Software Supply Chain: SLSA Framework, Secret/Container Scanning & Branch Protection

#### 1. Supply Chain Levels for Software Artifacts (SLSA)
Software supply chains are vulnerable to compromised dependencies, hijacked build systems, and poisoned artifacts (e.g., SolarWinds, Codecov).
- **SLSA Level 1**: Scripted build process generating build provenance.
- **SLSA Level 2**: Hosted build platform (GitHub Actions/Azure DevOps) generating tamper-evident provenance signed by the build service.
- **SLSA Level 3**: Isolated, ephemeral build environments where source code and provenance are cryptographically verified and unforgeable.

#### 2. Pipeline Security Best Practices
- **Secret Scanning**: Prevent secrets from entering git history via tools like `Gitleaks` in pre-commit hooks and GitHub Secret Scanning.
- **Static Application Security Testing (SAST)**: Analyze source code for OWASP vulnerabilities (e.g., CodeQL, SonarQube) on every PR.
- **Software Composition Analysis (SCA)**: Scan transitive NuGet packages for known CVEs (Dependabot, Snyk).
- **Branch Protection & Code Owners**:
  - Enforce `main` branch protection: require pull request reviews (minimum 2 approvals), require linear git history, require passing CI status checks, and restrict who can bypass protection rules.

---

### Section 12: Agile Delivery & Flow Metrics: Scrum Anti-Patterns, Kanban WIP Limits, Cycle Time & CFD

#### 1. Flow Metrics (Actionable Agile)
Story points are subjective estimates. Elite engineering teams rely on empirical flow metrics:
- **Work in Progress (WIP)**: The number of active items started but not finished. High WIP directly increases cycle time (Little's Law: $CycleTime = WIP / Throughput$).
- **Cycle Time**: The elapsed time from when an engineer starts working on an item to when it is delivered to production.
- **Throughput**: The count of completed work items delivered per unit of time (e.g., 14 PRs per week).
- **Cumulative Flow Diagram (CFD)**: Visualizes WIP, cycle time, and bottlenecks across states (To Do, In Progress, Review, Staging, Done). Expanding bands reveal systemic bottlenecks (e.g., items piling up in "Code Review").

#### 2. Common Scrum Anti-Patterns
- *Two-Week Waterfall*: Sprints where week 1 is all coding and week 2 is all QA/bug fixing.
- *Carrying Unfinished Work*: Rolling 40% of stories into the next sprint sprint after sprint, masking estimation dysfunction.
- *Story Point Velocity as Performance Metric*: Measuring developer productivity by velocity encourages story-point inflation and penalty for refactoring tech debt.

---

### Section 13: Enterprise Change Management & Compliance: Automated Audit Trails, SOC 2 / ISO 27001 Compliance & Modern CAB

#### 1. Concept & Modernizing the CAB
Traditional enterprises rely on weekly Change Advisory Board (CAB) meetings where managers approve changes by reviewing PowerPoint decks. DORA research proves that manual CAB approvals **do not decrease failure rates**; they dramatically increase lead time and encourage massive, high-risk release batches.

#### 2. The Modern Compliance Paved Road
- For SOC 2 Type II and ISO 27001 compliance, auditors require evidence of:
  1. *Change Authorization*: Proof that every production change is mapped to an approved issue/ticket (Jira, Azure DevOps).
  2. *Segregation of Duties*: Proof that the person who authored the code is not the person who approved or deployed it.
  3. *Testing Evidence*: Automated verification logs showing passing unit/integration tests and zero high/critical CVEs.
- *Automated Pipeline Attestation*: The CI/CD pipeline attaches cryptographic signatures and audit metadata to the container image (Cosign / Notation), publishing the evidence automatically to compliance storage.

---

### Section 14: DevOps Capstone: End-to-End GitOps on Azure AKS with Bicep, Canary Rollout & Sev-1 Postmortem

#### 1. Architecture Specification
Design and implement a complete enterprise progressive delivery pipeline:
1. **Infrastructure**: Azure AKS cluster provisioned via modular Bicep templates with User-Assigned Managed Identity and Azure CNI.
2. **Container Build**: .NET 9 Web API compiled into an Ubuntu Chiseled non-root container image and published to Azure Container Registry (ACR).
3. **Deployment**: Progressive Canary delivery managed via Argo CD / Flux GitOps and Flagger using Prometheus metrics to automatically promote or roll back based on HTTP error rates.
4. **Postmortem Artifact**: A real-world Sev-1 postmortem report detailing a production memory exhaustion incident caused by a missing Linux cgroup configuration.

---

# Part III — Interview Readiness

### 1. Mid-Level vs Senior vs Staff Engineer Comparisons

| Topic / Scenario | Mid-Level Response | Senior Engineer Response | Staff / Principal Response |
|---|---|---|---|
| **DORA Metrics** | "We track velocity in Jira and measure how many story points we finish each sprint." | "We track the four DORA metrics: Deployment Frequency, Lead Time for Changes, Change Failure Rate, and MTTR. We prioritize small batch sizes and trunk-based development to keep Lead Time under 2 hours." | "DORA metrics serve as our operational health baseline. We link DORA metrics to developer cognitive load and organizational throughput, establishing self-service internal platforms to eliminate cross-team wait states." |
| **Deploying Database Migrations** | "We run `context.Database.Migrate()` in `Program.cs` when the app starts up so the database is always updated automatically." | "Running migrations on container boot causes race conditions and deadlocks when multiple replicas spin up. We generate idempotent SQL migration scripts in CI and execute them as an isolated pipeline gate using expand/contract patterns before new app versions deploy." | "We mandate decoupled database evolution across all services. Schemas must maintain backward and forward compatibility (N-1 support). Schema migrations are fully automated, verified against ephemeral production data clones in CI, and audited for zero table locks." |
| **Kubernetes Health Probes** | "We point liveness and readiness probes to `/health` which checks SQL, Redis, and external APIs." | "Checking external dependencies like SQL in a liveness probe is dangerous: if SQL blips, Kubernetes kills all healthy app pods, turning a transient database blip into a total cluster restart loop. Liveness checks internal process health only; readiness checks dependencies." | "We design standardized probe architecture across the enterprise platform. Probes are paired with graceful shutdown lifecycle hooks (`SIGTERM` handling, draining connections, unregistering from ingress) and Startup Probes for high-JIT services." |
| **CI/CD Azure Authentication** | "We create a Service Principal with a client secret password and save it in GitHub Actions Secrets." | "Client secrets expire, risk exposure in logs, and require manual rotation. We configure OIDC Workload Identity Federation between GitHub Actions and Entra ID, allowing ephemeral, cryptographically verified tokens with zero static secrets." | "We enforce zero-secret CI/CD pipelines across all enterprise repos via Azure Policy and GitHub organization rulesets. CI runners run on ephemeral, hardened private runner clusters with restricted egress." |
| **Production Incident Response** | "I jump into production logs or connect a debugger to figure out why the code crashed." | "Mitigate first, debug later. As Incident Commander or responder, my primary goal is restoring customer service immediately via rollback, feature flag toggle, or traffic shifting. Deep debugging happens post-mitigation, followed by a blameless postmortem." | "I architect the incident command hierarchy, establish clear severity definitions, lead high-stakes executive crisis communications, and steer postmortems toward structural systemic remedies (chaos experiments, automated blast-radius limits)." |

---

### 2. 50-Truth Rapid-Fire Revision Sheet

1. DevOps is a cultural and operational model centered on flow, feedback, and continuous learning—not a tooling stack or job title.
2. The CALMS framework stands for Culture, Automation, Lean, Measurement, and Sharing.
3. The Three Ways are Flow (left-to-right), Feedback Loops (right-to-left), and Continuous Learning and Experimentation.
4. The four core DORA metrics are Deployment Frequency, Lead Time for Changes, Change Failure Rate, and Time to Restore Service.
5. Elite DORA performers deploy multiple times per day with lead times under an hour and MTTR under an hour.
6. Git is an immutable, content-addressable storage engine whose primary objects are Blobs, Trees, Commits, and Annotated Tags.
7. A Git Blob stores file contents only—it does not store filenames, directory paths, or modification timestamps.
8. Git Trees store directory structures, mapping file modes and filenames to Blob or subtree SHA hashes.
9. Git Commits point to a root Tree object, zero or more parent commit SHAs, author/committer metadata, and a message.
10. `git merge` preserves historical branch topology by creating a 3-way merge commit with two parents.
11. `git rebase` replays commits onto a new base, rewriting commit history to produce a linear commit graph.
12. `git merge --squash` condenses a branch's commits into a single commit on the destination branch, keeping main bisectable.
13. `git bisect` uses binary search across the commit graph to find the exact commit introducing a bug in $O(\log N)$ steps.
14. GitFlow causes long-lived branch divergence, merge conflicts, delayed feedback, and release batching delays.
15. Trunk-Based Development mandates small, frequent merges into `main` (<24 hour branch lifespan) paired with feature flags.
16. Central Package Management (CPM) via `Directory.Packages.props` locks NuGet package versions centrally across a solution.
17. Deterministic compilation (`<Deterministic>true</Deterministic>`) produces byte-identical binaries from the same source code.
18. A Software Bill of Materials (SBOM) details all direct and transitive dependencies and is vital for supply chain security.
19. Slow CI pipelines degrade engineering velocity by encouraging context switching and discouraging frequent integration.
20. Caching NuGet package directories based on hash keys cuts CI pipeline build durations significantly.
21. OIDC federated credentials eliminate long-lived service principal client secrets in GitHub Actions and Azure DevOps.
22. An OIDC token issued by GitHub Actions is exchanged for a short-lived Entra ID access token valid for 60 minutes.
23. The "Build Once, Deploy Many" principle mandates compiling binaries once and promoting that exact immutable artifact across environments.
24. Environment configuration must be injected externally via environment variables, ConfigMaps, or Key Vault at runtime.
25. Automated database migrations should never run inside application container startup code in scaled environments.
26. Database migrations must be generated as idempotent scripts and executed as dedicated pipeline gates using expand/contract strategies.
27. Rolling updates incrementally replace old pods with new pods with zero downtime, but run mixed versions concurrently.
28. Blue-Green deployments run two identical production environments and swap traffic instantly, providing fast rollback at 2x cost.
29. Canary deployments route a small fraction (e.g. 5%) of live traffic to the new version to monitor telemetry before full rollout.
30. Feature flags decouple software deployment from business feature release, enabling dark launches and instant rollbacks.
31. Production Docker images should use multi-stage builds and minimal, shell-less base images such as Ubuntu Chiseled or Distroless.
32. Running containers as non-root (`USER $APP_UID`) prevents attackers from exploiting host root vulnerabilities.
33. Kubernetes Startup Probes protect slow-starting applications by disabling liveness and readiness checks during initialization.
34. Kubernetes Liveness Probes restart containers if they become unresponsive, and must never check downstream dependencies like databases.
35. Kubernetes Readiness Probes remove pods from service endpoints when external dependencies are unavailable without restarting the container.
36. Bicep is an Azure-native declarative language transpiled to ARM templates with day-zero Azure support and no state file management.
37. Terraform uses HCL and manages state files externally, requiring storage locking to prevent concurrent state corruption.
38. Infrastructure drift occurs when resources are modified out-of-band via cloud portals instead of declarative IaC code.
39. User-Assigned Managed Identities provide passwordless authentication from Azure compute resources to other Azure services.
40. OpenTelemetry provides a vendor-neutral observability standard covering Tracing, Metrics, and Logging.
41. In .NET, `System.Diagnostics.Activity` represents an OpenTelemetry Span and `ActivitySource` acts as the Tracer.
42. Kusto Query Language (KQL) is used to query Azure Log Analytics, Application Insights, and Azure Resource Graph.
43. High-cardinality metric dimensions (e.g. user IDs, order IDs) can overwhelm time-series databases; use spans or logs instead.
44. Multi-window multi-burn-rate alerting alerts on error budget consumption rates rather than arbitrary instantaneous thresholds.
45. In Sev-1 production incidents, the priority is mitigation and service restoration first, not root-cause debugging.
46. The Incident Commander coordinates response and communication, deliberately abstaining from hands-on debugging.
47. Blameless postmortems investigate systemic failure mechanisms and process weaknesses rather than assigning personal blame.
48. The SLSA framework defines standards for protecting software artifacts and build pipelines against supply chain attacks.
49. According to Little's Law ($CycleTime = WIP / Throughput$), reducing Work in Progress directly reduces delivery cycle time.
50. Manual Change Advisory Boards (CABs) do not reduce change failure rates; automated testing and small batch sizes do.

---

### 3. Self-Assessment Rubric

| Level | Criteria & Capabilities |
|---|---|
| **Developing (Mid-Level)** | Understands basic Git commands (commit, push, pull, branch). Can write a basic CI pipeline in GitHub Actions or Azure DevOps. Deploys apps using Docker. Writes application logs using standard logging frameworks. |
| **Proficient (Senior)** | Masters Git DAG manipulation (`rebase`, `bisect`, `reflog`). Enforces trunk-based development and CPM across solutions. Implements secure CI/CD using OIDC without static credentials. Architectures zero-downtime rolling and canary rollouts. Configures OpenTelemetry, KQL queries, and SLO burn-rate alerts. Leads blameless incident postmortems. |
| **Exemplary (Staff / Principal)** | Designs enterprise-wide platform engineering golden paths. Drives organizational DORA metrics improvements. Enforces supply chain security (SLSA, SBOM, provenance signing) across all repositories. Establishes incident management command structures and disaster recovery game days. Replaces legacy CABs with continuous compliance pipelines. |

---

# Part IV — References

1. **Forsgren, N., Humble, J., & Kim, G. (2018).** *Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations.* IT Revolution Press.
2. **Humble, J., & Farley, D. (2010).** *Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation.* Addison-Wesley.
3. **Kim, G., Debois, P., Willis, J., Humble, J., & Allspaw, J. (2016).** *The DevOps Handbook: How to Create World-Class Agility, Reliability, and Security in Technology Organizations.* IT Revolution Press.
4. **Beyer, B., Jones, C., Petoff, J., & Murphy, N. R. (2016).** *Site Reliability Engineering: How Google Runs Production Systems.* O'Reilly Media.
5. **Beyer, B., Murphy, N. R., Rensin, D. K., Kawahara, K., & Thorne, S. (2018).** *The Site Reliability Workbook: Practical Ways to Implement SRE.* O'Reilly Media.
6. **Skelton, M., & Pais, M. (2019).** *Team Topologies: Organizing Business and Technology Teams for Fast Flow.* IT Revolution Press.
7. **Chacon, S., & Straub, B. (2014).** *Pro Git (2nd Edition).* Apress. Available free online at [git-scm.com/book](https://git-scm.com/book/en/v2).
8. **Vacanti, D. S. (2015).** *Actionable Agile Metrics for Predictability: An Introduction.* Daniel S. Vacanti, Inc.
9. **Microsoft Learn:** *OpenID Connect (OIDC) with Azure and GitHub Actions / Azure Pipelines.*
10. **Microsoft Learn:** *Azure Bicep Documentation & Best Practices.*
11. **OpenTelemetry.io:** *OpenTelemetry .NET Documentation and Instrumentation Architecture.*
12. **SLSA Specification:** *Supply-chain Levels for Software Artifacts (slsa.dev).*
