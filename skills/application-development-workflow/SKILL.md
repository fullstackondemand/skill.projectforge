---
name: application-development-workflow
description: Use when a user wants to turn an application idea into a structured IT project plan, define team roles, understand the software development lifecycle, or create an actionable workflow from requirements through maintenance.
---

# Application Development Workflow

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

### 5. Technical Design

Define:

- System architecture
- Database schema
- API contracts
- Authentication and authorization
- Third-party integrations
- Security controls
- Logging, backup, and monitoring requirements

**Primary roles:** Software Architect, backend lead, DevOps, security engineer.

**Output:** Architecture document, ER diagram, and API specification.

### 6. Development

#### Frontend

- Build reusable UI components
- Implement responsive screens
- Add forms and validation
- Integrate APIs
- Handle loading, empty, success, and error states
- Add accessibility and browser compatibility

#### Backend

- Build APIs and business logic
- Implement authentication and permissions
- Design database models
- Add validation and error handling
- Integrate email, payments, notifications, or external services
- Add logging and automated tests

**Primary roles:** Frontend Developer, Backend Developer, Full-Stack Developer.

**Output:** Working application increments.

### 7. Code Review

Check:

- Requirement compliance
- Correctness
- Security
- Performance
- Maintainability
- Test coverage
- Coding standards

**Output:** Approved pull request or documented changes.

### 8. Testing

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

### 9. Bug Resolution

Follow this loop:

`Bug reported → Reproduced → Prioritized → Fixed → Reviewed → Retested → Closed`

Never close a bug without verifying the expected behavior.

### 10. User Acceptance Testing

Confirm that:

- Required workflows work end to end
- Acceptance criteria are satisfied
- Business users approve the release
- Critical issues are resolved

**Output:** Release approval.

### 11. Deployment

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

### 12. Maintenance and Improvement

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

1. Review the assigned user story and acceptance criteria.
2. Confirm design, API contract, and dependencies.
3. Break the story into small technical tasks.
4. Create or update automated tests.
5. Create a Git branch.
6. Implement the smallest complete change.
7. Test locally.
8. Commit and push the code.
9. Open a pull request.
10. Address code-review feedback.
11. Merge after approval.
12. Deploy to the test or staging environment.
13. Support QA and fix defects.
14. Mark the task complete only after verification.

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
- Every major feature belongs to a user role
- MVP and future scope are separated
- Requirements have testable acceptance criteria
- Frontend and backend responsibilities are clear
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
