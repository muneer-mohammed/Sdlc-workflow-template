# Workflow & Agent Bootstrap — Technology-Agnostic Reusable SDLC Template

**applyTo:** `**/*`

TL;DR
This file defines a technology‑agnostic SDLC: feature intake → design → implementation → verification → release. Use it as the canonical workflow; project-specific skills and configuration belong in the .claude/skills, pipeline/, and docs/ areas.

How to use
1. Read `AGENTS.md` first, then `pipeline/orchestration.md`.
2. Use the feature files in `pipeline/features/` for official specs and decisions.
3. Author agents and skills using the templates in `docs/AGENTS-templates.md` and `docs/SKILLS-templates.md`.
4. Make changes via a feature branch and open a draft PR; do not merge without required human approval.

Table of Contents
- TL;DR & How to use
- 1. Technology-Agnostic Design Principle
- 2. Core Purpose
- 3. Core Principles
- 4. Required Repository Structure
- 5. Universal vs Project-Specific Rules
- 6. Repository Entry Point
- 7. Feature State Machine
- 8. Feature Intake
- 9. Branch or Workspace Setup
- 10. Feature Specification
- 11. Definition of Ready
- 12. Architecture and Design
- 13. Architecture Review
- 14. Implementation Planning
- 15. Implementation
- 16. Automated Quality Checks
- 17. Testing Strategy
- 18. Architecture Fitness Checks
- 19. Contract and Compatibility Validation
- 20. QA Validation
- 21. Build and Package Verification
- 22. Final Review Gate
- 23. Human Approval
- 24. Delivery
- 25. Release and Deployment Workflow
- 26. Safe Release Strategies
- 27. Observability
- 28. Production Validation
- 29. Incident and Defect Management
- 30. Developer Experience
- 31. Engineering Metrics
- 32. Security
- 33. AI-Assisted Development
- 34. AI Application Quality
- 35. Required Agent Definitions (see docs/AGENTS-templates.md)
- 36. Required Skills (see docs/SKILLS-templates.md)
- 37. Repository Conventions
- 38. Execution Logging
- 39. Review Checklist
- 40. Continuous Improvement Loop
- 41. Success Criteria
- 42. Canonical Lifecycle Summary

## Purpose

Use this instruction file whenever a project needs a canonical Software Development Lifecycle (SDLC), feature delivery workflow, engineering quality model, and supporting agent definitions.

This template is intentionally:

* Technology agnostic
* Programming-language agnostic
* Framework agnostic
* Cloud-provider agnostic
* Database agnostic
* Architecture-style agnostic

It can be applied to projects using different combinations of:

* Backend, frontend, mobile, desktop, data, infrastructure, or AI systems
* Monoliths, modular monoliths, microservices, event-driven systems, or serverless architectures
* Relational databases, NoSQL databases, files, streams, or external services
* Cloud platforms, hybrid environments, or on-premises infrastructure

The canonical workflow defines **how work moves through the SDLC**.

Project-specific skills and conventions define **how that work is implemented for the selected technology stack**.

---

# 1. Technology-Agnostic Design Principle

The repository workflow must separate:

```text
Universal SDLC Principles
        ↓
Canonical Workflow
        ↓
Project Architecture
        ↓
Stack-Specific Skills
        ↓
Tool-Specific Commands and Configuration
```

The canonical SDLC workflow must not assume:

* A specific programming language
* A specific framework
* A specific dependency injection mechanism
* A specific database
* A specific cloud provider
* A specific testing framework
* A specific CI/CD provider
* A specific source control platform

Technology-specific details belong in project-level skills, conventions, configuration, and implementation documentation.

## Example

The canonical workflow may require:

> Run the project's required build and verification process.

The project-specific build skill defines:

```text
Project A → dotnet build
Project B → mvn verify
Project C → npm run build
Project D → go test ./...
```

The workflow remains unchanged.

---

# 2. Core Purpose

The goal is to create a consistent, traceable, developer-friendly SDLC that improves:

* Developer productivity
* Software quality
* Reliability
* Security
* Maintainability
* Delivery confidence
* Operational visibility

The complete lifecycle is:

```text
Feature Intake
  ↓
Definition of Ready
  ↓
Specification
  ↓
Architecture & Design
  ↓
Architecture Review
  ↓
Planning
  ↓
Implementation
  ↓
Automated Quality Checks
  ↓
QA Validation
  ↓
Build / Package Verification
  ↓
Final Review
  ↓
Human Approval
  ↓
Commit + Push + Draft Change Request
  ↓
Merge / Release Pipeline
  ↓
Deployment
  ↓
Production Validation
  ↓
Metrics, Incidents & Continuous Improvement
```

The exact implementation of each stage may vary by project.

---

# 3. Core Principles

## 3.1 One Canonical Workflow

`pipeline/orchestration.md` is the single source of truth for feature development.

`pipeline/release-orchestration.md` is the single source of truth for release and deployment.

Other instructions must reference these files instead of duplicating the workflow.

---

## 3.2 Explicit State Transitions

Features must move through explicit states.

No agent, developer, or automation may silently skip required workflow stages.

Every transition must record:

* Previous state
* New state
* Responsible role
* Validation result
* Reason for transition
* Required next action

---

## 3.3 Shift-Left Quality

Quality must be validated as early as practical.

Responsibilities include:

| Stage          | Primary Quality Focus                    |
| -------------- | ---------------------------------------- |
| Requirements   | Completeness and clarity                 |
| Design         | Technical risks and constraints          |
| Implementation | Correctness and automated testing        |
| Automation     | Build, analysis, security, compatibility |
| QA             | Functional and behavioral validation     |
| Review         | Overall engineering quality              |
| Production     | Real-world behavior and reliability      |

The principle is:

> Detect problems at the earliest practical and lowest-cost stage.

---

## 3.4 Automation Before Repetition

Repeated and deterministic checks should be automated where practical.

Examples may include:

* Build or compilation validation
* Formatting
* Static analysis
* Automated tests
* Dependency checks
* Secret detection
* Security analysis
* Contract validation
* Architecture or dependency validation

Humans should focus on:

* Business trade-offs
* Design decisions
* Complex correctness
* Risk assessment
* Security acceptance
* Ambiguous requirements

---

## 3.5 Developer Experience

The SDLC should make the correct engineering path the easiest path.

Projects should provide:

* Predictable setup
* Discoverable commands
* Clear architecture guidance
* Fast feedback
* Useful error messages
* Local development guidance
* Test and verification instructions
* Troubleshooting guidance

---

## 3.6 Explicit Human Gates

AI agents and automation may analyze, design, implement, test, and review.

Human approval is required for decisions such as:

* Material business trade-offs
* Significant architectural decisions
* Security risk acceptance
* Destructive or irreversible changes
* Production-impacting decisions
* Final delivery actions when configured by the project

The default workflow creates a draft pull request or equivalent change request and does not merge automatically.

---

## 3.7 Traceable Artifacts

Important specifications, decisions, reviews, validations, incidents, and execution history must be traceable.

Prefer durable artifacts over conversational state.

---

## 3.8 Continuous Improvement

Feedback from:

* Build failures
* Test failures
* QA failures
* Code reviews
* Production incidents
* Deployment failures
* Developer friction
* Engineering metrics

must be used to improve the engineering system.

---

# 4. Required Repository Structure

The following structure is the default template.

Equivalent project-specific structures are allowed where necessary.

```text
AGENTS.md
CLAUDE.md

.github/
  workflows/
    ci.yml
    quality.yml
    security.yml
    deploy.yml

  instructions/
    review-checklist.instructions.md
    quality-gate.instructions.md
    security.instructions.md
    compliance.instructions.md
    workflow-agent-bootstrap.instructions.md

  prompts/
    start-feature.prompt.md
    review-feature.prompt.md
    create-pr.prompt.md
    pr-review.prompt.md

  copilot-instructions.md
  pull_request_template.md
  CODEOWNERS

.claude/
  agents/
    ba-agent.md
    architect-agent.md
    architecture-review-agent.md
    planner-agent.md
    developer-agent.md
    qa-agent.md
    review-agent.md
    bugfix-agent.md
    pr-review-agent.md
    devops-agent.md
    security-agent.md

  skills/
    build-code-skill/
      SKILL.md
    spec-generation-skill/
      SKILL.md
    migration-safety-skill/
      SKILL.md
    testing-strategy-skill/
      SKILL.md
    observability-skill/
      SKILL.md
    security-skill/
      SKILL.md
    developer-experience-skill/
      SKILL.md
    create-pr-skill/
      SKILL.md

pipeline/
  orchestration.md
  release-orchestration.md
  ExecutionLog.md

  features/
    FEATURE-<id>.md

  decisions/
    FEATURE-<id>-decisions.md

  metrics/
    engineering-metrics.md

  templates/
    feature-spec.template.md
    architecture.template.md
    implementation-plan.template.md
    review.template.md
    incident.template.md
    execution-log.template.md

docs/
  architecture/
  adr/
  api/
  reviews/
  runbooks/
  incidents/
  postmortems/

  getting-started.md
  local-development.md
  architecture-overview.md
  testing-strategy.md
  deployment.md
  troubleshooting.md

contracts/

tests/

.mcp.json
```

Directories such as `.github`, `.claude`, or `.mcp.json` are optional when the relevant tools are not used.

Equivalent structures should be used for other development environments.

---

# 5. Universal vs Project-Specific Rules

The workflow must distinguish between two layers.

## Universal Layer

The reusable SDLC template owns:

* Feature lifecycle
* State transitions
* Approval gates
* Agent responsibilities
* Artifact traceability
* Quality principles
* Failure loops
* Review requirements
* Delivery rules
* Continuous improvement

## Project-Specific Layer

The project defines:

* Language conventions
* Framework conventions
* Architecture style
* Dependency management
* Data access conventions
* UI conventions
* API conventions
* Testing tools
* Build commands
* Deployment commands
* Cloud services
* Security tooling
* Observability tooling

Example:

```text
Universal Rule:
"Validate architecture boundaries."

Project Rule:
"Use the project's approved architecture testing or dependency validation mechanism."
```

---

# 6. Repository Entry Point

## AGENTS.md

`AGENTS.md` is the repository entry point.

It must remain short and directional.

Before beginning work, an agent or developer must:

1. Read `AGENTS.md`.
2. Read `pipeline/orchestration.md`.
3. Identify the current feature.
4. Identify the current feature state.
5. Read the official feature specification.
6. Read relevant decisions and constraints.
7. Follow allowed state transitions.
8. Record required evidence.
9. Stop when human approval is required.

`AGENTS.md` must not duplicate the complete workflow.

---

# 7. Feature State Machine

Every feature must have a clearly identifiable state.

The default model is:

```text
INTAKE
  ↓
BRANCH_READY
  ↓
SPECIFIED
  ↓
READY_FOR_DEVELOPMENT
  ↓
DESIGNED
  ↓
ARCH_REVIEW_PASSED
  ↓
PLANNED
  ↓
IMPLEMENTED
  ↓
AUTOMATED_CHECKS_PASSED
  ↓
QA_PASSED
  ↓
BUILD_VERIFIED
  ↓
REVIEW_PASSED
  ↓
HUMAN_APPROVED
  ↓
DELIVERED
```

Additional states:

```text
BLOCKED_FOR_REWORK
BLOCKED_FOR_HUMAN
CANCELLED
```

Projects may rename states if the meaning and control points remain equivalent.

---

# 8. Feature Intake

Input may originate from:

* Issue tracker
* Product requirement
* Customer request
* Defect
* Technical improvement
* Operational problem
* Security finding
* Raw feature intent

The work must receive a unique identifier.

No implementation begins during intake.

---

# 9. Branch or Workspace Setup

Every feature must have an isolated unit of work.

This may be:

* A feature branch
* A workspace
* A change set
* Another project-approved source control mechanism

The project must prevent uncontrolled changes to protected or mainline code.

Default rule:

> No hidden or untraceable development work.

---

# 10. Feature Specification

The BA Agent converts the request into the official feature specification.

Each feature must have exactly one official specification.

The specification should include:

* Identifier
* Problem statement
* Business context
* Intended users or consumers
* Scope
* Out of scope
* Functional requirements
* Non-functional requirements
* Acceptance criteria
* Definition of Done
* Dependencies
* Assumptions
* Risks
* Open questions
* Operational considerations
* Testing considerations

---

# 11. Definition of Ready

Before implementation planning proceeds, the feature must be sufficiently ready.

Validate:

* Requirements are understandable
* Acceptance criteria exist
* Scope is known
* Dependencies are identified
* Important questions are resolved or explicitly accepted
* Testing approach is understood
* Technical impact is understood
* Required contracts or interfaces are available where applicable

Possible outcomes:

```text
PASS
FAIL
NEEDS_HUMAN_DECISION
```

---

# 12. Architecture and Design

The Architect Agent produces the required technical design.

Depending on the project, this may include:

* Component design
* Module design
* Service interactions
* Interface or API changes
* Data model changes
* Integration design
* Workflow or sequence design
* Error handling
* Security considerations
* Performance considerations
* Scalability considerations
* Migration strategy
* Rollback strategy
* Observability requirements

The template must not assume a particular architecture style.

For example, projects may use:

* Layered architecture
* Clean architecture
* Hexagonal architecture
* Modular monolith
* Microservices
* Event-driven architecture
* Serverless architecture
* Another documented model

---

# 13. Architecture Review

The Architecture Review Agent independently validates the design.

Review areas may include:

* Requirement coverage
* Simplicity
* Maintainability
* Security
* Reliability
* Performance
* Scalability
* Failure handling
* Compatibility
* Migration safety
* Operational impact
* Observability
* Project rule compliance

The review must not assume a particular programming language or architecture framework.

Possible outcomes:

```text
PASS
FAIL
NEEDS_HUMAN_DECISION
```

---

# 14. Implementation Planning

The Planner Agent converts approved design into an ordered implementation plan.

The plan should identify:

* Areas expected to change
* Components or modules affected
* Interfaces affected
* Data changes
* Compatibility concerns
* Tests required
* Dependencies
* Implementation sequence
* Rollback or mitigation considerations
* Deployment implications

The Planner must not silently introduce a new architecture.

---

# 15. Implementation

The Developer Agent implements the approved plan according to the project's stack-specific conventions.

The Developer must:

1. Read the canonical workflow.
2. Read the official feature specification.
3. Read applicable decisions.
4. Follow project-specific skills and conventions.
5. Implement approved scope.
6. Add appropriate automated tests.
7. Follow security requirements.
8. Add observability where required.
9. Record material deviations.

Stack-specific implementation details belong in:

```text
build-code-skill
testing-strategy-skill
security-skill
migration-safety-skill
```

or equivalent project-specific skills.

---

# 16. Automated Quality Checks

The project must define applicable automated quality checks.

Depending on the technology, these may include:

* Build or compilation
* Package validation
* Formatting
* Linting
* Static analysis
* Automated tests
* Dependency checks
* Secret detection
* Security analysis
* Contract validation
* Architecture fitness checks
* Infrastructure validation

The canonical workflow does not prescribe specific tools.

It only requires that applicable quality checks are defined and enforced.

---

# 17. Testing Strategy

Every project should define a testing strategy appropriate to its technology and risk profile.

Possible test categories include:

* Unit tests
* Integration tests
* Component tests
* Contract tests
* End-to-end tests
* Performance tests
* Security tests
* Architecture tests
* Infrastructure tests

Not every project requires every category.

The principle is:

> Use the lowest-cost validation that provides sufficient confidence.

Testing tools and commands must be project-specific.

---

# 18. Architecture Fitness Checks

Projects should automate architectural rules where practical.

Examples:

* Dependency boundaries
* Module isolation
* Forbidden dependencies
* Circular dependency prevention
* Interface compatibility
* Infrastructure policy validation

The implementation mechanism is stack-specific.

The canonical rule is:

> Important architecture constraints should be automatically validated where practical.

---

# 19. Contract and Compatibility Validation

Projects with independent consumers, services, integrations, events, or public interfaces should evaluate compatibility validation.

Contracts may include:

* API specifications
* Event schemas
* Interface definitions
* Message contracts
* Protocol definitions
* Data schemas

The specific contract format and tooling are project-specific.

---

# 20. QA Validation

The QA Agent validates the implementation against:

* Official feature specification
* Acceptance criteria
* Definition of Done
* Expected behavior
* Failure scenarios
* Edge cases
* Regression risks

Possible outcomes:

```text
PASS
FAIL
NEEDS_HUMAN_DECISION
```

QA failure must explicitly route work back to the appropriate responsible role.

---

# 21. Build and Package Verification

The project must validate that the deliverable can be produced.

Depending on the project, this may include:

* Compilation
* Packaging
* Artifact generation
* Container creation
* Infrastructure validation
* Deployment package generation
* Dependency restoration

The canonical workflow requires verification but does not prescribe commands.

Commands belong in project-specific skills.

---

# 22. Final Review Gate

The Review Agent performs a structured quality review.

Review areas include:

* Acceptance criteria
* Scope alignment
* Code or implementation quality
* Design alignment
* Security
* Testing adequacy
* Project conventions
* Compatibility
* Migration safety
* Dependency impact
* Observability
* Documentation

Each review item must explicitly be:

```text
Pass
Fail
Needs Human Decision
```

---

# 23. Human Approval

Human approval is a mandatory workflow gate before final delivery unless the project explicitly defines a different approved governance model.

Human decisions may include:

* Approve
* Reject
* Request changes
* Request clarification
* Escalate a decision

Approval must be recorded.

---

# 24. Delivery

Only after required approval may the workflow perform final source control delivery actions.

The default process is:

1. Verify current work state.
2. Verify required checks.
3. Commit approved changes.
4. Push or publish the change.
5. Create a draft pull request or equivalent review request.
6. Record the delivery reference.

The default workflow must not:

* Modify protected mainline code directly
* Commit secrets
* Bypass required checks
* Merge automatically

Projects may explicitly override the change-management mechanism.

---

# 25. Release and Deployment Workflow

Feature development and release management are separate workflows.

Release guidance belongs in:

```text
pipeline/release-orchestration.md
```

The release workflow may include:

```text
Approved Change
  ↓
Merge or Integrate
  ↓
Continuous Integration
  ↓
Environment Deployment
  ↓
Automated Validation
  ↓
Acceptance Validation
  ↓
Production Deployment
  ↓
Production Validation
```

Deployment mechanisms are project-specific.

---

# 26. Safe Release Strategies

Projects should evaluate appropriate release strategies based on risk.

Possible approaches include:

* Progressive rollout
* Canary release
* Blue/green deployment
* Rolling deployment
* Feature flags
* Staged environment validation
* Controlled activation

The canonical workflow does not require a particular strategy.

It requires that higher-risk changes have an appropriate mitigation or rollback strategy.

---

# 27. Observability

Significant features should answer:

> How will we know whether this works correctly after release?

Projects may use:

* Logs
* Metrics
* Traces
* Health checks
* Error monitoring
* Dashboards
* Alerts

The specific observability platform is project-specific.

The requirement is not.

---

# 28. Production Validation

Deployment does not automatically mean success.

Where applicable, validate:

* System health
* Error behavior
* Performance
* Feature-specific behavior
* Operational metrics
* Important business outcomes

Production validation failures must have a defined mitigation or rollback path.

---

# 29. Incident and Defect Management

Production problems should feed back into the engineering lifecycle.

Default flow:

```text
Incident
  ↓
Triage
  ↓
Investigation
  ↓
Root Cause Analysis
  ↓
Fix
  ↓
Regression Protection
  ↓
Release
  ↓
Postmortem
  ↓
Preventive Improvement
```

The goal is learning and prevention, not blame.

---

# 30. Developer Experience

Projects should provide sufficient guidance for productive development.

At minimum, where applicable:

```text
Getting Started
Local Development
Architecture Overview
Testing
Troubleshooting
```

The project should provide discoverable ways to:

```text
setup
build
run
test
verify
```

The actual commands are stack-specific.

---

# 31. Engineering Metrics

Measure the engineering system rather than individual developer activity.

Useful signals may include:

## Flow

* Lead time
* Cycle time
* Review turnaround
* Blocked time
* Deployment frequency

## Quality

* Change failure rate
* Escaped defects
* Production incidents
* Build failure trends
* Test instability

## Developer Experience

* Setup time
* Build duration
* CI duration
* Feedback turnaround
* Developer-reported friction

Metrics should improve the system, not rank individuals.

---

# 32. Security

Security must be integrated throughout the lifecycle.

Applicable controls may include:

* Threat modeling
* Secure design review
* Static analysis
* Dependency analysis
* Secret detection
* Infrastructure security validation
* Container or artifact scanning
* Dynamic testing

The exact controls depend on the project and risk profile.

The canonical requirement is:

> Security controls must be selected deliberately rather than added accidentally or only after an incident.

---

# 33. AI-Assisted Development

AI-generated changes must meet the same quality expectations as other changes.

AI-generated work must:

* Follow project conventions
* Pass required validation
* Include appropriate tests
* Respect architecture boundaries
* Avoid introducing secrets
* Avoid introducing unapproved dependencies
* Remain traceable through normal review

AI must not silently:

* Override human gates
* Accept significant risks
* Make irreversible production changes
* Merge changes automatically

---

# 34. AI Application Quality

Projects containing AI capabilities should define additional evaluation appropriate to the system.

Possible areas include:

* Task success
* Accuracy
* Safety
* Reliability
* Latency
* Cost
* Regression evaluation
* Human evaluation
* Production monitoring

AI-specific evaluation methods are project-specific.

---

# 35. Required Agent Definitions

Agent definitions and examples have been moved to `docs/AGENTS-templates.md` to keep this file concise. That file contains a ready-to-copy agent template and several example agent definitions (BA, Architect, Developer, QA, Planner, Review).

Please author new agents using the template in `docs/AGENTS-templates.md` and add agent files under `.claude/agents/` when appropriate.

---

# 36. Required Skills

Reusable, stack-specific skills and their templates live in `docs/SKILLS-templates.md` and should be implemented under `.claude/skills/` or an equivalent project directory.

---

# 37. Repository Conventions

The template enforces universal principles rather than technology-specific coding rules.

## Universal Rules

* Changes must be traceable.
* Protected or mainline code must not be modified outside approved workflow.
* Every feature has one official specification.
* Important decisions must be recorded.
* Required validation must not be silently skipped.
* Secrets must never be committed.
* Final delivery requires the configured approval gate.
* Automatic merge is disabled by default.

## Project-Specific Rules

The project must define:

* Code organization
* Dependency conventions
* Architecture boundaries
* Data access conventions
* Interface conventions
* UI conventions
* Testing conventions
* Build conventions
* Deployment conventions

These rules belong in project-level skills or instruction files.

---

# 38. Execution Logging

Maintain:

```text
pipeline/ExecutionLog.md
```

Record:

* Feature identifier
* Previous state
* Current state
* Responsible role
* Relevant branch or workspace
* Artifacts created or changed
* Validation results
* Failure reason
* Required next action
* Human decisions
* Delivery references

The log should answer:

> What happened, who performed it, what evidence exists, and why is the feature in its current state?

---

# 39. Review Checklist

Every project must maintain a structured review checklist.

The baseline checklist includes:

* [ ] Acceptance criteria verified
* [ ] Official feature specification followed
* [ ] Definition of Done satisfied
* [ ] Scope controlled
* [ ] Implementation quality acceptable
* [ ] Design alignment verified
* [ ] Appropriate tests added
* [ ] Required verification passed
* [ ] Security controls checked
* [ ] No secrets committed
* [ ] Dependencies reviewed where applicable
* [ ] Project conventions followed
* [ ] Compatibility reviewed where applicable
* [ ] Migration safety reviewed where applicable
* [ ] Observability reviewed where applicable
* [ ] Documentation updated where required
* [ ] Human decisions identified

Every item must have one explicit result:

```text
Pass
Fail
Needs Human Decision
```

---

# 40. Continuous Improvement Loop

The SDLC is a feedback system.

```text
Development
  ↓
Validation Feedback
  ↓
Review
  ↓
Release
  ↓
Production Signals
  ↓
Incidents / Defects / Developer Feedback
  ↓
Bottleneck and Root Cause Analysis
  ↓
Improve:
- Workflow
- Automation
- Architecture
- Testing
- Documentation
- Developer Experience
- Tooling
  ↓
Improved Engineering System
```

The goal is not more process.

The goal is:

> Faster feedback, lower friction, safer changes, and increasing engineering confidence.

---

# 41. Success Criteria

The generated workflow is successful when:

* [ ] The workflow is independent of programming language and framework.
* [ ] Stack-specific implementation details are separated from the canonical SDLC.
* [ ] `AGENTS.md` directs agents to the canonical workflow.
* [ ] Feature development has one canonical orchestrator.
* [ ] Release and deployment have a defined lifecycle.
* [ ] Features use explicit states and transitions.
* [ ] Definition of Ready exists.
* [ ] Every feature has one official specification.
* [ ] Design is reviewed before implementation.
* [ ] Applicable automated quality checks are defined.
* [ ] Testing strategy is project appropriate.
* [ ] Architecture constraints are automated where practical.
* [ ] QA validates requirements and Definition of Done.
* [ ] Verification failures explicitly route to rework.
* [ ] Review evidence is retained.
* [ ] Execution history is recorded.
* [ ] Required human approval gates exist.
* [ ] Default delivery creates a draft review request.
* [ ] Automatic merge is disabled by default.
* [ ] Production validation is considered where applicable.
* [ ] Incidents and feedback improve the engineering system.
* [ ] Developer experience is treated as an engineering concern.
* [ ] Security is integrated throughout the lifecycle.
* [ ] AI-generated changes follow the same quality standards.
* [ ] Engineering metrics focus on system improvement.

---

# 42. Canonical Lifecycle Summary

```text
              UNIVERSAL SDLC WORKFLOW
────────────────────────────────────────────────

Feature / Request
      ↓
Isolated Work Setup
      ↓
BA / Specification
      ↓
Definition of Ready
      ↓
Architecture & Design
      ↓
Architecture Review
      ↓
Implementation Planning
      ↓
Development
      ↓
Automated Quality Checks
      ↓
QA Validation
      ↓
Build / Package Verification
      ↓
Final Review
      ↓
Human Approval
      ↓
Commit + Push
      ↓
Draft PR / Change Request

────────────────────────────────────────────────
              RELEASE WORKFLOW
────────────────────────────────────────────────

Integration
      ↓
CI/CD
      ↓
Environment Deployment
      ↓
Validation
      ↓
Safe Rollout Strategy
      ↓
Production Validation
      ↓
Metrics + Feedback
      ↓
Continuous Improvement
```

# Final Principle

This template defines **how software work should flow**, not **how a particular technology should be coded**.

Therefore:

> **The SDLC is universal. The workflow is reusable. The quality principles are consistent. The implementation details belong to the individual project and technology stack.**

The system should continuously optimize for:

**Fast feedback + clear ownership + small safe changes + automation + explicit decisions + excellent developer experience + production learning.**
