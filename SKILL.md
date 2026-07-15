---
name: projectforge
description: Use when Codex must plan, design, implement, refactor, or verify an application feature or repository change from an idea, requirement, issue, or existing codebase.
---

# ProjectForge

## Overview

Guide Codex from an application idea, issue, or repository task to a verified code change. Inspect the existing codebase, clarify expected behaviour, choose the smallest suitable design, implement with tests, and report evidence.

**Core principle:** Codex must understand the repository and verify behaviour before claiming a change is complete.

## When to Use

Use this skill when Codex is asked to:

- Create or extend a web, mobile, desktop, SaaS, API, CLI, or internal application
- Convert an idea, issue, PRD, or bug report into an implementation plan
- Analyze an existing repository before changing it
- Design a feature, module, API, database change, or system boundary
- Implement a multi-file feature or refactor
- Establish architecture, clean-code, folder, and filename conventions
- Add tests, review code quality, or verify a completed change
- Prepare a repository for deployment or maintenance

For a tiny, fully specified edit, use the repository's normal workflow directly. Still inspect the relevant files and run focused verification.

## Codex Repository Workflow

Follow this sequence whenever a repository is available.

### 1. Inspect Before Editing

- Read repository instructions such as `AGENTS.md`, `README.md`, contribution guides, and package scripts.
- Inspect the relevant directory tree, source files, tests, configuration, and dependency manifests.
- Search for similar features and existing conventions before introducing a new pattern.
- Check the current Git status and avoid overwriting unrelated user changes.
- Identify the smallest set of files that should change.

**Rule:** Do not invent the stack, folder structure, commands, or coding style when the repository already defines them.

### 2. Resolve the Task

Write down or infer:

- Current behaviour
- Desired behaviour
- Acceptance criteria
- Constraints and compatibility requirements
- Edge cases and failure states
- Files, modules, and interfaces likely to be affected

For ambiguous details, make conservative, clearly stated assumptions rather than expanding scope unnecessarily.

### 3. Plan the Change

For multi-step work, create a concise implementation plan that includes:

1. Behaviour or tests to add
2. Production files to change
3. Data, API, or migration impact
4. Security and backward-compatibility risks
5. Verification commands

Keep the plan proportional to the task. Do not produce a large planning document for a one-line change.

### 4. Implement Test-First

- Add or update a focused test that demonstrates the required behaviour.
- Run it and confirm it fails for the expected reason.
- Write the minimum implementation required to pass.
- Refactor only after the behaviour passes.
- Preserve public interfaces unless the requirement explicitly changes them.
- Follow existing repository naming, error handling, dependency, and architectural conventions.

When tests are impractical, explain why and use the strongest available verification such as type checking, build checks, static analysis, or a reproducible manual check.

### 5. Review the Diff

Before completion:

- Inspect the final Git diff.
- Remove accidental edits, debug output, temporary files, dead code, and unrelated formatting changes.
- Check imports, filenames, public exports, migrations, configuration, and documentation.
- Review security-sensitive boundaries: input validation, authorization, secrets, file access, commands, and external requests.

### 6. Verify With Evidence

Run the narrowest relevant checks first, then broader checks when justified:

1. Focused unit or feature tests
2. Type checking or compilation
3. Linting and formatting checks
4. Integration or end-to-end tests
5. Production build

Never claim that tests pass, a bug is fixed, or the application builds without seeing successful command output.

### 7. Report Completion

State:

- What changed
- Important design decisions
- Files or modules affected
- Verification commands and results
- Any remaining limitation, risk, or follow-up

Do not expose internal chain-of-thought. Provide concise rationale and observable evidence.

## Required Inputs

Collect or infer as much as possible:

1. Application idea or business problem
2. Target users
3. Platform: web, mobile, desktop, or multiple
4. Main user roles
5. Core features
6. Business constraints
7. Preferred technology, if any
8. Expected timeline or MVP scope

When details are missing, make clearly labelled assumptions and continue with a best-effort plan.


## Coding vs Programming

Treat these as related but different activities:

| Coding | Programming |
|---|---|
| Writes instructions in a programming language | Solves the complete software problem |
| Focuses on syntax, functions, components, and files | Includes analysis, design, coding, testing, deployment, and maintenance |
| Produces code changes | Produces a reliable software outcome |
| Can be an isolated implementation task | Requires understanding users, requirements, constraints, and quality |

**Rule:** Never reduce an application request to code generation alone. First understand the problem, define expected behaviour, design the solution, then write and verify the code.

Use this decision check:

- If the request is only to implement a clearly specified function or component, perform a coding task.
- If the request involves an application, feature, business workflow, architecture, users, or uncertain requirements, treat it as a programming task and follow the full development cycle.


## System Architecture vs System Design

Treat system architecture and system design as two connected but separate levels of technical planning.

| System Architecture | System Design |
|---|---|
| Defines the high-level structure of the complete system | Defines how components and features work internally |
| Focuses on boundaries, major components, deployment, and communication | Focuses on APIs, data models, workflows, algorithms, and error handling |
| Answers “what parts exist and how do they connect?” | Answers “how will each part behave and be implemented?” |
| Usually applies across the whole application | May apply to the whole application or one feature/module |
| Produces architecture diagrams and major technology decisions | Produces detailed technical specifications and implementation guidance |

**Rule:** Create the architecture before detailed design. Do not choose tables, endpoints, classes, or algorithms until the major system boundaries and responsibilities are clear.

Use this decision check:

- If deciding monolith vs microservices, frontend/backend boundaries, cloud topology, queues, external services, scaling, availability, or trust boundaries, perform **system architecture**.
- If deciding API endpoints, database tables, object models, state transitions, validation, caching behaviour, algorithms, or failure handling, perform **system design**.
- If the user asks for “system design” broadly, provide both levels but label them separately.

### Architecture Deliverables

Include as relevant:

- Context diagram
- Container or component diagram
- Major service responsibilities
- Communication patterns
- Data ownership
- Deployment topology
- Scaling and availability approach
- Security and trust boundaries
- Major technology decisions and trade-offs

### System Design Deliverables

Include as relevant:

- Module and feature responsibilities
- API contracts
- Database schema and entity relationships
- Request and event flows
- Authentication and authorization rules
- Validation and business rules
- Caching and consistency behaviour
- Error, retry, timeout, and fallback handling
- Observability requirements
- Testable acceptance criteria


## Module-Based vs Feature-Based Architecture

Use these terms for source-code organization, not for choosing between monoliths and microservices.

| Module-Based Organization | Feature-Based Organization |
|---|---|
| Groups code by technical type or layer | Groups code by business capability |
| Examples: `components`, `services`, `hooks`, `models` | Examples: `auth`, `orders`, `payments`, `reports` |
| Simple and familiar for small projects | Easier to scale across features and teams |
| One feature may be scattered across many folders | Most feature code stays together |
| Shared technical ownership | Clearer business-feature ownership |

### Decision Rules

Choose **module-based organization** when:

- The application is small or short-lived
- It has only a few screens and business workflows
- One developer or a very small team owns most of the code
- Technical simplicity is more valuable than strict boundaries

Choose **feature-based organization** when:

- The application has several independent business capabilities
- Multiple developers or teams work in parallel
- Features change at different rates
- Clear ownership, testing, and maintainability are important
- The codebase is expected to grow

Prefer a **hybrid feature-first structure** for most medium and large applications:

```text
src/
├── app/
│   ├── router/
│   ├── providers/
│   └── config/
├── features/
│   ├── auth/
│   ├── users/
│   ├── orders/
│   └── payments/
├── shared/
│   ├── components/
│   ├── hooks/
│   ├── services/
│   ├── utils/
│   └── types/
└── layouts/
```

### Placement Rules

- Put business-specific code inside its owning feature.
- Put genuinely reusable, business-neutral code inside `shared`.
- Put application bootstrap, routing, providers, and global configuration inside `app`.
- Do not move code into `shared` merely because two files currently use it; share it only when its meaning is truly cross-feature.
- Avoid direct imports from another feature's internal folders.
- Expose a feature's supported public API through an entry point such as `index.ts`.
- Keep feature-specific UI, services, state, tests, and types close together.
- Prevent circular dependencies between features.

Example feature boundary:

```text
features/auth/
├── components/
├── hooks/
├── services/
├── state/
├── types/
├── tests/
└── index.ts
```

Other code should import from the public boundary:

```typescript
import { LoginForm, useAuth } from "@/features/auth";
```

Avoid importing private implementation details:

```typescript
import LoginForm from "@/features/auth/components/LoginForm";
```

### Backend Application

The same principle applies on the backend. Organize business capabilities such as `users`, `billing`, `orders`, and `notifications` as bounded modules. Inside each feature, keep its controllers, services, domain rules, repositories, schemas, and tests together when the framework allows it.

### Architecture Deliverables

When code organization is in scope, document:

- Selected organization style and rationale
- Feature boundaries and ownership
- Shared-code rules
- Allowed dependency direction
- Public interfaces between features
- Naming and folder conventions
- Strategy for preventing circular dependencies
- Migration plan if reorganizing an existing project

**Rule:** Organize business functionality by feature and reusable technical capabilities by shared modules. Do not create one global folder for every file type in a growing business application.

## Clean Code and File Naming

Clean code is code that another developer can understand, test, change, and maintain without unnecessary effort. A clean filename makes the purpose and ownership of a file obvious before opening it.

### Clean-Code Principles

Apply these rules during implementation and review:

- Use names that reveal intent.
- Keep functions and components focused on one responsibility.
- Prefer simple control flow over deeply nested conditions.
- Remove duplication only when the shared abstraction is genuinely stable.
- Keep business rules separate from UI, transport, and persistence details.
- Validate inputs at system boundaries.
- Handle expected failures explicitly.
- Write comments to explain important reasons or trade-offs, not obvious syntax.
- Keep public interfaces small and predictable.
- Add tests for important behaviour, edge cases, and regressions.

Bad:

```typescript
const x = 18;
function doIt(a: number) {
  return a + x;
}
```

Better:

```typescript
const taxPercentage = 18;

function calculatePriceWithTax(basePrice: number): number {
  return basePrice + (basePrice * taxPercentage) / 100;
}
```

### Function and Component Rules

- A function should perform one clear job at one level of abstraction.
- Prefer early returns when they make conditions easier to read.
- Avoid boolean parameters whose meaning is unclear at the call site.
- Keep side effects visible and controlled.
- Split large components when they combine data fetching, business logic, and multiple UI responsibilities.
- Do not split code into tiny functions when that makes the flow harder to follow.

### File-Naming Principles

A filename should describe the main responsibility or primary export of the file.

Avoid vague or temporary names:

```text
file.ts
new.ts
temp.ts
helper2.ts
component-final.tsx
```

Prefer specific names:

```text
calculateOrderTotal.ts
authService.ts
orderRepository.ts
LoginForm.tsx
paymentWebhookHandler.ts
```

### Naming-Conventions Decision

Select conventions based on the language and framework, then apply them consistently across the repository.

| File category | Common convention | Examples |
|---|---|---|
| React components and classes | PascalCase | `ProductCard.tsx`, `UserProfile.tsx` |
| Functions, hooks, services, utilities | camelCase or kebab-case | `useAuth.ts`, `formatCurrency.ts`, `auth-service.ts` |
| Routes and framework pages | Framework convention | `page.tsx`, `route.ts`, `user-profile.vue` |
| Tests | Match source name plus test suffix | `authService.test.ts`, `OrderController.spec.ts` |
| Constants and configuration | Project convention | `apiConfig.ts`, `featureFlags.ts` |

**Rule:** Follow the established repository convention before introducing a new one. Consistency is more valuable than personal preference.

### Match Filename and Main Export

When one file has one primary component, class, service, or function, align its filename with that export.

```tsx
// ProductCard.tsx
export function ProductCard() {
  return <article>Product</article>;
}
```

Avoid files whose names disagree with their main responsibility.

### Feature-Based Naming

Use the feature context to remove ambiguity:

```text
features/orders/services/createOrder.ts
features/orders/components/OrderSummary.tsx
features/auth/hooks/useAuth.ts
features/payments/api/paymentClient.ts
```

Do not repeat unnecessary context when the folder already provides it. For example, inside `features/orders`, prefer `createOrder.ts` over `createOrderOrderService.ts`.

### Generic Names

Names such as `utils`, `helpers`, `common`, `manager`, and `data` often hide mixed responsibilities.

Use them only when the contents are truly cohesive. Prefer domain-specific names such as:

```text
formatCurrency.ts
parseDateRange.ts
validateCheckout.ts
sessionStorage.ts
```

### Renaming and Refactoring Rules

- Rename files and exports together.
- Update imports using refactoring tools where possible.
- Preserve version-control history with a proper move or rename.
- Avoid mixing large naming changes with unrelated feature work.
- Run tests, type checks, linting, and build verification after renaming.
- Respect case-sensitive filesystems; names that work on one operating system may fail in CI or production.

### Clean-Code Review Checklist

Before approving implementation, verify:

- Names communicate purpose without requiring extra explanation.
- Functions, classes, and components have focused responsibilities.
- Complex logic has been simplified or clearly structured.
- Error paths and boundary validation are present.
- Duplication has not created inconsistent business rules.
- Comments explain reasons rather than restating code.
- Filenames follow the repository convention.
- The main export matches the filename where appropriate.
- No vague files such as `temp`, `misc`, `final`, or numbered copies remain.
- Tests, linting, type checks, and the build pass after changes.

**Rule:** Code is not complete merely because it runs. It is complete when its intent is clear, its behaviour is verified, and its files are easy to locate and safely change.



## Recommend the Best Approach Before Planning

Do not create an implementation plan immediately. First inspect the problem, compare realistic approaches, recommend the best option, and then plan the work.

### 1. Understand the Decision

Determine:

- The real problem and required outcome
- Existing repository architecture and conventions
- Functional and non-functional requirements
- Project size and expected growth
- Team skills and maintenance capacity
- Delivery urgency
- Security, performance, and reliability needs
- Existing dependencies and infrastructure
- Constraints that cannot be changed

When information is missing, inspect the repository and state assumptions clearly.

### 2. Identify Viable Approaches

For a non-trivial decision, consider two or three realistic approaches.

Examples:

- Extend an existing module or create a new feature boundary
- Use a local solution or shared infrastructure
- Use synchronous work or a background job
- Keep a modular monolith or introduce a service boundary
- Reuse an existing dependency or add a new library
- Refactor first or make a minimal compatible change
- Use server state, client state, URL state, or local component state

Do not invent alternatives when repository rules or user constraints clearly require one solution.

### 3. Compare Trade-offs

Evaluate relevant criteria:

| Criterion | Evaluation |
|---|---|
| Correctness | Satisfies required behaviour and edge cases |
| Simplicity | Uses the smallest clear solution |
| Repository fit | Matches existing architecture and conventions |
| Maintainability | Remains understandable and safe to change |
| Scalability | Supports expected growth without premature complexity |
| Security | Protects data and limits attack surface |
| Performance | Is efficient enough for realistic usage |
| Testability | Allows important behaviour to be verified |
| Delivery risk | Minimizes regressions and unnecessary delay |
| Reversibility | Can be changed later without excessive cost |

### 4. Recommend One Approach

State the decision before writing the plan:

```text
Recommended approach:
[Approach name]

Why:
- [Primary reason]
- [Repository or requirement fit]
- [Maintainability or risk reason]

Trade-offs:
- [Known cost or limitation]
- [What is intentionally not optimized]

Rejected alternatives:
- [Alternative]: [Concrete reason it is weaker here]
```

Be decisive. Do not leave the choice unresolved unless the user explicitly asks for options only.

### 5. Record Planning Assumptions

Before planning, record:

- Chosen approach
- Scope boundaries
- Important assumptions
- Affected features or modules
- Compatibility or migration needs
- Verification strategy
- Important risks

### 6. Create the Implementation Plan

Only after choosing the approach, create an ordered plan.

Each step should include:

- Goal
- Likely files or modules
- Behaviour to add or preserve
- Tests or verification
- Dependencies
- Completion condition

### Proportionality

- **Small change:** Brief recommendation, one alternative, and a short plan.
- **Medium feature:** Compare two or three options with important trade-offs.
- **Architecture or high-risk change:** Include migration impact, failure modes, rollback, and staged delivery.

Do not over-design a small fix. Do not under-analyze a major architectural change.

### Quality Gate

Before planning, verify:

- A meaningful alternative was considered for non-trivial decisions
- The recommendation fits the repository
- The simplest sufficient solution is preferred
- Security and failure modes were considered
- Premature abstraction is avoided
- Trade-offs are explicit
- Rejected alternatives have concrete reasons
- The decision clearly guides implementation

**Rule:** Recommend first. Plan second. Code third.


## Evidence-Based Code Optimization

Optimize only after correctness is established and a meaningful bottleneck or efficiency goal is identified. Do not trade clarity, safety, or maintainability for unmeasured speed.

### Optimization Order

Use this order:

1. **Correctness:** Preserve required behaviour and edge cases.
2. **Measure:** Establish a baseline using profiling, benchmarks, logs, query plans, bundle analysis, or production metrics.
3. **Locate:** Identify the actual hot path, expensive query, repeated request, large allocation, or unnecessary render.
4. **Improve:** Apply the smallest high-impact change.
5. **Verify:** Re-run correctness tests and compare before/after measurements.
6. **Document:** Record trade-offs when the optimized solution is less obvious.

**Rule:** No optimization claim without before-and-after evidence when measurement is practical.

### Optimization Priorities

Prefer improvements in this order:

| Priority | Examples |
|---|---|
| Algorithm and data structure | Replace repeated linear scans, avoid nested work, use appropriate indexing or lookup structures |
| I/O and network | Remove duplicate requests, batch operations, paginate, stream, compress, cache carefully |
| Database | Fix N+1 queries, add justified indexes, reduce selected columns, use query plans, avoid unnecessary transactions |
| Rendering and state | Prevent unnecessary re-renders, colocate state, virtualize large lists, memoize only measured hot paths |
| Memory | Avoid retaining large objects, release resources, stream large payloads, reduce copies and allocations |
| Build and delivery | Reduce bundle size, lazy-load meaningful boundaries, remove dead dependencies, optimize assets |
| Micro-optimization | Tight-loop or allocation tuning only after higher-impact options are exhausted |

### Complexity Review

For performance-sensitive code, state the expected time and space complexity when useful.

Check for:

- Repeated work inside loops
- Nested iteration over growing collections
- Unbounded in-memory accumulation
- Expensive serialization or parsing
- Repeated computation that can be safely reused
- Blocking work on request or UI-critical paths
- Excessive database or API round trips

Do not replace a clear linear solution with a complex structure unless scale or measurement justifies it.

### Frontend Optimization

Inspect:

- Unnecessary component re-renders
- State stored higher than required
- Derived state duplicated instead of computed
- Oversized bundles and eagerly loaded routes
- Large lists rendered without pagination or virtualization
- Images, fonts, and assets loaded at inappropriate sizes
- Repeated client requests or missing request deduplication
- Expensive calculations during render

Use memoization only when referential stability or measured render cost requires it. Unnecessary memoization adds complexity and can make performance worse.

### Backend and API Optimization

Inspect:

- N+1 database queries
- Missing pagination or unsafe unbounded queries
- Repeated external service calls
- Missing timeouts and cancellation
- Sequential independent I/O that can safely run concurrently
- Large response payloads
- Slow serialization or unnecessary transformations
- Work that belongs in a background job
- Cache opportunities with clear invalidation rules

Never add concurrency without considering ordering, rate limits, resource exhaustion, retries, and partial failure.

### Database Optimization

Before changing queries or indexes:

- Capture the slow query and representative parameters
- Inspect the execution plan when available
- Verify table size and access pattern
- Check existing indexes
- Consider write cost and storage overhead
- Test realistic data volume

An index is justified only when its read benefit outweighs write and maintenance cost.

### Caching Rules

Before adding a cache, define:

- What is cached
- Cache key
- Lifetime or eviction rule
- Invalidation source
- Consistency expectations
- Failure fallback
- Memory or storage limit
- Whether sensitive data is safe to cache

Do not use caching to hide an inefficient algorithm or broken query unless the underlying issue is also understood.

### Memory and Resource Safety

Check for:

- Event listeners or subscriptions not removed
- Timers not cleared
- Streams, files, sockets, or database connections not closed
- Unbounded queues, maps, logs, or caches
- Large objects retained by closures
- Full-file loading where streaming is appropriate

Performance improvements must not introduce leaks or resource starvation.

### Benchmark and Profiling Standards

A useful benchmark should:

- Exercise representative data and realistic workloads
- Run enough times to reduce noise
- Separate warm-up from measured execution when relevant
- Compare the same environment and inputs
- Report latency, throughput, memory, bundle size, query count, or another task-relevant metric
- Avoid benchmarking only synthetic code when end-to-end behaviour is the true bottleneck

### Optimization Trade-offs

For every non-trivial optimization, consider:

- Readability cost
- Maintenance cost
- Correctness risk
- Cache consistency risk
- Memory versus CPU trade-off
- Latency versus throughput trade-off
- Build size versus runtime speed
- Immediate gain versus future flexibility

Prefer reversible optimizations and preserve simple interfaces around complex internals.

### Optimization Rejection Conditions

Do not approve an optimization when:

- No meaningful bottleneck or target is identified
- There is no baseline measurement when one is practical
- Tests do not protect existing behaviour
- The change relies on unrealistic benchmark data
- Complexity increases for negligible benefit
- Cache invalidation is undefined
- Concurrency failure modes are ignored
- Memory usage or resource limits are unbounded
- Security or data correctness is weakened
- The claimed improvement was not re-measured

### Required Optimization Report

When optimization is part of the task, report:

```text
Optimization target:
[What was slow or inefficient]

Baseline:
[Measurement and method]

Change:
[What was changed and why]

Result:
[Before/after measurement]

Trade-offs:
[Complexity, memory, consistency, or maintenance impact]

Verification:
[Tests, profiling, build, and relevant checks]
```

**Rule:** Make the common path faster only when evidence shows it matters, and keep the code understandable enough to maintain safely.


## Code Structure Standard

Organize code so that ownership, dependencies, and change boundaries are obvious. A good structure helps developers find behaviour quickly and modify one feature without unexpectedly breaking another.

### Structural Goals

The project structure should make these questions easy to answer:

- Where does a feature live?
- Which module owns a business rule?
- Which code is reusable across features?
- Which layer communicates with external systems?
- Where are tests located?
- Which imports are public and supported?
- Which dependencies are allowed?

### Preferred High-Level Structure

Use a feature-first structure for medium and large applications:

```text
src/
├── app/
│   ├── config/
│   ├── providers/
│   ├── router/
│   └── bootstrap/
├── features/
│   ├── auth/
│   ├── users/
│   ├── products/
│   └── orders/
├── shared/
│   ├── components/
│   ├── utilities/
│   ├── types/
│   └── infrastructure/
└── main.ts
```

Use a simpler module-based structure only when the project is small and unlikely to grow significantly.

### Feature Boundary

A feature should own its related behaviour:

```text
features/orders/
├── api/
├── components/
├── domain/
├── hooks/
├── pages/
├── services/
├── state/
├── tests/
├── types/
└── index.ts
```

Not every feature needs every folder. Create only the folders that represent real responsibilities.

### Layer Responsibilities

| Layer | Responsibility |
|---|---|
| `app` | Application startup, global providers, routing, and configuration |
| `features` | Business capabilities and feature-specific behaviour |
| `shared` | Stable reusable code with no feature ownership |
| `domain` | Business rules, entities, and value objects |
| `api` or `infrastructure` | HTTP, database, queues, storage, and third-party integrations |
| `components` | Presentation and user interaction |
| `services` | Coordinating use cases or external operations |
| `tests` | Behaviour verification close to the code it protects |

### Dependency Direction

Prefer dependencies that flow inward toward stable business rules:

```text
UI → application/use cases → domain
                     ↓
              infrastructure
```

Rules:

- Domain code must not depend on UI frameworks.
- Business rules must not depend directly on HTTP, database, or vendor SDKs.
- Shared code must not import feature-specific code.
- One feature must not reach into another feature's internal folders.
- Cross-feature communication should use public exports, events, or well-defined interfaces.
- Avoid circular dependencies.

### Public Exports

Each feature should expose a small public surface:

```text
features/auth/index.ts
```

Consumers should import from:

```typescript
import { LoginForm, useAuth } from "@/features/auth";
```

Avoid deep internal imports:

```typescript
import { LoginForm } from "@/features/auth/components/forms/LoginForm";
```

Deep imports couple callers to internal structure and make refactoring harder.

### File Responsibility

Each file should have one clear purpose.

Prefer:

```text
createOrder.ts
calculateOrderTotal.ts
OrderRepository.ts
OrderSummary.tsx
useOrderFilters.ts
```

Avoid:

```text
helpers.ts
utils.ts
common.ts
misc.ts
everything.ts
```

Generic filenames are acceptable only when the scope is already narrow and unambiguous.

### Test Placement

Use one consistent strategy:

**Colocated tests**

```text
calculateOrderTotal.ts
calculateOrderTotal.test.ts
```

**Feature test folder**

```text
features/orders/
├── domain/
├── services/
└── tests/
```

Choose based on repository conventions. Do not mix styles without a clear reason.

### Frontend Structure Rules

- Keep reusable design-system components in `shared`.
- Keep business-specific components inside their feature.
- Separate presentation from data-fetching logic when complexity justifies it.
- Keep route-level components thin.
- Avoid global state for state owned by one feature or component.
- Keep server-state handling separate from local UI state.
- Co-locate styles, tests, and stories when the repository supports it.

### Backend Structure Rules

- Keep transport logic thin.
- Put business rules outside controllers and route handlers.
- Keep persistence behind repositories or equivalent interfaces when useful.
- Separate validation from persistence.
- Avoid placing all logic in one service file.
- Organize code by business capability rather than only by technical layer when the codebase grows.
- Keep migrations, schemas, and data-access ownership clear.

### Structure Decision Guide

Use module-based organization when:

- The project is small
- The team is small
- The domain is simple
- Features have little independent ownership

Use feature-based organization when:

- The application has several business capabilities
- Multiple developers work in parallel
- Features evolve independently
- The codebase is expected to grow

Use a hybrid approach when:

- Global application concerns must remain centralized
- Business code should stay feature-owned
- Stable reusable code belongs in shared modules

### Refactoring Structure Safely

When restructuring code:

1. Preserve behaviour with tests.
2. Move one boundary at a time.
3. Update imports mechanically.
4. Keep public interfaces stable where possible.
5. Run tests, type checks, linting, and builds after each meaningful move.
6. Review the final diff for accidental edits.
7. Remove dead paths only after verifying no callers remain.

Do not combine a large structural refactor with unrelated feature development unless necessary.

### Code Structure Quality Gate

Before approving the structure, verify:

- Feature ownership is clear
- Business logic is not trapped in UI or transport layers
- Shared code is genuinely reusable
- Dependencies flow in the intended direction
- Circular imports are absent
- Public exports are small and intentional
- Filenames describe responsibilities
- Tests are easy to locate
- New developers can find feature code quickly
- The structure matches project size and team needs
- Empty or speculative folders were not added
- The structure supports change without unnecessary coupling

**Rule:** Structure code around responsibility and change boundaries, not around arbitrary folder names.


## Senior Programmer Code-Quality Gate

Treat correctness, readability, and understandability as separate requirements. A change is not complete unless it satisfies all three.

| Quality dimension | Required outcome |
|---|---|
| Correctness | The code produces the required behaviour and handles relevant failures |
| Readability | A developer can follow the control flow and naming without decoding the implementation |
| Understandability | The purpose, business rules, inputs, outputs, side effects, and failure conditions are apparent |
| Maintainability | The change can be extended or fixed without unnecessary coupling or duplication |
| Testability | Important behaviour can be verified through focused automated tests or strong equivalent checks |

### Understand Before Changing

Before editing code, Codex must be able to state:

- What responsibility the relevant module owns
- Which behaviour is changing
- Which public interface or caller depends on it
- Where business rules belong
- Which inputs are trusted or untrusted
- Which side effects occur
- What can fail
- How the change will be verified

If these cannot be determined, inspect more of the repository before implementation.

### Readability Rules

- Use domain language instead of generic abbreviations.
- Name booleans as states or questions, such as `isActive`, `hasPermission`, or `canCancelOrder`.
- Keep related statements close together.
- Use guard clauses when they reduce nesting.
- Avoid clever expressions that save lines but hide intent.
- Extract a named concept when an expression represents an important business rule.
- Keep one level of abstraction within a function where practical.
- Make side effects visible in names and structure.
- Prefer explicit error handling over silent failure.
- Keep the happy path easy to find.

```typescript
function canUserCancelOrder(order: Order, user: User): boolean {
  const ownsOrder = order.customerId === user.id;
  const isPending = order.status === "pending";

  return ownsOrder && isPending;
}
```

Prefer this over an unexplained compound condition repeated across controllers or components.

### Function Review Questions

For every changed function, ask:

1. Does its name describe the result or action?
2. Does it perform one cohesive responsibility?
3. Are its inputs and return value clear?
4. Are side effects obvious?
5. Are failure modes handled or deliberately propagated?
6. Is complex branching necessary?
7. Would extracting a business rule improve clarity?
8. Is the function tested at the appropriate level?

Do not enforce arbitrary line-count limits. Split functions when responsibilities or abstraction levels are mixed.

### Comments and Documentation

Use comments for:

- Non-obvious business reasons
- Compatibility constraints
- Security decisions
- Performance trade-offs
- Temporary workarounds
- Invariants future changes must preserve

Do not use comments to translate obvious syntax. Improve names or structure instead.

### Error-Handling Standard

- Never swallow an error without an intentional fallback.
- Preserve useful context when wrapping errors.
- Avoid leaking secrets or sensitive user data into logs.
- Return errors at the correct abstraction level.
- Distinguish validation, authorization, not-found, conflict, dependency, and unexpected failures when needed.
- Test important failure paths, not only successful execution.

### Duplication and Abstraction

Create an abstraction when:

- The duplicated code represents the same stable concept
- The implementations must change together
- The abstraction has clear ownership and a meaningful name

Keep code separate when:

- Similar code serves different business rules
- Sharing would require unrelated flags or branching
- The duplication is clearer than a premature framework

### Senior Review Sequence

Review code in this order:

1. **Behaviour:** Acceptance criteria are satisfied.
2. **Safety:** Validation, authorization, data integrity, and failures are handled.
3. **Design:** Responsibility is placed in the correct feature or module.
4. **Readability:** Another developer can understand the intent quickly.
5. **Maintainability:** Coupling is controlled and duplication is reasonable.
6. **Verification:** Tests and repository checks prove the change works.
7. **Diff hygiene:** Unrelated edits, debug code, and temporary files are absent.

### Required Completion Evidence

Before reporting completion, include evidence for applicable checks:

- Focused test command and result
- Type-check or compile result
- Lint result
- Build result
- Relevant integration or manual verification
- Final diff review

If a check cannot run, state the exact reason and the alternative verification used.

### Code-Quality Rejection Conditions

Do not approve or claim completion when any of these remain without explanation:

- Vague names that hide business meaning
- Mixed UI, business, persistence, or transport responsibilities
- Silent error handling
- Deep nesting that obscures the main path
- Repeated business rules that can drift
- Unvalidated external input
- Unclear feature ownership
- Dead code, debug output, or temporary files
- Missing regression coverage for a bug fix
- Claims of passing checks without observed output

**Rule:** Optimize code for the next developer who must understand and safely change it, not merely for the current implementation to execute.


## Application Development Cycle

### 1. Discovery

Identify:

- Business problem
- Target users
- Existing alternatives
- Expected business value
- Main success metrics
- Constraints and risks

**Primary roles:** Product Manager, Business Analyst, stakeholders.

**Output:** Problem statement and project goals.

### 2. Requirements

Define:

- User roles
- Functional requirements
- Non-functional requirements
- User stories
- Acceptance criteria
- MVP and future features
- Out-of-scope items

**Primary roles:** Business Analyst, Product Manager, technical lead.

**Output:** PRD or Software Requirements Specification.

### 3. Planning

Decide:

- Team structure
- Technology stack
- Architecture direction
- Development phases
- Milestones
- Dependencies
- Risk controls

**Primary roles:** Project Manager, Software Architect, technical lead.

**Output:** Roadmap, task backlog, timeline, and responsibility matrix.

### 4. UI/UX Design

Create:

- User flows
- Information architecture
- Wireframes
- High-fidelity screens
- Responsive layouts
- Clickable prototype
- Design system or reusable UI rules

**Primary roles:** UI/UX Designer, Product Manager, frontend lead.

**Output:** Approved design and interaction specifications.

### 5. System Architecture

Define the high-level structure:

- System boundaries and external actors
- Major applications, services, and components
- Monolith, modular monolith, or microservice direction
- Communication patterns such as HTTP, events, or queues
- Data ownership and storage boundaries
- Deployment topology and cloud infrastructure
- Scaling, availability, resilience, and disaster recovery
- Security and trust boundaries
- Major technology decisions and trade-offs

**Primary roles:** Software Architect, technical lead, DevOps, security engineer.

**Output:** Architecture decision records, context/component diagrams, and deployment view.

### 6. System Design

Translate the architecture into implementation-ready details:

- Module and feature boundaries
- Source-code organization: module-based, feature-based, or hybrid
- Allowed dependency direction and public feature interfaces
- Database schema and entity relationships
- API and event contracts
- Authentication and authorization flows
- Business rules and state transitions
- Validation and error responses
- Caching and consistency decisions
- Third-party integration behaviour
- Logging, metrics, tracing, backup, and monitoring requirements
- Failure handling, retries, timeouts, and fallbacks

**Primary roles:** Software Architect, frontend and backend leads, database engineer, DevOps, security engineer.

**Output:** Detailed design document, ER diagram, sequence diagrams, and API specification.

### 7. Programming and Implementation

Before writing code:

- Confirm the user story and acceptance criteria
- Identify edge cases and failure states
- Confirm API contracts and data models
- Choose a small, testable implementation approach
- Add or update tests for the expected behaviour

Coding begins only after these programming decisions are clear.

#### Frontend Coding

- Build reusable UI components
- Implement responsive screens
- Add forms and validation
- Integrate APIs
- Handle loading, empty, success, and error states
- Add accessibility and browser compatibility

#### Backend Coding

- Build APIs and business logic
- Implement authentication and permissions
- Design database models
- Add validation and error handling
- Integrate email, payments, notifications, or external services
- Add logging and automated tests

**Primary roles:** Frontend Developer, Backend Developer, Full-Stack Developer.

**Output:** Working application increments.

### 8. Code Review

Check:

- Requirement compliance
- Correctness
- Security
- Performance
- Maintainability
- Test coverage
- Coding standards

**Output:** Approved pull request or documented changes.

### 9. Testing

Perform:

- Unit testing
- API and integration testing
- UI and functional testing
- Responsive and cross-browser testing
- Permission testing
- Performance testing
- Security testing
- Regression testing

**Primary role:** QA Engineer, supported by developers.

**Output:** Test report and bug list.

### 10. Bug Resolution

Follow this loop:

`Bug reported → Reproduced → Prioritized → Fixed → Reviewed → Retested → Closed`

Never close a bug without verifying the expected behavior.

### 11. User Acceptance Testing

Confirm that:

- Required workflows work end to end
- Acceptance criteria are satisfied
- Business users approve the release
- Critical issues are resolved

**Output:** Release approval.

### 12. Deployment

Prepare:

- Production environment
- Domain and SSL
- Environment variables
- Database migrations
- CI/CD pipeline
- Monitoring and alerts
- Backups and rollback plan

**Primary role:** DevOps Engineer with development support.

**Output:** Production release.

### 13. Maintenance and Improvement

Continue with:

- Production monitoring
- Bug fixes
- Security updates
- Performance improvements
- User feedback analysis
- New feature planning
- Database and infrastructure maintenance

**Output:** Stable releases and an updated product backlog.

## Role Responsibility Guide

| Role | Main responsibility |
|---|---|
| Product Manager | Defines product direction and priorities |
| Business Analyst | Converts business needs into clear requirements |
| Project Manager | Manages tasks, timeline, dependencies, and communication |
| UI/UX Designer | Designs usable interfaces and user journeys |
| Software Architect | Defines technical structure and major engineering decisions |
| Frontend Developer | Builds the user-facing interface |
| Backend Developer | Builds APIs, business logic, authentication, and data processing |
| Full-Stack Developer | Works across frontend and backend |
| Database Engineer | Designs and optimizes data storage |
| QA Engineer | Tests features and verifies fixes |
| DevOps Engineer | Automates deployment and manages infrastructure |
| Security Engineer | Reviews threats, access controls, and vulnerabilities |

## Developer Daily Work Cycle

1. Understand the problem, user outcome, and acceptance criteria.
2. Confirm the design, API contract, data model, dependencies, and risks.
3. Break the solution into small testable tasks.
4. Define expected success, error, loading, permission, and edge-case behaviour.
5. Create or update automated tests and verify new tests fail for the expected reason.
6. Create a Git branch.
7. Write the minimum code required to satisfy the test and requirement.
8. Run local tests, linting, type checks, and relevant quality checks.
9. Refactor while keeping tests green.
10. Commit and push the code.
11. Open a pull request that explains the problem, solution, tests, and risks.
12. Address code-review feedback.
13. Merge only after approval and successful checks.
14. Deploy to the test or staging environment.
15. Support QA and fix verified defects.
16. Mark the task complete only after acceptance criteria are verified.

## Codex Change Output

For repository implementation tasks, prefer this completion format:

### Summary
Describe the user-visible or developer-visible outcome.

### Implementation
List the main modules changed and the approach used.

### Verification
Include the exact checks run and whether each succeeded.

### Notes
Mention migrations, compatibility concerns, assumptions, or unresolved limitations only when relevant.

## Recommended Output Format

When applying this skill, produce:

### 1. Project Summary
A concise explanation of the problem, solution, users, and platform.

### 2. Assumptions
Clearly label any inferred information.

### 3. User Roles
List each application user and their permissions.

### 4. MVP Features
Separate essential features from future enhancements.

### 5. Development Phases
Present discovery, design, development, testing, deployment, and maintenance.

### 6. Team Roles
Explain who is responsible for each phase.

### 7. Suggested Technology Stack
Recommend technologies based on scale, team experience, budget, and maintainability.

### 8. Data and API Plan
Describe major entities, modules, and integrations.

### 9. Testing Strategy
Include functional, security, responsive, performance, and regression testing.

### 10. Risks
Identify technical, business, security, schedule, and dependency risks.

### 11. Immediate Next Actions
Give a short, ordered set of tasks that can begin now.

## Quality Checklist

Before completing the plan, verify:

- Repository instructions and existing conventions were inspected
- Git status and unrelated user changes were respected
- The problem and target users are defined
- The plan distinguishes programming decisions from code-writing tasks
- Every major feature belongs to a user role
- MVP and future scope are separated
- Requirements have testable acceptance criteria
- Frontend and backend responsibilities are clear
- Module and feature boundaries are explicit
- Shared code has clear ownership and dependency rules
- System architecture and detailed system design are separated
- Major architectural decisions include rationale and trade-offs
- APIs, data models, failure states, and security rules are implementation-ready
- Authentication and permissions are covered
- Security, validation, errors, and backups are considered
- Testing happens before production deployment
- Deployment includes monitoring and rollback
- The final diff contains no accidental or unrelated edits
- Completion claims are supported by successful verification output
- The plan contains concrete next actions

## Common Mistakes

### Starting with technology instead of the problem
Choose the stack after understanding users, scope, scale, and constraints.

### Treating every feature as MVP
Prioritize the smallest version that delivers the main user outcome.

### Writing vague requirements
Replace “user can manage appointments” with explicit create, view, reschedule, cancel, permission, and notification rules.

### Ignoring non-functional requirements
Include security, performance, accessibility, responsiveness, reliability, and maintainability.

### Separating frontend and backend too late
Define API contracts and data models before parallel implementation.

### Testing only at the end
Test each increment and keep regression coverage throughout development.

### Deploying without recovery planning
Always include monitoring, backups, migration safety, and rollback steps.
