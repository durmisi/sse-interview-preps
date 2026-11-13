# Senior Software Engineer: Enterprise Onboarding & Delivery Playbook

**Purpose:** A practical guide for joining and becoming effective in a complex engineering organization. It covers how to understand the organization, work with Jira and Confluence, communicate professionally, develop in VS Code, use AI coding tools responsibly, estimate work, implement and test changes, document systems, review pull requests, release software, and support production.

**Intended environment:** A multi-team enterprise engineering organization using Jira, Confluence, VS Code, Git-based source control, CI/CD, automated testing, APIs, databases, cloud infrastructure and production services. Examples use C#/.NET, SQL Server and React where useful, but the practices apply more broadly.

**Important:** This is a starting playbook, not a replacement for company policy. During onboarding, discover and follow the organization's actual Jira workflow, Definition of Ready, Definition of Done, branching strategy, security rules, architecture standards, release approvals, incident process and approved AI-tool policy. Do not impose the templates or processes in this document on a team without first understanding its existing conventions.

---

## Table of contents

1. [The senior engineer's operating principles](#1-the-senior-engineers-operating-principles)
2. [The end-to-end engineering lifecycle](#2-the-end-to-end-engineering-lifecycle)
3. [First week: organizational onboarding](#3-first-week-organizational-onboarding)
4. [Understand the business and product](#4-understand-the-business-and-product)
5. [Jira: manage and describe work](#5-jira-manage-and-describe-work)
6. [Requirements, refinement and acceptance criteria](#6-requirements-refinement-and-acceptance-criteria)
7. [Estimation and forecasting](#7-estimation-and-forecasting)
8. [Confluence: manage engineering knowledge](#8-confluence-manage-engineering-knowledge)
9. [Architecture and system discovery](#9-architecture-and-system-discovery)
10. [VS Code: professional development workflow](#10-vs-code-professional-development-workflow)
11. [AI-assisted software engineering](#11-ai-assisted-software-engineering)
12. [Implementation quality and maintainable code](#12-implementation-quality-and-maintainable-code)
13. [Testing and verification](#13-testing-and-verification)
14. [Code and API documentation](#14-code-and-api-documentation)
15. [Git, branches, commits and pull requests](#15-git-branches-commits-and-pull-requests)
16. [Code review](#16-code-review)
17. [Professional communication](#17-professional-communication)
18. [Releases, deployments and database changes](#18-releases-deployments-and-database-changes)
19. [Production operations and incident response](#19-production-operations-and-incident-response)
20. [Security, privacy and responsible engineering](#20-security-privacy-and-responsible-engineering)
21. [Senior-level ownership and technical leadership](#21-senior-level-ownership-and-technical-leadership)
22. [30/60/90-day plan](#22-306090-day-plan)
23. [Daily, weekly and per-ticket routines](#23-daily-weekly-and-per-ticket-routines)
24. [Practical training plan and exercises](#24-practical-training-plan-and-exercises)
25. [Glossary](#25-glossary)
26. [Reference material](#26-reference-material)

---

# 1. The senior engineer's operating principles

A senior engineer is not simply a developer who writes more code or knows more frameworks. A senior engineer reduces uncertainty, makes sound trade-offs, delivers reliable outcomes and improves the effectiveness of the people and systems around them.

Use these principles as your default operating model:

1. **Understand before changing.** Learn the business context, existing design, operational constraints and history before proposing a significant change.
2. **Own outcomes, not just tickets.** Follow work from clarification through implementation, verification, review, release and operational confirmation.
3. **Make uncertainty visible.** State assumptions, unknowns, dependencies, risks and confidence instead of manufacturing certainty.
4. **Communicate early.** Raise blockers, risks, scope changes and missed expectations while there is still time to respond.
5. **Prefer small, reversible changes.** Small changes are easier to understand, test, review, deploy and recover.
6. **Respect the team's operating model.** Learn how decisions are made and who owns systems. Do not bypass established ownership or governance.
7. **Optimize for the whole lifecycle.** Consider security, performance, testability, observability, deployment, support and maintenance—not just implementation.
8. **Use evidence.** Base technical claims on code, tests, logs, metrics, traces, production behavior and documented decisions.
9. **Challenge ideas, not people.** Be direct about technical concerns while remaining respectful and open to counter-evidence.
10. **Keep learning and improve the system.** Turn recurring problems into prioritized, actionable improvements.

## 1.1 What good senior behavior looks like

| Situation | Senior behavior |
|---|---|
| You do not understand a subsystem | Ask a focused question, trace the flow, find the owner and document what you learn. |
| A requirement is ambiguous | Identify the ambiguity and its impact; ask the product/domain owner to decide. |
| You disagree with an architectural choice | Explain evidence, constraints, alternatives and trade-offs; follow the decision process. |
| You discover a security or data-integrity risk | Raise it promptly through the approved channel and avoid exposing users to the risk. |
| A task is taking longer than expected | Reassess scope and assumptions, communicate the revised outlook and propose options. |
| Your PR receives criticism | Separate the technical feedback from personal feelings; clarify, improve or explain with evidence. |
| A production issue occurs | Help stabilize the service, coordinate, communicate facts and learn without blame. |
| You notice technical debt | Describe impact and propose a proportionate, prioritized improvement rather than demanding a rewrite. |

## 1.2 What not to do when joining

- Do not declare the architecture wrong before understanding its constraints and history.
- Do not rewrite a subsystem just because you prefer a different pattern or technology.
- Do not make production changes without the required authorization and release process.
- Do not silently expand ticket scope.
- Do not promise dates before understanding dependencies and uncertainty.
- Do not treat story points, commit counts, lines of code or PR counts as individual productivity measures.
- Do not paste company code, customer data, credentials or confidential documents into unapproved AI tools.
- Do not close work simply because the code has been committed. Confirm the team's actual completion criteria.

---

# 2. The end-to-end engineering lifecycle

A typical change moves through the following lifecycle. The exact order and gates vary, but the engineer should understand every stage.

```text
Business need
    ↓
Discovery and requirements
    ↓
Jira epic / story / task / bug / spike
    ↓
Refinement and estimation
    ↓
Technical analysis and design
    ↓
Confluence design / ADR (when warranted)
    ↓
VS Code: investigate → plan → implement
    ↓
Automated tests and local verification
    ↓
Git commit and pull request
    ↓
Peer review and approval
    ↓
CI quality gates and artifact creation
    ↓
Test / staging validation
    ↓
Release approval and deployment
    ↓
Production verification and monitoring
    ↓
Documentation and Jira follow-up / closure
    ↓
Learning and continuous improvement
```

## 2.1 Tool responsibilities

| Tool | Primary purpose | What belongs there |
|---|---|---|
| Jira | Work tracking and delivery coordination | Scope, issue status, acceptance criteria, ownership, priority, dependencies, estimates, links and progress. |
| Confluence | Shared organizational knowledge | Business context, technical designs, architecture, decisions, how-to guides, runbooks and incident reviews. |
| VS Code | Development and debugging | Source code, tests, debugger, terminal, Git changes and approved AI assistance. |
| Git hosting (GitHub / Azure Repos / other) | Source collaboration | Commits, branches, pull requests, review discussion and merge history. |
| CI/CD platform | Automated validation and delivery | Builds, tests, scans, artifacts, deployments, approvals and pipeline history. |
| Observability platform | Runtime understanding | Logs, metrics, traces, dashboards, alerts and service health. |

Keep a clear source of truth. Link related artifacts instead of copying the same information into several places that can drift apart.

---

# 3. First week: organizational onboarding

Your first week is about learning how the organization actually works. The organizational chart is only one source of information; understand practical ownership, influence, decision rights and escalation paths too.

## 3.1 Identify the people and their responsibilities

| Role | What to learn |
|---|---|
| Engineering Manager | Team goals, performance expectations, capacity, priorities, feedback and escalation. |
| Tech Lead | Team-level technical direction, engineering conventions and local decision-making. |
| Software / Solution Architect | Cross-system boundaries, architecture standards and major design decisions. |
| Product Owner / Product Manager | Product outcomes, priorities, roadmap and acceptance decisions. |
| Business Analyst / Domain Specialist | Business rules, workflows, terminology, exceptions and stakeholders. |
| QA Engineer / Test Engineer | Test strategy, environments, acceptance testing and defect process. |
| Platform / DevOps Engineer | Build and release pipelines, infrastructure, deployment, secrets and operational support. |
| Security / Privacy | Security requirements, threat reviews, data classification and incident escalation. |
| Developers / Service Owners | Codebase history, system behavior, support responsibilities and practical conventions. |

One person may hold several roles. Do not assume every organization has a dedicated architect, QA team or product owner.

## 3.2 Build a stakeholder and system-owner map

Create a private onboarding note (in an approved company location) with fields such as:

| Person / team | Responsibility | Systems owned | Decisions they make | How to contact |
|---|---|---|---|---|
| Engineering Manager | Team leadership | Team delivery | Priorities / people | Team channel / 1:1 |
| Tech Lead | Technical direction | Team services | Local design | Engineering channel |
| Product Owner | Product priorities | Product backlog | Scope / acceptance | Product channel |
| Platform team | Runtime platform | CI/CD / infrastructure | Platform operations | Support channel |

Do not record sensitive personal details or speculative judgments. Keep the map factual and update it as you learn.

## 3.3 Questions for your manager

Ask these during the first few conversations. Do not fire all questions at once; use the context of the discussion.

- What outcomes would make my first 30, 60 and 90 days successful?
- Which product or system should I learn first?
- What responsibilities should I gradually own?
- How are technical decisions made in this team?
- Which decisions can I make independently, and which require alignment?
- What are the team's biggest delivery or operational challenges?
- How do you prefer updates about progress, risk and blockers?
- What is the expected balance between feature work, maintenance and support?
- Is there an on-call or incident-support responsibility?
- Are there organizational, regulatory or customer constraints I should understand?
- Where are engineering standards, runbooks and architecture decisions documented?

## 3.4 First-week meeting behavior

- Listen more than you speak.
- Introduce your relevant experience without trying to prove yourself in every conversation.
- Learn names, responsibilities, terminology and team boundaries.
- Take notes and confirm important decisions.
- Ask where authoritative documentation lives.
- Do not assume a meeting decision is final unless the decision owner confirms it.
- Follow up on actions you accept.

Useful phrases:

- "Could you walk me through the reasoning behind this design?"
- "Is this convention used across the organization or only in this service?"
- "Who owns this integration and its production support?"
- "Where is the current decision documented?"
- "Before changing this behavior, I'd like to understand the compatibility constraints."

## 3.5 First-week checklist

- [ ] Understand team structure and responsibilities.
- [ ] Know your manager, tech lead and relevant system owners.
- [ ] Join the correct team channels and recurring meetings.
- [ ] Obtain approved access to repositories, Jira, Confluence and development environments.
- [ ] Understand how to request access and report an access/security issue.
- [ ] Learn the team's workflow and communication expectations.
- [ ] Identify the first system or bounded area to study.
- [ ] Agree on what success looks like for the first month.
- [ ] Know who to contact for development, test-environment and production issues.

---

# 4. Understand the business and product

Do not learn a codebase in isolation. Understand the users, business processes and consequences of incorrect behavior.

## 4.1 Questions to answer

- Who uses the product: employees, managers, customers, partners, administrators or other systems?
- What business problem does it solve?
- Which workflows are financially, legally or operationally critical?
- What are the important domain concepts and their definitions?
- Which data is sensitive or regulated?
- What are the main integrations and who owns them?
- What does the user consider a successful outcome?
- What happens if the system is unavailable, delayed or produces incorrect data?
- What are the known customer pain points and roadmap priorities?

## 4.2 Trace one important business workflow

For a workforce-management example:

```text
Employee starts shift
    ↓
Clock-in request
    ↓
Authentication and authorization
    ↓
Attendance validation
    ↓
Timestamp persistence
    ↓
Event publication / downstream processing
    ↓
Manager review of exceptions
    ↓
Timesheet approval
    ↓
Payroll integration
```

For each step, understand:

- Which component owns the behavior?
- Which data is authoritative?
- What are the business invariants?
- What can fail?
- Are retries possible, and are operations idempotent?
- What happens when components disagree?
- What is the user-visible fallback?
- How is the behavior audited and monitored?

## 4.3 Learn the domain language

Maintain a small glossary of terms, definitions, synonyms and domain owners. Do not assume ordinary words have ordinary meanings in the product. Terms such as "shift", "working day", "attendance", "approval", "employee", "organization" and "pay period" may have precise business meanings.

When a rule is ambiguous, ask the domain owner. Do not invent a rule in code.

---

# 5. Jira: manage and describe work

Jira is the team's work-management system. Learn the exact project/space configuration, issue types, workflow statuses, required fields, permissions and conventions before relying on generic Jira terminology.

Recent Jira Cloud documentation uses the term **work item** in parts of the interface. Many organizations and teams still say **issue** or use customized issue types. The labels and hierarchy depend on configuration.

## 5.1 Understand the common work-item types

| Type | Use | Example |
|---|---|---|
| Initiative (if configured) | Strategic body of work spanning epics or teams | Workforce management modernization |
| Epic | Large capability composed of smaller work | Employee attendance management |
| Story | User or stakeholder outcome | Manager can view attendance history |
| Task | Engineering or operational work | Add correlation IDs to payroll logs |
| Bug | Existing behavior does not match expected behavior | Overnight shift totals are incorrect |
| Sub-task | A separately trackable part of a parent item | Add API integration tests |
| Spike / Research | Time-boxed investigation to reduce uncertainty | Investigate payroll event idempotency |
| Technical debt item | A known maintainability, reliability or security improvement | Remove duplicated authorization logic |

These are common examples, not a required universal hierarchy. Ask which work types the team actually uses.

## 5.2 Rules for good ticket titles

A title should be specific, searchable and outcome-oriented. Avoid vague titles such as "Improve API", "Fix issue" or "Update code".

Useful patterns:

- Story: `Allow managers to filter attendance history by employee and date range`
- Bug: `[Attendance API] Returns incorrect duration for overnight shifts`
- Engineering task: `[Payroll Integration] Add correlation identifiers to failure logs`
- Spike: `[Payroll Integration] Investigate duplicate event processing`

Use the team's component, product and naming conventions where they exist.

## 5.3 Structured Jira Story template

```markdown
## Background / business context
Why is this needed? What problem or opportunity does it address?

## User story
As a [user / stakeholder],
I want [capability],
so that [business value / outcome].

## Scope
- Included behavior.
- Included scenarios.
- Relevant components or user journeys.

## Acceptance criteria
1. Given [context], when [action], then [observable result].
2. Given [context], when [action], then [observable result].

## Out of scope
- Explicit exclusions.

## Dependencies
- Services, teams, approvals, environments or data required.

## Constraints / business rules
- Confirmed rules only. Mark unresolved rules as questions.

## Technical considerations
- Known implementation constraints, security, compatibility or performance concerns.
- Do not prescribe implementation unnecessarily.

## UX / API / supporting links
- Designs, API contracts, Confluence pages, related tickets.

## Open questions
- Question, decision owner and due point if known.
```

### Example Story

**Title:** Allow managers to view employee attendance history

**Background:** Managers currently use multiple reports to investigate attendance discrepancies. A centralized view is needed.

**User story:** As a manager, I want to view an employee's attendance history so that I can investigate attendance discrepancies.

**Scope:**
- Display attendance records for a selected employee.
- Filter by a selected date range.
- Display clock-in and clock-out timestamps.
- Display the attendance record status.

**Acceptance criteria:**

1. Given an authorized manager, when they open an employee's attendance history, then records for that employee are displayed.
2. Given a selected date range, when the manager applies the filter, then only records matching the agreed date-boundary rules are returned.
3. Given no records in the selected range, when the history is opened, then an appropriate empty state is displayed.
4. Given a user who is not authorized to access the employee, when they request the records, then access is denied.

**Open questions:**
- Does the date range refer to UTC timestamps, employee-local dates or shift dates?
- What organizational relationship makes a manager authorized to see an employee?

Do not mark the story as ready for development until the material business rules are decided or the team explicitly accepts the uncertainty and scope.

## 5.4 Structured Jira Bug template

```markdown
## Summary
One sentence describing the observed defect and affected area.

## Environment
- Environment: Dev / Test / Staging / Production
- Application version / build:
- Browser / client / device (if relevant):
- Tenant / organization (use approved non-sensitive identifiers):

## Preconditions
Data, configuration or state required to reproduce.

## Steps to reproduce
1.
2.
3.

## Expected result
What should happen, based on an authoritative requirement or known behavior?

## Actual result
What happens instead?

## Reproducibility
Always / Intermittent / Once / Not yet reproduced.

## Impact
Affected users, workflows, data, severity and known scope.

## Evidence
Screenshots, sanitized logs, trace/correlation IDs, request samples.
Do not paste secrets, tokens or unnecessary personal data.

## Workaround
Known safe workaround, or None known.

## Related items
Links to requirements, incidents, PRs or other bugs.
```

A bug should explain the difference between expected and actual behavior. If expected behavior is unknown, record that as a requirements question rather than guessing.

## 5.5 Structured Engineering Task template

```markdown
## Context
What technical or operational problem exists?

## Objective
What outcome should this task achieve?

## Scope
- Included work.
- Explicit exclusions.

## Acceptance criteria / completion checks
- Observable or verifiable outcomes.
- Relevant automated checks.

## Dependencies
- Teams, services, approvals, environments or other tickets.

## Risks / constraints
- Security, compatibility, performance, support or deployment concerns.

## Documentation / operational impact
- Pages, API specs, runbooks, dashboards or alerts to update.

## Related items
- Jira / Confluence / PR links.
```

## 5.6 Structured Spike template

```markdown
## Question / uncertainty
What decision cannot currently be made confidently?

## Context
What is known and what evidence has already been collected?

## Objective
What should the investigation determine?

## Investigation areas
- Code / architecture.
- Data / integrations.
- Operational behavior.
- Alternatives and constraints.

## Timebox
Agreed maximum investigation time.

## Expected deliverables
- Findings.
- Options and trade-offs.
- Recommendation (if evidence supports one).
- Risks and open questions.
- Follow-up Jira items.

## Out of scope
Implementation unless explicitly included.
```

A Spike must have a clear question, timebox and useful output. It should not become unbounded research.

## 5.7 Acceptance criteria quality

Good acceptance criteria are:

- Observable: a tester or stakeholder can see whether they pass.
- Testable: a clear method exists to verify them.
- Specific: avoid ambiguous adjectives such as "fast", "robust", "easy" or "appropriate" without a definition.
- Focused: each criterion describes one coherent behavior or condition.
- At the right level: describe required behavior, not unnecessary internal implementation details.
- Consistent: do not contradict other requirements or policies.

Cover the relevant scenarios:

- Happy path.
- Validation failures.
- Authorization and access boundaries.
- Empty states and missing data.
- Boundary values and date/time behavior.
- Duplicate requests and concurrency, where relevant.
- Dependency timeouts and failures.
- Backward compatibility and migration behavior.

### Given / When / Then example

```text
Given an employee has a valid open attendance session
When the employee clocks out
Then the system records the clock-out timestamp
and marks the attendance session as completed.
```

Use a separate scenario for an employee who has no open session, a duplicate request, or an unauthorized caller.

## 5.8 Definition of Ready (example, adapt to team)

A ticket may be ready for refinement or development when:

- [ ] The business outcome is understood.
- [ ] Scope and exclusions are reasonably clear.
- [ ] Acceptance criteria are testable.
- [ ] Important business rules and edge cases are identified.
- [ ] Dependencies and decision owners are known.
- [ ] Designs, API contracts or data examples are linked where relevant.
- [ ] Material unknowns are resolved or explicitly accepted for investigation.
- [ ] The team can reasonably size the work.

Not every team uses a formal Definition of Ready. Treat this as a checklist for clarity, not a bureaucratic gate unless the team has adopted it.

## 5.9 Definition of Done (example, adapt to team)

- [ ] Acceptance criteria are met.
- [ ] Code follows repository conventions.
- [ ] Relevant automated tests pass.
- [ ] Security, authorization and validation implications are addressed.
- [ ] Code has been reviewed and approved according to policy.
- [ ] CI checks pass.
- [ ] API/code/operational documentation is updated where needed.
- [ ] Deployment and migration implications are addressed.
- [ ] Required acceptance or smoke tests are complete.
- [ ] Known limitations and follow-up work are recorded.
- [ ] The change is deployed or released if the team's workflow defines Done that way.

Be precise about whether "Done" means merged, deployed to an environment, released to users or accepted by the product owner. Teams define this differently.

## 5.10 Jira workflow habits

**When you take a ticket:**

1. Read the complete description, comments, acceptance criteria and linked material.
2. Check related tickets, bugs, designs and dependencies.
3. Confirm the expected outcome and decision owner.
4. Identify missing information before coding.
5. Understand the team's status workflow and WIP rules.

**While working:**

1. Keep the status accurate.
2. Add comments when new evidence, scope changes, blockers or decisions arise.
3. Link relevant PRs and design pages.
4. Raise blockers early and identify who can resolve them.
5. Do not use comments as a substitute for a needed requirements decision.

**When completing:**

1. Verify acceptance criteria.
2. Link the PR and tests/evidence where appropriate.
3. Record known limitations and follow-up tickets.
4. Update documentation.
5. Move the ticket according to the actual workflow.

---

# 6. Requirements, refinement and acceptance criteria

A senior engineer contributes to requirements quality even when a Product Owner or Business Analyst owns the requirement.

## 6.1 Ask questions in useful categories

| Category | Example question |
|---|---|
| User / actor | Who is allowed to perform this action? |
| Trigger | What event or condition starts the workflow? |
| Outcome | What should the user or downstream system observe? |
| Business rule | What rule determines whether the operation is valid? |
| Data | Which source is authoritative? What is required or optional? |
| Boundaries | What are the minimum, maximum, date and timezone rules? |
| Failure | What should happen when an integration is unavailable? |
| Security | Who may access or change this data? |
| Scale | What workload or data volume should be supported? |
| Compatibility | Must existing clients or integrations continue to work? |
| Operations | How will the behavior be monitored and supported? |

## 6.2 Functional and non-functional requirements

Functional requirements describe behavior: what the system does.

Non-functional requirements describe quality attributes and constraints: how well, under what conditions, and with what operational characteristics.

Examples of non-functional requirement categories:

- Performance and capacity.
- Availability and resilience.
- Security and privacy.
- Accessibility and usability.
- Compatibility and interoperability.
- Observability and supportability.
- Data retention and recoverability.
- Maintainability and deployability.

Do not invent numerical thresholds. Ask stakeholders for the required workload, environment, measurement method and target.

Example of an incomplete statement:

> The API must be fast.

Better requirement structure:

> Under [agreed workload and environment], [specified operation] should meet [agreed latency percentile/threshold], measured using [agreed test or telemetry method].

The placeholders must be decided by the relevant stakeholders.

## 6.3 Refinement meeting checklist

Before refinement:

- Read the ticket and linked documents.
- Understand the product goal.
- Identify obvious ambiguities.
- Inspect the relevant code or system only as much as needed.
- Prepare questions and possible dependencies.

During refinement:

- Confirm the problem and intended outcome.
- Discuss acceptance criteria and exceptions.
- Identify technical dependencies and constraints.
- Separate business decisions from implementation choices.
- Decide whether a Spike or design discussion is needed.
- Size only when the team has enough shared understanding.

After refinement:

- Update the ticket with agreed facts and decisions.
- Record open questions and owners.
- Link relevant Confluence documentation.
- Split oversized work where useful.

---

# 7. Estimation and forecasting

Estimation is an informed prediction, not a promise. Your job is to explain likely work, uncertainty, assumptions, dependencies and confidence.

## 7.1 Distinguish the terms

| Term | Meaning |
|---|---|
| Effort | Amount of work, often expressed in person-hours or person-days. |
| Duration / elapsed time | Calendar time between start and finish. |
| Complexity | Technical difficulty and interaction of components. |
| Uncertainty | How much is unknown or unverified. |
| Risk | An uncertain event or condition that may affect outcome. |
| Confidence | How reliable the estimate or forecast is, given current evidence. |
| Capacity | Available team time after leave, support, meetings and other commitments. |
| Throughput | Number of work items completed in a period. |
| Cycle time | Elapsed time from a defined start point to a defined completion point. |
| Lead time | Elapsed time from request/commitment to delivery, depending on the team's definition. |

Do not treat 3 developer-days as 3 calendar days automatically. Dependencies, reviews, waiting time, test environments and release windows affect elapsed time.

## 7.2 Relative estimation with story points

Story points are a team-specific relative sizing method. They are not hours, days, lines of code or an individual productivity score. Common considerations include work/effort, complexity and uncertainty/risk.

The Scrum Guide does not mandate story points or Fibonacci. It says the Developers responsible for the work are responsible for sizing Product Backlog items. Follow the team's established scale and calibration.

A common Fibonacci-like scale is:

| Points | Typical interpretation (illustrative only) |
|---:|---|
| 1 | Tiny, familiar, very limited change |
| 2 | Small, predictable change |
| 3 | Moderate, known implementation with several steps |
| 5 | Medium, multiple components or meaningful testing |
| 8 | Large, significant integration or uncertainty |
| 13 | Very large; examine whether it should be split or investigated |
| 21+ | Often too large or uncertain for useful story-level sizing |
| ? | Not enough information to estimate responsibly |

These are not universal definitions. Calibrate points using completed examples from your team.

### Reference stories

Ask the team to show previously completed work representing small, medium and large items. Compare a new story with those reference examples. This is more reliable than inventing a point scale in isolation.

### Planning Poker

1. Clarify the story and acceptance criteria.
2. Identify the main components, dependencies and risks.
3. Each participant selects an estimate privately.
4. Reveal estimates simultaneously.
5. Ask people with the highest and lowest estimates to explain what they saw.
6. Resolve different assumptions and missing information.
7. Re-estimate if needed and record the team's result.

Do not force artificial unanimity. If uncertainty remains, record it and consider a Spike or split.

### Never use story points to

- Compare individuals or teams.
- Rank developers.
- Set arbitrary productivity quotas.
- Convert directly into hours for every person.
- Treat a point total as a delivery guarantee.
- Encourage padding or point inflation.

Velocity is a local planning signal for a team using that scale. It is not a general measure of engineering value or quality.

## 7.3 Decompose before estimating

For a feature, inspect all relevant work dimensions:

- Business rules and validation.
- API or UI changes.
- Application and domain logic.
- Database queries, indexes and migrations.
- Authentication and authorization.
- Integrations and messaging.
- Concurrency, idempotency and transactions.
- Tests and test data.
- Documentation and observability.
- Deployment, configuration and support.

Estimate the complete deliverable, not only the code-writing activity.

## 7.4 Estimate effort in ranges

For tasks where hours or days are useful, decompose work into activities and provide a range.

Example only:

| Activity | Effort range |
|---|---:|
| Inspect existing implementation | 1–2 h |
| Implement query changes | 2–4 h |
| Add validation | 1–2 h |
| Unit and integration tests | 3–5 h |
| Documentation | 0.5–1 h |
| Local verification and debugging | 1–2 h |
| Review adjustments | 1–2 h |

The total of ranges is approximately 9.5–18 hours. This is not automatically a 1.5–2.5 calendar-day delivery commitment. State the capacity and dependency assumptions.

Avoid false precision. "About 1–2 days" can be more honest than "11.75 hours".

## 7.5 Three-point estimation

For an uncertain task, record:

- Optimistic (O): a reasonable best-case scenario.
- Most likely (M): the normal expected scenario.
- Pessimistic (P): a reasonable difficult scenario, not an impossible catastrophe.

A common PERT weighted estimate is:

`E = (O + 4M + P) / 6`

Example: O = 4 hours, M = 8 hours, P = 20 hours.

`E = (4 + 4×8 + 20) / 6 = 9.33 hours`

This is a planning model, not a guarantee or a substitute for understanding assumptions. Preserve the range (4–20 hours) and explain why it is wide.

## 7.6 T-shirt sizing

For early roadmap discussions, XS / S / M / L / XL can provide a quick rough size. It is useful before there is enough detail for implementation estimates. XL or XXL items usually need decomposition or discovery before delivery planning.

## 7.7 Forecast using historical data

For a Scrum team, use historical completed work, current capacity, the Definition of Done and known dependencies to inform a forecast. Do not divide a large feature's points by a single sprint's velocity and call the result a commitment.

For flow-based teams, useful data may include:

- Throughput: completed items per period.
- Cycle-time distribution: how long comparable items take.
- Work in progress.
- Age of currently active work.

With enough representative historical data, probabilistic methods such as Monte Carlo simulation can estimate a range of likely completion dates or throughput. Do not invent a confidence percentage; calculate it from relevant data and state the assumptions.

## 7.8 Estimation checklist

Before giving an estimate, ask:

- [ ] Do I understand the expected business outcome?
- [ ] Are acceptance criteria sufficiently clear?
- [ ] Which components must change?
- [ ] What can be reused?
- [ ] Are there unknown business rules?
- [ ] Are there external or internal dependencies?
- [ ] Are data changes, migrations or compatibility issues involved?
- [ ] Have I included testing, review, documentation and deployment considerations?
- [ ] What assumptions does the estimate rely on?
- [ ] What confidence level is justified?
- [ ] Should this be split or investigated first?

## 7.9 How to communicate an estimate

Use this structure:

```text
Scope:
What exactly is included?

Estimate:
Relative size and/or effort range, using the team's conventions.

Confidence:
High / Medium / Low, with a reason.

Assumptions:
What must be true for this estimate to hold?

Dependencies:
What input, access, decision or work is required from others?

Risks / unknowns:
What could materially change the estimate?

Exclusions:
What is not included?

Next step:
What would increase confidence?
```

Example message:

> I've reviewed the requirement and existing implementation. My current effort estimate is approximately 2–3 engineering days, with medium confidence. This assumes we can reuse the existing API and authorization mechanisms. The main uncertainty is how overnight shifts are represented in the data model. I recommend clarifying that business rule before finalizing the estimate. The range includes implementation, tests, documentation and normal review adjustments; it excludes a schema change if one proves necessary.

## 7.10 AI-assisted estimation

AI can help inspect a repository and identify likely changes, but it cannot know undocumented business rules, the team's actual capacity, every dependency or the team's historical calibration. Use it to challenge omissions, not to generate an authoritative number.

Example prompt:

```text
Act as a Senior Software Engineer performing a technical estimation.

Analyze Jira issue [JIRA-ID]. Do not modify files.

Investigate:
- Relevant components and dependencies.
- API and UI changes.
- Business logic and validation.
- Data model, queries and migrations.
- Authentication and authorization.
- Unit, integration and end-to-end testing.
- Security, performance and concurrency implications.
- Documentation, deployment and operational impact.

Produce:
1. A scope breakdown.
2. Proposed implementation activities.
3. Verified repository facts with file references.
4. Assumptions and unresolved questions.
5. Dependencies and risks.
6. Suggested sequence.
7. Indicative effort ranges, not a single falsely precise number.

Do not invent business rules. Distinguish facts from hypotheses.
Do not convert hours into story points.
Do not modify files. The engineering team owns the final estimate.
```

## 7.11 Review estimation accuracy without blame

In retrospectives, compare estimates with outcomes to learn:

- Was the original scope understood?
- Were hidden dependencies missed?
- Was testing or review effort omitted?
- Did unplanned work interrupt the task?
- Did the requirement change?
- Was the estimate reasonable given what was known at the time?

The purpose is to improve the process and shared understanding, not punish people for uncertainty.

---

# 8. Confluence: manage engineering knowledge

Jira records work and delivery status. Confluence should preserve useful knowledge that people need to understand, change, operate and support systems.

## 8.1 Common document types

| Document | Purpose | Typical audience |
|---|---|---|
| Product / business overview | Explain capabilities, users and domain terms | Product and engineering |
| Architecture overview | Explain systems, boundaries and dependencies | Engineers, architects, operations |
| Technical design | Explain a proposed change and alternatives | Implementers, reviewers, owners |
| ADR | Record an important technical decision and rationale | Current and future engineers |
| API guide | Explain API usage and contracts | Internal/external consumers |
| Developer guide | Explain local setup and development conventions | Developers |
| Runbook | Explain operational tasks and recovery | On-call and operations |
| Incident review | Record impact, timeline, response and learning | Relevant teams and stakeholders |
| Meeting notes | Record decisions, actions and unresolved questions | Participants and affected teams |

## 8.2 Technical design template

```markdown
# [Feature / System] — Technical Design

## Status
Draft / In review / Accepted / Superseded

## Owners and reviewers
Decision owner, author, relevant teams.

## Context
Business and technical background.

## Problem statement
What problem are we solving? What is the impact?

## Goals
What outcomes should the design achieve?

## Non-goals
What is explicitly outside the design?

## Requirements and constraints
Functional requirements, NFRs, compatibility, security and compliance.

## Current state
Existing architecture and behavior. Link authoritative diagrams.

## Proposed design
Components, responsibilities, interactions, contracts and data flow.

## Alternatives considered
Options, benefits, costs and reasons for selection.

## Data and migration
Schema, ownership, backfill, compatibility and rollback implications.

## Failure modes and resilience
Timeouts, retries, duplicate messages, partial failure and recovery.

## Security and privacy
Authentication, authorization, data classification, secrets and audit.

## Performance and scalability
Expected workload, bottlenecks and validation method.

## Testing strategy
Unit, integration, contract, end-to-end, performance and security tests.

## Deployment and rollback
Release sequence, feature flags, migration order and recovery plan.

## Observability and support
Logs, metrics, traces, dashboards, alerts and runbook changes.

## Open questions
Unresolved decisions, owners and next steps.

## Related work
Jira items, PRs, ADRs and API specifications.
```

## 8.3 Architecture Decision Record template

Use ADRs for decisions with meaningful long-term consequences, not every local coding choice.

```markdown
# ADR-XXX: [Decision title]

- Status: Proposed / Accepted / Rejected / Superseded
- Date:
- Decision owners:

## Context
What forces, constraints or problems require a decision?

## Decision
What are we choosing?

## Options considered
What realistic alternatives were considered?

## Rationale
Why does the selected option fit the constraints?

## Consequences
Positive, negative and operational consequences.

## Follow-up actions
What needs to be implemented or monitored?

## Related decisions and work
Links to ADRs, Jira, design documents and PRs.
```

## 8.4 Runbook template

```markdown
# [Service] — Operational Runbook

## Purpose and scope
What service or scenario does this cover?

## Service owner and escalation
Team, on-call route and escalation contact/channel.

## Dependencies
Upstream/downstream services and infrastructure.

## Normal health signals
Dashboards, SLOs, alerts and expected behavior.

## Common alerts and symptoms
What the operator may observe.

## Diagnostic steps
Safe commands, dashboards, logs, traces and checks.

## Mitigation / recovery
Approved steps, prerequisites, risks and verification.

## Rollback / roll-forward
When and how to use the approved recovery options.

## Data safety warnings
Actions that can cause data loss or inconsistency.

## Verification
How to confirm service and business recovery.

## Related incidents and documentation
Links to postmortems, ADRs and architecture pages.

## Last reviewed
Date and responsible owner.
```

## 8.5 Meeting notes template

```markdown
# [Meeting] — YYYY-MM-DD

## Purpose

## Participants / roles

## Topics discussed

## Decisions
- Decision:
- Decision owner:
- Rationale:

## Action items
- [ ] Action — owner — due date

## Open questions
- Question — owner / next step

## References
Jira, Confluence, PRs, diagrams.
```

## 8.6 Documentation quality rules

- Give every important page an owner and review/update expectation.
- Put the intended audience and purpose near the top.
- Separate confirmed facts, proposals, assumptions and unresolved questions.
- Date consequential decisions and state their status.
- Link to the source of truth rather than duplicating specifications.
- Use diagrams when they improve understanding, but explain the important behavior in text.
- Avoid pages that are long but unstructured or impossible to maintain.
- Remove or mark superseded material rather than leaving competing instructions.
- Never put passwords, tokens, private keys or sensitive customer data in documentation.

---

# 9. Architecture and system discovery

Do not begin by reading every class. Start with system boundaries and follow one business operation end-to-end.

## 9.1 Architecture discovery sequence

1. List applications, services, major modules and repositories.
2. Identify users and external systems.
3. Understand synchronous communication: HTTP, gRPC, direct SDK calls, etc.
4. Understand asynchronous communication: queues, topics, events and scheduled jobs.
5. Identify data stores and ownership boundaries.
6. Understand identity, authentication, authorization and service-to-service trust.
7. Map infrastructure and deployment topology.
8. Find observability dashboards, alerts and runbooks.
9. Trace one critical request and one asynchronous workflow.
10. Identify failure handling and operational ownership.

## 9.2 Questions for each service

- What business capability does it own?
- What is its public interface?
- Which systems call it?
- Which systems does it call?
- What data is authoritative here?
- What are its availability and performance expectations?
- How are authentication and authorization enforced?
- How are retries, timeouts and idempotency handled?
- What happens when a dependency is unavailable?
- How is it deployed and monitored?
- Who owns production support?

## 9.3 Trace an end-to-end request

For an ASP.NET Core API, a conceptual path could be:

```text
Browser / client
    ↓
Ingress / gateway / load balancer
    ↓
Kestrel and ASP.NET Core middleware
    ↓
Authentication and authorization
    ↓
Endpoint / controller
    ↓
Application use case
    ↓
Domain logic
    ↓
Persistence / external service / message broker
    ↓
Response or asynchronous result
```

Verify the actual path in the repository and runtime. Do not assume every application follows this exact design.

## 9.4 Create a lightweight system map

Record:

- System / service name.
- Business responsibility.
- Repository and owner.
- Interfaces and dependencies.
- Data stores.
- Deployment environment.
- Critical dashboards and runbooks.
- Known reliability or security constraints.

Use C4-style context and container diagrams where appropriate. Add component or sequence diagrams when the question needs more detail.

## 9.5 Do not make architecture changes without understanding

Before proposing a major change, understand:

- Existing constraints and historical decisions.
- Operational cost and team ownership.
- Consumer compatibility.
- Data migration and rollback implications.
- Security and compliance impact.
- Deployment and support complexity.
- Whether a smaller change solves the problem.

---

# 10. VS Code: professional development workflow

The objective is to become independently productive in the repository while following team conventions.

## 10.1 First repository setup checklist

- [ ] Read repository README and contribution guide.
- [ ] Confirm correct repository, branch and access permissions.
- [ ] Install only approved extensions and SDKs.
- [ ] Confirm required .NET SDK / Node.js / package-manager versions.
- [ ] Restore dependencies.
- [ ] Build the solution.
- [ ] Run the automated tests.
- [ ] Start the application locally.
- [ ] Debug a request or important code path.
- [ ] Understand required local services, containers and environment variables.
- [ ] Learn how configuration and secrets are provided safely.
- [ ] Identify formatting, analyzers and lint commands.
- [ ] Record setup problems in the appropriate onboarding channel or documentation.

## 10.2 VS Code capabilities to learn

| Capability | Practical use |
|---|---|
| Explorer | Understand folder and project structure. |
| Search / symbol search | Find usages, types, references and configuration. |
| Go to Definition / References | Follow code dependencies and contracts. |
| Git / Source Control | Inspect status, diff, staged changes and branch. |
| Integrated terminal | Build, test, run, format and diagnose. |
| Debugger | Breakpoints, call stack, locals, watches and exception behavior. |
| Test Explorer | Discover and run relevant tests. |
| Problems panel | Compiler, analyzer and language-server diagnostics. |
| Extensions | Add approved language, Git, container and productivity tooling. |
| AI Chat / Agent | Investigate, plan and perform bounded changes under supervision. |

## 10.3 .NET command-line workflow (adapt to the solution)

```bash
# Inspect installed SDKs
dotnet --info

# Restore dependencies
dotnet restore

# Build the solution or project
dotnet build

# Run tests
dotnet test

# Run one project
dotnet run --project path/to/Api.csproj

# Run tests with a filter (example)
dotnet test --filter FullyQualifiedName~Attendance

# Format according to repository configuration
dotnet format
```

Use the repository's documented commands. A monorepo or solution may have custom scripts, build orchestration or required environment setup.

## 10.4 Debugging discipline

When a defect occurs:

1. Reproduce it with a known input and environment.
2. Identify the expected and actual behavior.
3. Set a breakpoint at the boundary where behavior diverges.
4. Inspect call stack, arguments, state and relevant data.
5. Check asynchronous continuations and exception paths where applicable.
6. Inspect database queries or outgoing HTTP requests safely.
7. Form a hypothesis and test it.
8. Fix the underlying cause, not only the visible symptom.
9. Add a regression test.
10. Verify the relevant behavior again.

Avoid random breakpoint placement or speculative code changes before reproducing the problem.

## 10.5 Learn the repository's Git model

Ask whether the team uses trunk-based development, short-lived feature branches, release branches or another model. Do not introduce a branching strategy on your own.

Understand:

- How branches are named.
- Whether commits are squashed or preserved.
- Whether direct pushes to main are prohibited.
- Required PR approvals.
- Merge strategy.
- How hotfixes are handled.
- How tags and release branches are created.

### A generic feature-branch flow

```bash
git status
git switch main
git pull --ff-only
git switch -c feature/ATT-315-attendance-clock

# Work in small increments
git status
git diff
git add <specific-files>
git commit -m "ATT-315 Add attendance clock endpoints"

# Before PR
git fetch
git diff origin/main...HEAD
```

Commands are illustrative. Follow team policy for branch names, rebasing, signing and pushing.

## 10.6 Self-review before committing

- [ ] No unrelated changes.
- [ ] No debug code or temporary files.
- [ ] No secrets or local environment files.
- [ ] No accidental generated artifacts.
- [ ] No unnecessary package changes.
- [ ] Tests and build have been run.
- [ ] Diff is understandable.
- [ ] Commit message describes the intent and references work as required.

---

# 11. AI-assisted software engineering

AI tools can accelerate code navigation, explanation, planning, test generation and implementation. They do not own the engineering result. You remain accountable for every change you submit.

**First rule:** Use only AI tools and account configurations approved by the organization. Follow data classification, privacy, intellectual-property, retention and security policies. Never send source code, customer data, personal data, secrets, tokens, private documentation or production information to an unapproved model or external service.

## 11.1 Choose the appropriate interaction mode

| Mode | Best use | Example |
|---|---|---|
| Inline completion | Small local code suggestions | Boilerplate, repetitive mapping, syntax assistance. |
| Ask / Explain | Understanding code without modifying it | Explain a request pipeline or query. |
| Inline edit | Small bounded transformation | Refactor one method with preserved behavior. |
| Plan | Multi-file or architectural change | Propose implementation steps and affected files. |
| Agent | Bounded multi-file task with tool use | Implement an approved feature plan. |
| Specialized review workflow | Recurring quality checks | Review current diff for correctness or security concerns. |

Choose the smallest capable mode. Do not use a broad autonomous agent for a task that can be handled with a targeted explanation or edit.

## 11.2 A safe AI-assisted workflow

```text
1. Understand the ticket yourself
       ↓
2. Ask AI to inspect; prohibit edits initially
       ↓
3. Verify its findings in the repository
       ↓
4. Ask for an implementation plan
       ↓
5. Review plan, assumptions and affected files
       ↓
6. Approve a bounded implementation task
       ↓
7. Inspect every generated change
       ↓
8. Run build, tests, analyzers and security checks
       ↓
9. Debug failures and verify behavior independently
       ↓
10. Review the final diff and own the PR
```

## 11.3 Repository instructions

Once you understand the repository and have permission to add project guidance, maintain concise instructions that describe information the model cannot reliably infer from code.

Example `.github/copilot-instructions.md` (use the correct file and format for the approved AI tool):

```markdown
# Project engineering guidance

## Project structure
- Describe the important projects and ownership boundaries.
- Explain where API, application, domain and infrastructure code belongs.

## Architecture
- Follow established project conventions.
- Do not introduce a new architectural pattern without discussion.
- Preserve module boundaries and public contracts.

## C# and .NET
- Use the repository's supported SDK and language version.
- Follow existing naming, formatting and dependency-injection conventions.
- Use asynchronous APIs for I/O where appropriate.
- Propagate cancellation where the existing design supports it.

## Quality
- Add tests for changed behavior and relevant regressions.
- Cover error and boundary conditions.
- Do not weaken assertions or disable tests to obtain a passing build.

## Security
- Enforce authorization on the server.
- Validate untrusted input.
- Never log credentials, tokens or sensitive personal data.
- Do not bypass existing security mechanisms.

## Change boundaries
- Keep changes focused.
- Do not modify unrelated files.
- Do not introduce dependencies without justification.
- Do not change public contracts or database schemas without reporting the impact.

## Before completion
- Run the relevant build and tests.
- Inspect the final diff.
- Report commands actually executed and their results.
- List unresolved risks and assumptions.
```

Keep instructions short, specific and true. Update them when the repository changes. Do not copy generic rules into every project if the organization maintains shared standards elsewhere.

## 11.4 Example prompt: understand a new repository

```text
Act as a senior software engineer onboarding to this repository.
Do not modify files.

Investigate:
1. Solution and project structure.
2. Architectural style and project dependencies.
3. Application entry points and request flow.
4. Database and persistence approach.
5. Authentication and authorization.
6. Integrations and background processing.
7. Testing conventions and commands.
8. Build, run and deployment documentation.

Return:
- A high-level architecture summary.
- Important folders and files.
- One end-to-end request flow.
- Known facts with file references.
- Questions that require team clarification.

Do not infer undocumented business rules.
```

## 11.5 Example prompt: investigate a Jira story

```text
Investigate Jira item [KEY] in the context of this repository.
Do not modify files.

1. Identify relevant endpoints, services, domain logic and data access.
2. Trace the existing behavior end-to-end.
3. Find existing validation and authorization rules.
4. Find related tests and documentation.
5. Identify dependencies and compatibility constraints.
6. Compare the ticket's acceptance criteria with existing behavior.

Produce a proposed implementation plan with:
- Files/components likely to change.
- Purpose of each change.
- Risks and edge cases.
- Tests required.
- Missing requirements or decisions.

Separate repository facts from assumptions. Do not invent business rules.
```

## 11.6 Example prompt: implement an approved plan

```text
Implement the approved plan for [JIRA-KEY].

Constraints:
- Follow established architecture and repository conventions.
- Keep the change within the agreed scope.
- Preserve existing behavior outside the requirement.
- Reuse existing validation, authorization and error-handling mechanisms.
- Avoid unnecessary abstractions and dependencies.
- Add relevant unit and integration tests.
- Cover failure and boundary cases.

Do not modify public contracts, database schema or infrastructure
without stopping and reporting the impact first.

Before finishing:
1. Run the relevant build and tests.
2. Inspect the complete diff.
3. Report files changed and why.
4. Report exact commands executed and actual results.
5. Identify assumptions, risks and remaining work.
```

## 11.7 Example prompt: review the current diff

```text
Review the current Git diff. Do not modify files.

Prioritize:
1. Correctness and business behavior.
2. Security and authorization.
3. Data integrity, transactions and concurrency.
4. Error handling and resilience.
5. Performance.
6. API and backward compatibility.
7. Tests and maintainability.

For each finding provide:
- Severity (blocking / important / suggestion / question).
- File and line reference.
- Concrete problem.
- Likely consequence.
- Suggested correction.

Do not invent issues. Do not report subjective style preferences as defects.
If no issue is found in an area, say so without claiming exhaustive proof.
```

## 11.8 Prompt files and specialized agents

Use prompt files for manually invoked, repeatable workflows such as:

- Investigate a bug.
- Prepare an implementation plan.
- Generate test cases from acceptance criteria.
- Review a diff.
- Check API compatibility.
- Draft a PR description.
- Update documentation after a change.

Use specialized agents only when the tool supports them and the organization permits them. Define their scope, tool permissions, input data and output expectations. An agent should not silently approve its own work or perform production actions.

AI customization formats and supported features change. Check the current documentation for the tool and version actually installed. Do not assume Copilot, Claude Code, Codex and other agents load the same instruction files or interpret prompts identically.

## 11.9 AI failure modes to watch for

- Hallucinated APIs, file paths, config keys or framework behavior.
- Plausible code that does not compile.
- Tests that assert implementation details or fail to cover real behavior.
- Broad refactors outside the ticket scope.
- Removed validation or weakened security controls.
- Incorrect assumptions about timezones, concurrency or transactions.
- Fabricated test execution or success claims.
- Leaked secrets or confidential data.
- Dependency additions with licensing, security or support consequences.

Never accept an agent's claim that tests passed without checking the actual test output. Never merge generated code that you cannot explain and maintain.

---

# 12. Implementation quality and maintainable code

Good implementation is correct, understandable, appropriately designed, testable, secure and supportable.

## 12.1 Engineering quality dimensions

| Dimension | Questions |
|---|---|
| Correctness | Does it meet the requirement and preserve invariants? |
| Design | Are responsibilities and boundaries appropriate? |
| Maintainability | Can another engineer understand and change it? |
| Testability | Can behavior be verified at suitable boundaries? |
| Security | Are trust boundaries, authorization and input validation correct? |
| Performance | Are database, network, memory and CPU costs reasonable? |
| Reliability | What happens on timeout, retry, partial failure or duplicate input? |
| Observability | Can operators diagnose behavior and impact? |
| Compatibility | Are existing users, APIs, data and integrations preserved? |
| Deployability | Can the change be introduced and recovered safely? |

## 12.2 Design habits

- Keep methods and classes focused on coherent responsibilities.
- Preserve encapsulation and protect domain invariants.
- Prefer explicit contracts and clear names.
- Separate business rules from infrastructure concerns where the architecture requires it.
- Use dependency injection consistently with existing patterns.
- Avoid unnecessary abstractions, factories, repositories or layers.
- Avoid premature generalization.
- Make error handling intentional and consistent.
- Use cancellation and timeouts appropriately for I/O.
- Be deliberate about transaction boundaries.
- Consider concurrency and duplicate processing for distributed workflows.
- Make API and database changes backward-compatible where required.

SOLID, Clean Architecture, Onion Architecture, DDD and CQRS are tools for reasoning, not checklists to apply mechanically. Follow the system's context and use the simplest design that satisfies its quality requirements.

## 12.3 Common .NET review areas

- Correct use of `async` / `await` and cancellation.
- Avoid blocking asynchronous work with `.Result` or `.Wait()` in request paths.
- Reuse `HttpClient` through `IHttpClientFactory` or the approved client strategy.
- Use parameterized queries or safe ORM APIs.
- Validate untrusted input and enforce server-side authorization.
- Use structured logging; avoid sensitive values.
- Consider transaction and isolation behavior.
- Make retries bounded and safe; do not retry non-idempotent operations blindly.
- Dispose resources appropriately.
- Avoid exposing persistence entities directly as API contracts unless that is the established and intentional design.
- Avoid leaking internal exception details to callers.
- Ensure API error responses follow the team's contract.

## 12.4 API design checklist

- Is the endpoint/resource name clear?
- Are HTTP methods and status codes appropriate?
- Is the request/response contract explicit?
- Are validation failures predictable?
- Is authorization enforced server-side?
- Are pagination, filtering and sorting safe and bounded?
- Are idempotency and concurrency relevant?
- Are error responses consistent?
- Is versioning or backward compatibility required?
- Is the contract documented and tested?

## 12.5 Database and data integrity checklist

- Understand table size, access patterns and ownership.
- Inspect generated SQL for important queries.
- Check index selectivity, coverage and write overhead.
- Avoid loading unbounded result sets.
- Use pagination where appropriate.
- Understand transaction scope and isolation.
- Consider unique constraints and concurrency tokens.
- Define migration and backfill strategy.
- Do not log sensitive records or expose production data in lower environments.
- Make data retention and deletion requirements explicit.

## 12.6 Distributed systems concerns

For integrations, events and background work, consider:

- Timeouts and cancellation.
- Retries with bounded backoff and jitter where appropriate.
- Idempotency and deduplication.
- At-least-once delivery and duplicate messages.
- Ordering requirements.
- Dead-letter handling.
- Circuit breakers and bulkheads where justified.
- Transactional outbox/inbox patterns where appropriate.
- Correlation and trace propagation.
- Schema and contract compatibility.
- Partial failure and reconciliation.

Do not assume an asynchronous message is delivered exactly once or that a network timeout means the remote operation did not happen.

---

# 13. Testing and verification

Testing should provide evidence that required behavior works and important regressions have not been introduced.

## 13.1 Testing levels

| Test type | What it verifies | Typical example |
|---|---|---|
| Unit | Isolated logic and business rules | Attendance state transition validation |
| Integration | Multiple components and real infrastructure boundaries | ASP.NET Core endpoint with database behavior |
| Contract | Agreement between service/provider and consumer | OpenAPI or message contract compatibility |
| End-to-end | Important user workflows | Employee clocks in, then views attendance history |
| Performance/load | Behavior under representative workload | Concurrent attendance requests |
| Security | Security controls and abuse cases | Authorization boundary tests |
| Smoke/health | Essential behavior after deployment | Health endpoint and critical business request |
| Exploratory | Unexpected behavior and usability | Manually probe unusual date and shift cases |

Use the smallest suitable test level for a behavior. A healthy test suite is not simply the largest possible number of end-to-end tests.

## 13.2 Test scenario checklist

For a meaningful business operation, consider:

- Valid input and expected result.
- Invalid or malformed input.
- Missing entity or missing required data.
- Unauthorized and forbidden access.
- Boundary values and date/time transitions.
- Empty result.
- Duplicate request.
- Concurrent request.
- Dependency timeout or unavailable service.
- Partial failure.
- Retry and recovery behavior.
- Backward compatibility.
- Audit and observability behavior.

Not every case applies to every ticket. Choose scenarios according to risk.

## 13.3 Test quality

- Tests should fail when the relevant behavior is broken.
- Assert observable behavior, not private implementation details unnecessarily.
- Keep test data understandable and isolated.
- Avoid time-dependent or order-dependent tests.
- Use deterministic clocks or controlled time where date/time behavior is important.
- Do not mock every dependency by default; integration tests are necessary for important infrastructure interactions.
- Do not weaken assertions or skip tests to get a green pipeline.
- Treat flaky tests as engineering problems, not background noise.

## 13.4 ASP.NET Core testing

For .NET, understand the team's chosen framework (xUnit, NUnit or MSTest), test host patterns, test containers/infrastructure strategy and any test data conventions.

Integration tests can exercise the ASP.NET Core request pipeline and supporting infrastructure such as database, file system and network boundaries. Use them selectively for critical integration behavior; unit tests are generally more efficient for isolated logic.

## 13.5 Definition of verified

Before claiming a change works, know:

- Which commands actually ran.
- Which test projects and filters were used.
- Whether build warnings or analyzer failures remain.
- Which scenarios were tested manually.
- What was not tested and why.
- Whether the environment was representative.

Be precise in PR descriptions and status messages. "Build passed; unit tests passed; integration tests not run because the test database was unavailable" is more useful than "All good".

---

# 14. Code and API documentation

Documentation has different levels. Do not use code comments to replace architecture documentation, or Confluence pages to replace the authoritative API contract.

## 14.1 Where information belongs

| Location | What to document |
|---|---|
| XML documentation | Public C# API contracts and non-obvious semantics. |
| Inline code comment | Why a surprising or constrained implementation exists. |
| README | What the repository does and how to build/run/test it. |
| OpenAPI / API spec | HTTP endpoint contracts, schemas, errors and authentication. |
| ADR | Why a significant technical decision was made. |
| Technical design | How a multi-component feature is proposed to work. |
| Runbook | How to diagnose, operate and recover the service. |
| Jira | Work scope, acceptance criteria, status and links. |

## 14.2 XML documentation example

```csharp
/// <summary>
/// Retrieves attendance records for an employee within the specified range.
/// </summary>
/// <param name="employeeId">The employee identifier.</param>
/// <param name="from">Inclusive start of the requested range.</param>
/// <param name="to">Exclusive end of the requested range.</param>
/// <param name="cancellationToken">Token used to cancel the operation.</param>
/// <returns>The matching attendance records.</returns>
Task<IReadOnlyList<AttendanceRecord>> GetAttendanceAsync(
    EmployeeId employeeId,
    DateTimeOffset from,
    DateTimeOffset to,
    CancellationToken cancellationToken);
```

Document semantics that callers need to understand, such as inclusive/exclusive boundaries, ordering, nullability, authorization expectations or idempotency. Do not write comments that merely narrate the syntax.

Bad:

```csharp
// Increment the counter.
counter++;
```

Better when there is a real reason:

```csharp
// The upper bound is exclusive so records at the next period boundary
// are not included in this query.
```

## 14.3 README checklist

- What is this repository / service?
- What business capability does it provide?
- What SDKs and prerequisites are required?
- How do you restore, build, test and run it?
- How is local configuration supplied safely?
- What local dependencies are required?
- Where are the main projects and entry points?
- Where are API specs and architecture docs?
- How do contributors follow branch and PR conventions?
- Where are troubleshooting and support instructions?

Update docs when behavior, setup, commands, ownership or operational procedures change.

---

# 15. Git, branches, commits and pull requests

## 15.1 Branching

Follow the repository's existing branching model. Possible models include trunk-based development, short-lived feature branches, release branches or a configured GitFlow variant. Learn why the organization chose its model before recommending a change.

Branch names should be descriptive and follow team convention, for example:

- `feature/ATT-315-attendance-clock`
- `bugfix/ATT-402-overnight-duration`
- `hotfix/INC-123-payment-timeout`

## 15.2 Commit habits

- Keep commits focused and understandable.
- Explain intent rather than narrating trivial syntax.
- Reference Jira keys when required.
- Avoid committing secrets, local settings and generated noise.
- Do not rewrite shared history unless the team's workflow allows it.
- Do not create one huge commit for unrelated work.

Example:

`ATT-315 Add attendance clock-in validation`

## 15.3 Pull request template

```markdown
## Summary
What does this PR change?

## Context
Why is the change needed? Link Jira and design documents.

## Implementation
- Main code changes.
- Important design decisions.

## Testing
- Build command and result.
- Unit tests and result.
- Integration / E2E tests and result.
- Manual verification, if any.
- Tests not run and why.

## Database / configuration changes
Migrations, configuration, secrets or infrastructure changes.

## Security / compatibility considerations
Authorization, data sensitivity, API compatibility and risks.

## Deployment / rollback considerations
Ordering, feature flags, migration steps and recovery.

## Documentation
Pages, API specs and runbooks updated.

## Reviewer focus
Specific areas where careful review is useful.

## Related work
Jira / Confluence / PR / incident links.
```

## 15.4 Keep PRs focused

A PR should tell one coherent story. Split changes when that improves reviewability and can be done without creating unsafe intermediate states. Large or cross-cutting changes may need a design review and staged PRs.

Before requesting review:

- Check the full diff, not only the files you remember changing.
- Remove unrelated formatting and refactoring.
- Ensure CI is not known to be broken because of your change.
- Explain migrations and compatibility risks.
- Provide test evidence.
- Mark drafts clearly if work is incomplete.

---

# 16. Code review

Code review is a quality, risk-reduction and knowledge-sharing activity. It is not a contest or an opportunity to enforce personal taste.

## 16.1 Review sequence

1. Read the Jira requirement and acceptance criteria.
2. Read the PR title and description.
3. Understand the affected components and intended behavior.
4. Inspect the overall diff and file changes.
5. Check correctness and business invariants first.
6. Check security, authorization and data exposure.
7. Check data integrity, transactions and concurrency.
8. Check resilience, errors, observability and performance.
9. Inspect tests and compatibility.
10. Run locally when the risk or complexity warrants it.
11. Write concise, actionable comments.
12. Submit the review using the repository's approval rules.

## 16.2 Review dimensions

- Does the code meet the requirement?
- Does it preserve existing behavior outside scope?
- Are responsibilities and boundaries appropriate?
- Are error paths and validation correct?
- Is authorization enforced at the appropriate boundary?
- Are concurrency, retries and transactions safe?
- Are queries and network calls reasonable?
- Are logs useful and free from sensitive values?
- Are tests meaningful and sufficient for the risk?
- Are public contracts and database changes compatible?
- Are documentation and operations affected?

## 16.3 Classify findings

Use the team's labels if they exist. A practical generic distinction is:

| Category | Meaning | Expected action |
|---|---|---|
| Blocking | Security, correctness, data integrity or severe reliability defect | Must be resolved or formally handled before merge. |
| Important | Material maintainability, performance or operational concern | Discuss and normally resolve before merge. |
| Suggestion | Non-blocking improvement | Author considers it; should not block by default. |
| Question | Reviewer needs context or explanation | Author clarifies; may reveal a real issue. |
| Nitpick | Minor preference or cosmetic observation | Avoid blocking; follow style tooling where possible. |

## 16.4 Good review comment structure

**Finding → impact → question or suggested outcome.**

Blocking example:

> **Blocking — Authorization:** This endpoint accepts an arbitrary employee ID but I cannot see a check that the current manager is authorized to view that employee's attendance. This may expose attendance data across organizational boundaries. Could we enforce the existing employee-access policy before returning the records and add an integration test for cross-organization access?

Suggestion example:

> **Suggestion:** Could we reuse the existing date-range validation? Similar validation appears in the reporting endpoint. This is not blocking the current behavior, but reuse may reduce duplicated rules.

Question example:

> Could you explain why this operation remains synchronous? I'm trying to understand how the request behaves if the external payroll service is slow or unavailable.

Avoid comments such as "bad code", "wrong design" or "just use a repository" without evidence and context.

## 16.5 Receiving feedback

When you agree:

> Good point. I missed the authorization boundary in this case. I'll update the implementation and add an integration test for access to another organizational unit.

When you disagree:

> I understand the concern. I chose this approach because the operation requires an immediate response and the dependency has a defined latency expectation. An asynchronous design would change the API behavior. Could we compare the trade-offs before deciding whether to change the design?

When a comment is unclear:

> Could you clarify the scenario you're concerned about? I want to make sure I'm addressing the underlying behavior rather than changing the implementation unnecessarily.

## 16.6 AI-assisted code review

AI can provide a supplementary pass over a diff, but it is not an approval authority. Review its findings, verify them in context and do not treat an absence of AI findings as proof of correctness or security.

---

# 17. Professional communication

The quality of your communication affects delivery, trust and decision-making. Keep messages clear, factual, respectful and appropriate to the channel.

## 17.1 A useful message structure

For important updates, use:

1. **Context:** What are we discussing?
2. **Observation:** What has happened or been discovered?
3. **Impact:** Why does it matter?
4. **Next step / ask:** What action or decision is needed?

Do not force every short message into a template. Use enough context for the recipient to act.

## 17.2 Daily stand-up update

```text
Yesterday:
Completed the attendance API filtering implementation
and added the main unit tests.

Today:
Working on integration tests and verifying authorization behavior.

Blockers:
The integration test environment is unavailable. I contacted
its owner and will continue with the local test cases meanwhile.
```

Keep it brief. Take detailed technical discussions offline with the relevant people.

## 17.3 Async progress update

```text
Status: In progress

Completed:
- Implemented the API query and validation.
- Added unit tests for the main cases.

Current focus:
- Integration tests for authorization and date boundaries.

Risk / blocker:
- Waiting for the shared integration environment.

Next step:
- Complete environment verification, then open the PR.

Decision needed:
- Confirm whether the date range is based on shift date or timestamp.
```

## 17.4 Asking for help

Weak:

> The API doesn't work. Can someone help?

Better:

> I'm investigating the attendance API's date filtering behavior. The implementation stores UTC timestamps, but I haven't found an authoritative rule for how local shift dates should be interpreted. I checked the API and database behavior but could not find the business decision. Does anyone know where this is documented or who owns the rule?

Show what you investigated and ask a focused question.

## 17.5 Reporting a blocker

```text
I'm blocked on [specific activity] because [verified reason].
The impact is [scope / expected delay / affected acceptance criterion].
I have already tried [reasonable steps].
I need [specific decision, access or action] from [owner/team].
Meanwhile I can continue with [alternative work], if appropriate.
```

Raise the blocker early. Do not wait until the sprint or release is nearly over.

## 17.6 Disagreeing constructively

> I see the benefit of adding a new service. My concern is that it adds another deployment and support boundary for a relatively small capability. Could we compare it with keeping the logic in the existing application? I may be missing a scaling or ownership requirement, so I'd like to understand that before recommending a direction.

## 17.7 Reporting a mistake

> I introduced a regression in the filtering logic. I've identified the cause and am preparing a correction with a regression test. I'll also check the related endpoint to see whether the same assumption exists there.

Acknowledge the mistake, state impact, show the response and follow through.

## 17.8 Communicating risk

Separate confirmed facts from hypotheses:

> I found a potential duplicate-processing risk in the event consumer. I have not confirmed that duplicate processing has occurred in production, but the current retry path appears capable of delivering the same event more than once. I recommend verifying the consumer's idempotency behavior before expanding this integration.

Do not present an unverified suspicion as a confirmed production incident.

## 17.9 Meeting behavior

- Read the agenda and relevant material beforehand.
- Know what outcome the meeting needs: information, decision, design or action.
- Listen and ask focused questions.
- Distinguish facts, opinions and assumptions.
- Invite relevant disciplines when a decision affects them.
- Summarize options and trade-offs if discussion becomes circular.
- Record decisions, owners, actions and open questions.
- Follow up on actions you accepted.

## 17.10 Weekly manager update

```text
Completed:
- Outcomes delivered, with links where useful.

Current focus:
- Main work and expected next milestone.

Risks / blockers:
- Evidence, impact, mitigation and owner.

Next week:
- Planned focus, dependencies and decisions needed.

Support / feedback:
- Where guidance or a decision would help.
```

## 17.11 Communication channel etiquette

- Use the team's designated channel for shared information.
- Use a direct message for a genuinely individual matter, not to hide a decision that others need to know.
- Keep Jira comments connected to ticket scope and status.
- Keep Confluence pages for durable knowledge.
- Use PR discussions for code-specific review and resolution.
- Do not create unnecessary parallel conversations across email, chat and tickets.
- Avoid sarcasm, blame, vague urgency and all-caps escalation.
- Respect time zones and meeting-free focus periods where practical.

---

# 18. Releases, deployments and database changes

Merging code is not necessarily the same as releasing a feature. Learn the organization's release model, deployment permissions, approval gates and recovery procedures before participating in production delivery.

## 18.1 Key terms

- **Build:** Compile and package source into an artifact.
- **CI:** Automatically validate changes through builds and checks.
- **Artifact:** Versioned package that can be promoted through environments.
- **Deploy:** Install or distribute a specific artifact/configuration into an environment.
- **Release:** Make a change available to its intended users or consumers.
- **Feature flag:** Control exposure of behavior independently from deployment, when supported.
- **Rollback:** Return to a previous known-good version or configuration.
- **Roll-forward:** Apply a corrective change to restore service or behavior.
- **Smoke test:** Small set of checks confirming critical behavior after deployment.

A deployment can occur while a feature remains disabled behind a feature flag.

## 18.2 Release lifecycle

```text
Changes merged
    ↓
CI build and automated tests
    ↓
Static analysis / security / quality gates
    ↓
Versioned artifact produced
    ↓
Deploy to development / test
    ↓
Integration and acceptance validation
    ↓
Release approval (if required)
    ↓
Production deployment / progressive exposure
    ↓
Health checks and business smoke tests
    ↓
Monitor and confirm
    ↓
Communicate release status and close work
```

Use the company's actual environment names and deployment process.

## 18.3 Before release checklist

- [ ] Scope and artifact version are known.
- [ ] Required PR approvals and CI checks are complete.
- [ ] Test results and unresolved defects are understood.
- [ ] Dependencies and configuration are checked.
- [ ] Secrets are provided through approved secret management.
- [ ] Database migrations are reviewed and ordered correctly.
- [ ] Compatibility with currently running versions is understood.
- [ ] Feature flags and rollout configuration are understood.
- [ ] Monitoring and health checks are ready.
- [ ] Rollback or roll-forward strategy is documented.
- [ ] Release owner and required approvals are identified.
- [ ] Stakeholders know the release window and potential impact.

## 18.4 During deployment

- Confirm the correct artifact and environment.
- Observe pipeline output and deployment events.
- Check startup, readiness and health probes.
- Run agreed smoke tests.
- Watch error rates, latency, saturation and business signals.
- Stop progressive rollout if health criteria fail.
- Keep release communications factual.

## 18.5 After deployment

- Verify important user/business workflows.
- Check logs, metrics, traces and alerts.
- Confirm the expected version is running.
- Record release status and known limitations.
- Update Jira and documentation.
- Capture follow-up actions.

## 18.6 Deployment patterns to understand

- Rolling deployment.
- Blue-green deployment.
- Canary / progressive deployment.
- Feature flags.
- Expand-and-contract database migration.
- Rollback versus roll-forward.

These patterns reduce or control certain risks but do not remove the need for health checks, compatibility planning and recovery procedures.

## 18.7 Database migration safety

Example expand-and-contract strategy for renaming a field used by multiple services:

1. Add the new schema element without removing the old one.
2. Deploy code that can work with both forms where required.
3. Backfill data safely and observe progress.
4. Switch reads and writes to the new form.
5. Verify that no old consumers remain.
6. Remove the old schema element in a later change.

Consider migration locks, data volume, long-running transactions, replication, rollback feasibility and application-version compatibility. A database rollback is not always equivalent to reverting application code.

## 18.8 Production release status message

```text
Release: [version / identifier]
Environment: [environment]
Status: In progress / Completed / Halted

Changes:
- [high-level change and Jira links]

Verification:
- Build / deployment status.
- Health checks and smoke tests.
- Key metrics reviewed.

Known issues / follow-up:
- [facts only]

Owner / next update:
- [person or team / time if agreed]
```

---

# 19. Production operations and incident response

A senior engineer should understand how software behaves after release and how the organization detects, responds to and learns from failures.

## 19.1 Three major observability signals

| Signal | Question answered | Examples |
|---|---|---|
| Logs | What happened? | Structured events, errors, correlation IDs. |
| Metrics | How much / how often / how long? | Request rate, error rate, latency, queue depth, CPU/memory. |
| Traces | Where did time or failure occur across components? | A distributed request across API, database and external service. |

Understand the organization's telemetry stack and how correlation/trace context flows across services. For .NET, learn the team's use of `ILogger`, `System.Diagnostics.Metrics`, `Activity` and OpenTelemetry where applicable.

Do not log passwords, access tokens, secrets, payment details or unnecessary personal data.

## 19.2 Production readiness questions

- Who owns the service and who is on call?
- What are its key dependencies?
- What are the service's SLOs or operational expectations?
- What dashboards and alerts should be checked?
- Are alerts actionable and routed to the right people?
- Is there a runbook?
- How are backups and recovery tested?
- What changes require approval?
- How are incidents declared and communicated?
- What is the safe rollback or mitigation process?

## 19.3 Incident response sequence

1. **Acknowledge and assess:** determine symptoms, severity and affected users/workflows.
2. **Establish coordination:** identify incident lead, technical responders and communication channel.
3. **Gather evidence:** inspect alerts, logs, metrics, traces and recent changes.
4. **Contain and mitigate:** reduce user impact safely; do not make uncontrolled changes.
5. **Communicate:** share verified facts, known impact, mitigation and next update.
6. **Restore:** roll back, roll forward or apply an approved mitigation.
7. **Verify:** confirm technical health and business behavior.
8. **Document:** record timeline, impact, decisions and evidence.
9. **Learn:** hold a blameless review and create prioritized corrective actions.

Follow the company's severity model and incident command process. Do not independently change production systems unless your authorization and incident role permit it.

## 19.4 Incident communication template

```text
Incident ID:
Service / environment:
Severity:
Start time / detection time:

Current status:
Investigating / Mitigating / Monitoring / Resolved

Known impact:
Affected users, workflows, regions or data (confirmed only).

What we know:
Evidence and recent relevant changes.

Actions in progress:
Owner — action — status.

Risks / decisions needed:

Next update:
Time or agreed cadence.
```

## 19.5 Blameless post-incident review template

```markdown
# Incident Review — [ID / summary]

## Summary
What happened, duration and impact.

## Detection
How it was detected and how long detection took.

## Timeline
Time-stamped events, decisions and actions.

## Technical explanation
Contributing system behaviors and conditions.

## Response
What helped, what slowed recovery and why.

## Customer / business impact
Known and verified impact.

## What went well

## What could be improved
Focus on systems, processes, tools and information—not personal blame.

## Corrective actions
- Action — owner — priority — target date.

## Links
Dashboards, logs, tickets, PRs, runbooks and related incidents.
```

The goal is organizational learning and reduced recurrence or impact, not finding someone to blame.

---

# 20. Security, privacy and responsible engineering

Security is part of ordinary engineering work. Follow company security policies and involve security specialists when required.

## 20.1 Everyday secure-development habits

- Treat all external input as untrusted.
- Enforce authorization on the server, not only in the UI.
- Apply least privilege to users, services and automation.
- Validate data at trust boundaries.
- Use parameterized queries and safe framework APIs.
- Protect secrets with approved secret-management systems.
- Avoid logging credentials, tokens and sensitive personal data.
- Use approved dependency sources and track vulnerabilities.
- Review file upload, deserialization, redirect and command execution paths carefully.
- Use secure defaults and explicit configuration.
- Consider tenant isolation and data ownership in multi-tenant systems.
- Review audit requirements for sensitive actions.
- Report suspected exposure through the approved security process.

## 20.2 AI and data handling

Before using an AI tool, establish:

- Is this tool approved by the organization?
- Is the account managed by the organization?
- What code/data classification can be sent to it?
- Are prompts or outputs retained or used for model improvement under the contract?
- Can the tool access files, terminals, network or external tools?
- Are tool permissions scoped to the task?
- Is human approval required for file edits, commands or external actions?

Do not assume a product's consumer privacy settings apply to a company account or enterprise deployment. Ask the organization's security/privacy owner.

## 20.3 Threat-aware implementation questions

- Who can call this endpoint?
- Can one tenant or user access another tenant's data?
- Can a caller manipulate object identifiers?
- Can untrusted data reach a query, shell, template or deserializer?
- Are secrets or personal data exposed in logs or error messages?
- Can a request cause unbounded resource use?
- Can retries duplicate a payment, event or state transition?
- Are dependency and package sources trusted?

Use the current OWASP guidance and the organization's secure development lifecycle. Do not treat any checklist as proof that an application is secure.

---

# 21. Senior-level ownership and technical leadership

Your influence should grow with your understanding of the system and the organization's trust in your judgment.

## 21.1 Decision scope

| Decision | Typical approach |
|---|---|
| Local implementation detail | Decide independently within team standards. |
| Feature-level design | Discuss with relevant team members and technical owner. |
| Cross-service API contract | Coordinate with affected service owners and consumers. |
| Database / architecture change | Review impact with system owners and architects as required. |
| Security / compliance change | Follow formal governance and involve specialists. |
| Organization-wide standard | Seek broad alignment and formal approval. |
| Production change | Follow release permissions and operational procedures. |

This is a guide, not a universal responsibility matrix. Confirm actual decision rights.

## 21.2 Present technical proposals effectively

Use this structure:

```text
Problem:
What is happening and why does it matter?

Evidence:
What code, data, incident, metric or user report supports it?

Constraints:
What business, technical, security or operational conditions apply?

Options:
What realistic choices exist?

Trade-offs:
What are the costs, benefits and risks of each?

Recommendation:
What do you recommend and why?

Reversibility:
Can the decision be changed later? At what cost?

Decision owner / next step:
Who decides and what must happen next?
```

## 21.3 Mentoring and knowledge sharing

- Explain reasoning, not only the final answer.
- Help teammates debug without immediately taking over their keyboard.
- Share system context and useful documentation.
- Give specific, respectful review feedback.
- Invite questions and acknowledge uncertainty.
- Avoid creating a single-person knowledge bottleneck.
- Pair on complex or high-risk changes where it improves understanding.

## 21.4 Improving the engineering system

Capture recurring friction:

- Slow or unreliable builds.
- Difficult local setup.
- Unclear ownership.
- Missing tests.
- Fragile deployments.
- Poor diagnostics.
- Repeated requirement ambiguity.
- Long or unfocused PRs.
- Manual repetitive release work.

For each improvement, record its impact, evidence, options, approximate cost and priority. Do not create an improvement initiative for every minor inconvenience.

## 21.5 Delivery and quality metrics

Use a balanced view. Depending on the team's model, useful delivery and operational signals may include:

- Lead time / change lead time.
- Deployment frequency.
- Change failure rate.
- Failed deployment recovery time.
- Deployment rework rate.
- Cycle time and throughput.
- Escaped defects and production incidents.
- Reliability / SLO attainment.
- Work-in-progress and aging work.
- Customer/business outcome measures.

DORA's current model describes five software delivery performance metrics: change lead time, deployment frequency, failed deployment recovery time, change fail rate and deployment rework rate. Metrics are intended to help understand system performance and improvement, not rank individual engineers. Combine speed and stability measures; never optimize a single number at the expense of quality or customer value.

---

# 22. 30/60/90-day plan

This is a suggested progression. Adjust it for the size of the organization, system complexity, access constraints, role expectations and the team's delivery cycle.

## Days 1–5: Orientation

**Focus:** people, expectations, access and communication.

- Meet manager, tech lead and key collaborators.
- Understand responsibilities and decision ownership.
- Join relevant channels and recurring meetings.
- Learn Jira and Confluence structure.
- Understand security and AI-tool policies.
- Identify the first system to learn.
- Confirm first-month success criteria.

**Evidence of progress:** You know who to contact, what is expected and where authoritative information lives.

## Week 1–2: Business and toolchain understanding

**Focus:** product, workflows, Jira, Confluence and local development.

- Learn key users, domain terms and business workflows.
- Trace one important operation through the system.
- Read existing architecture and runbooks.
- Understand Jira issue types and statuses.
- Learn how refinement and estimation work.
- Build, run and test the repository locally.
- Learn Git and PR conventions.

**Evidence of progress:** You can explain one business flow and can work independently in the development environment.

## Week 2–3: Technical discovery and engineering culture

**Focus:** architecture, testing, delivery and operational awareness.

- Map major components and dependencies.
- Understand APIs, databases, messaging and security.
- Inspect CI/CD and test environments.
- Find dashboards and understand service ownership.
- Review sample PRs and completed Jira tickets.
- Learn documentation and release expectations.

**Evidence of progress:** You can trace a change from code to test and deployment, and know where to find operational evidence.

## Days 15–30: First safe contribution

**Focus:** deliver a bounded, low-to-medium-risk change.

- Take a well-understood Jira item.
- Clarify acceptance criteria and risks.
- Investigate before editing.
- Write or update tests.
- Submit a focused PR.
- Respond professionally to feedback.
- Verify the change in the appropriate environment.
- Update documentation and communicate completion.

**Evidence of progress:** You deliver a validated change through the team's normal process.

## Days 31–60: Independent feature ownership

**Focus:** design, estimation, coordination and end-to-end delivery.

- Own a feature or bounded service area.
- Participate actively in refinement and estimation.
- Write clear Jira items when work needs to be split.
- Prepare design notes or ADRs where justified.
- Review other engineers' PRs.
- Coordinate with QA, product and platform teams.
- Understand deployment and rollback implications.
- Help investigate operational issues under the team's process.

**Evidence of progress:** You can plan and deliver a feature with appropriate consultation and visible risk management.

## Days 61–90: Trusted technical contributor

**Focus:** technical influence and system improvement.

- Own a meaningful system or capability area.
- Identify and prioritize a systemic improvement.
- Facilitate a technical discussion or design review.
- Improve documentation or operational readiness.
- Mentor or unblock another engineer.
- Contribute to reliability, delivery or quality improvements.
- Review outcomes with your manager and agree on next responsibilities.

**Evidence of progress:** Your work reduces uncertainty and improves the team's ability to deliver and operate software.

---

# 23. Daily, weekly and per-ticket routines

## 23.1 Daily routine

**Start of day:**
- Check team priorities, Jira and relevant messages.
- Review blockers and dependencies.
- Identify your main outcome for the day.
- Reserve focus time for implementation or analysis.

**During work:**
- Keep Jira status accurate.
- Work in small increments.
- Run relevant tests before handing work over.
- Ask for clarification when a material assumption is unresolved.
- Communicate blockers early.
- Avoid unnecessary context switching.

**End of day:**
- Record progress and remaining work.
- Update ticket comments/status if needed.
- Leave a clear note for handover if work is in progress.
- Identify the next action.

## 23.2 Weekly routine

- Review upcoming backlog items and dependencies.
- Prepare for refinement and planning.
- Check aging work and blockers.
- Review outstanding PRs.
- Share a concise status update with your manager/team where expected.
- Keep technical documentation current.
- Review operational issues or recurring quality problems.
- Reflect on an estimation or delivery assumption that could be improved.

## 23.3 Per-ticket routine

### Before coding
- [ ] Read and understand the requirement.
- [ ] Confirm acceptance criteria.
- [ ] Inspect existing implementation and conventions.
- [ ] Identify dependencies and risks.
- [ ] Clarify business decisions.
- [ ] Agree on an approach for material changes.

### During coding
- [ ] Keep changes focused.
- [ ] Follow established design and coding standards.
- [ ] Add tests as behavior is introduced.
- [ ] Consider authorization, errors, concurrency and observability.
- [ ] Communicate blockers or scope changes.

### Before PR
- [ ] Build and relevant tests pass.
- [ ] Review the complete diff.
- [ ] Remove unrelated or temporary changes.
- [ ] Check secrets and sensitive data.
- [ ] Update relevant docs.
- [ ] Write a clear PR description.

### After PR / delivery
- [ ] Address review feedback.
- [ ] Verify CI results.
- [ ] Follow deployment and release steps.
- [ ] Verify behavior after deployment where applicable.
- [ ] Update Jira and Confluence.
- [ ] Communicate completion and any known limitations.

---

# 24. Practical training plan and exercises

Use one continuous fictional enterprise case study: a workforce-management platform with employee attendance, manager approvals, payroll integrations, APIs, background workers, SQL Server and cloud deployment. The same requirements flow through Jira, Confluence, VS Code, tests, PR review and release.

## Module 1 — First week in the organization

**Learn:** manager conversations, stakeholder mapping, decision ownership, onboarding behavior.

**Exercise:** You join a team with a tech lead, architect, Product Owner and three service owners. Prepare the questions you would ask and create a stakeholder map.

**Deliverable:** First-week onboarding notes and manager expectations.

## Module 2 — Business and requirements discovery

**Learn:** domain discovery, business workflows, rules, functional and non-functional requirements.

**Exercise:** The Product Owner asks for employee attendance history but has not defined overnight-shift behavior. Identify blocking questions and write provisional acceptance criteria without inventing rules.

**Deliverable:** Refined requirement and open-question list.

## Module 3 — Jira mastery

**Learn:** Epic, Story, Task, Bug, Spike, acceptance criteria, DoR and DoD.

**Exercise:** Write a Story for manager attendance history, a Bug for incorrect overnight duration, a Task for correlation logging and a Spike for payroll idempotency.

**Deliverable:** Four structured Jira items.

## Module 4 — Confluence mastery

**Learn:** technical design, ADR, meeting notes, runbooks and page ownership.

**Exercise:** Document two possible payroll integration approaches and record the selected decision in an ADR.

**Deliverable:** Technical design and ADR.

## Module 5 — Architecture discovery

**Learn:** C4 diagrams, service boundaries, API and event flow, data ownership, failure modes.

**Exercise:** Trace clock-in from browser to API to SQL Server and identify where authorization, validation and observability belong.

**Deliverable:** Architecture summary and sequence diagram.

## Module 6 — VS Code workflow

**Learn:** repository setup, navigation, debugging, Git, tests and terminal.

**Exercise:** Clone a sample repository, run it, reproduce a bug, debug the call path and add a regression test.

**Deliverable:** Working local setup and verified fix.

## Module 7 — AI-assisted engineering

**Learn:** approved tooling, repo instructions, prompt files, planning, bounded agent work and verification.

**Exercise:** Ask an approved agent to inspect a Jira ticket without edits; verify its findings; review a plan; implement a small bounded change; inspect the diff and test results.

**Deliverable:** Repository-specific AI instructions and a verified PR.

## Module 8 — Implementation and quality

**Learn:** design principles, testing, security, data integrity, performance and refactoring.

**Exercise:** Implement clock-in validation with duplicate-request and concurrency scenarios.

**Deliverable:** Focused code and meaningful unit/integration tests.

## Module 9 — Code documentation

**Learn:** XML docs, README, OpenAPI, architecture notes, ADRs and runbooks.

**Exercise:** Document a public API contract, date-boundary semantics and an operational failure procedure.

**Deliverable:** Updated code/API docs and a runbook section.

## Module 10 — PR mastery

**Learn:** focused PRs, self-review, review severity, constructive feedback and disagreement.

**Exercise:** Review a deliberately flawed PR containing a missing authorization check, weak tests, unsafe retry behavior and unrelated refactoring.

**Deliverable:** Actionable review comments with severity and impact.

## Module 11 — Estimation and forecasting

**Learn:** reference stories, Planning Poker, decomposition, effort ranges, PERT, dependencies, capacity and flow metrics.

**Exercise:** Estimate the attendance capability, identify missing business decisions, break down work and communicate effort/confidence/assumptions.

**Deliverable:** Estimation worksheet and professional manager update.

## Module 12 — Release and operations

**Learn:** CI/CD, artifacts, staged deployment, migration safety, rollback, observability and incident response.

**Exercise:** Prepare a release checklist, identify a database migration risk, respond to a failed health check and write a blameless incident review.

**Deliverable:** Release plan, recovery steps and post-incident actions.

## Evaluation criteria for every exercise

A strong senior-engineer answer should demonstrate:

- Correct understanding of the business outcome.
- Clear distinction between facts, assumptions and unknowns.
- Awareness of system boundaries and affected teams.
- Appropriate security, data-integrity and reliability thinking.
- Proportionate scope and implementation strategy.
- Realistic estimation and risk communication.
- Professional, constructive communication.
- Verification and ownership through delivery.

---

# 25. Glossary

| Term | Meaning |
|---|---|
| Acceptance criteria | Observable conditions that a work item must satisfy. |
| ADR | Architecture Decision Record; captures a significant decision and its rationale. |
| Artifact | Versioned build output that can be promoted through environments. |
| Backlog refinement | Ongoing activity to clarify, split, order and estimate upcoming work. |
| Canary deployment | Gradually expose a change to a small portion of users or instances before wider rollout. |
| CI/CD | Continuous Integration / Continuous Delivery or Deployment. |
| Cycle time | Time from a defined work-start point to completion. |
| Definition of Done | Shared quality/completion criteria for work. |
| Definition of Ready | Team-defined criteria for work to be sufficiently clear to start. |
| Epic | Large body of related work, depending on Jira configuration. |
| Feature flag | Configuration that controls whether deployed behavior is enabled. |
| Idempotency | Repeating an operation with the same logical request does not create unintended additional effects. |
| Initiative | Higher-level grouping of strategic work, if configured. |
| Integration test | Test of multiple components and their interactions, often including infrastructure. |
| Lead time | Time from a defined request/commitment point to delivery. |
| Observability | Ability to understand system behavior using telemetry and other evidence. |
| PERT | Estimation technique using optimistic, most-likely and pessimistic estimates. |
| Planning Poker | Collaborative relative estimation using private simultaneous votes and discussion. |
| PR / Pull Request | Proposed source-code change submitted for review and integration. |
| Progressive delivery | Gradually expose a release and monitor health between stages. |
| Runbook | Operational instructions for diagnosis, procedures and recovery. |
| SLO | Service Level Objective; a target for a measured service-quality indicator. |
| Spike | Time-boxed investigation that reduces uncertainty. |
| Story point | Team-specific relative sizing unit, not elapsed time. |
| Throughput | Number of items completed during a defined period. |
| Trace | Correlated record of a request's path across components. |
| Velocity | Amount of estimated work completed by a team in a sprint; useful only in its local context. |
| Work in progress (WIP) | Work started but not yet completed. |

---

# 26. Reference material

Use these sources to deepen understanding. Product documentation and UI details change; check the documentation for the exact Jira, Confluence, VS Code and Git platform versions used by your organization.

## Agile, Scrum and estimation

- [The Scrum Guide — official current version](https://scrumguides.org/download.html)
- [Atlassian: Story points and estimation](https://www.atlassian.com/agile/project-management/estimation)
- [Atlassian: Fibonacci story points](https://www.atlassian.com/agile/project-management/fibonacci-story-points)
- [Atlassian Jira: Estimate in story points](https://confluence.atlassian.com/jirasoftware/estimate-in-story-points-1688898329.html)
- [Atlassian Jira: Create a work item and a subtask](https://support.atlassian.com/jira-software-cloud/docs/create-a-work-item-and-a-subtask/)

## Jira and Confluence

- [Atlassian: Create and edit Confluence content](https://support.atlassian.com/confluence-cloud/docs/create-and-edit-content/)
- [Atlassian: Create a page from a template](https://support.atlassian.com/confluence-cloud/docs/create-a-page-from-a-template/)

## VS Code and AI-assisted development

- [VS Code: Best practices for using AI](https://code.visualstudio.com/docs/agents/best-practices)
- [VS Code: Configure AI for your codebase](https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide)
- [VS Code: Prompt files](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- [VS Code: C# debugging configuration](https://code.visualstudio.com/docs/csharp/debugger-settings)

## Pull requests and code review

- [GitHub Docs: Reviewing pull requests quickstart](https://docs.github.com/en/pull-requests/get-started/reviewing-pull-requests-quickstart)
- [GitHub Docs: Helping others review your changes](https://docs.github.com/en/pull-requests/concepts/helping-others-review-your-changes)
- [GitHub Docs: Giving reviews](https://docs.github.com/en/pull-requests/concepts/giving-reviews)

## .NET, testing and documentation

- [Microsoft Learn: Integration tests in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/testing/integration-testing)
- [Microsoft Learn: Recommended XML documentation tags](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags)
- [Microsoft Learn: C# coding conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [OpenTelemetry: .NET documentation](https://opentelemetry.io/docs/languages/dotnet/)
- [OpenTelemetry: .NET logs](https://opentelemetry.io/docs/languages/dotnet/logs/)

## Security, operations and delivery

- [OWASP Top 10](https://owasp.org/projects/top-ten/) — consult the current release and your organization's secure development requirements.
- [Microsoft Azure Well-Architected: Operational Excellence checklist](https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/checklist)
- [Microsoft Azure Well-Architected: Safe deployment practices](https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/safe-deployments)
- [Microsoft Azure Well-Architected: Incident response](https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/incident-response)
- [Google SRE: Incident Management Guide](https://sre.google/resources/practices-and-processes/incident-management-guide/)
- [DORA: History of software delivery metrics](https://dora.dev/insights/dora-metrics-history/)
- [DORA FAQ](https://dora.dev/faq/)

---

## Final reminder

Your first responsibility in a new organization is to understand its business, people, systems and constraints. Then deliver small, verified changes, communicate clearly, and gradually take ownership of larger outcomes.

**Understand the system. Make uncertainty visible. Deliver safely. Learn continuously. Own the outcome.**
