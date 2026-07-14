---
name: projectforge
description: Use when a user wants to turn an application idea into a structured IT project plan, define team roles, understand the software development lifecycle, or create an actionable workflow from requirements through maintenance.
---

# ProjectForge

## Overview

Convert an application idea into a practical development workflow. Clarify the problem, define users and features, assign responsibilities, select an appropriate architecture, and produce a phased delivery plan.

**Core principle:** Do not begin implementation until the problem, users, scope, and acceptance criteria are clear enough to test.

## When to Use

Use this skill when the user asks to:

- Create a web, mobile, desktop, SaaS, or internal business application
- Understand which IT roles are required
- Convert an idea into a development roadmap
- Define the work cycle for an application team
- Prepare requirements before coding
- Organize frontend, backend, QA, DevOps, design, and product work
- Create an MVP feature list or project phases

Do not use it only for a small isolated code fix with already-defined requirements.

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
