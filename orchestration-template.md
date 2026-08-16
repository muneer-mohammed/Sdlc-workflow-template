# Workflow & Agent Orchestration — Reusable SDLC Template

**applyTo:** `**/*`

## Purpose

This instruction file defines the canonical Software Development Lifecycle (SDLC) workflow for the repository.

It governs how work moves from:

Request → Specification → Design → Planning → Implementation → Validation → Review → Human Approval → Draft Pull Request / Change Request

The workflow is designed to improve:

- Software quality
- Developer productivity
- Delivery confidence
- Maintainability
- Security
- Reliability
- Traceability
- Operational readiness
- AI-assisted engineering efficiency

This file is the **single source of truth for the software delivery workflow**.

Other instructions, agents, skills, prompts, and project-specific conventions must reference this workflow rather than duplicate it.

---

# 1. Scope

This workflow applies to:

- New features
- Enhancements
- Defects
- Refactoring
- Technical debt
- API or contract changes
- Persistent state changes
- Infrastructure changes
- Security fixes
- Performance improvements

The workflow is intentionally **technology-stack agnostic**.

It does not assume:

- Programming language
- Framework
- Database
- Cloud provider
- Architecture style
- Source control provider
- CI/CD platform
- Issue tracker
- Testing framework
- AI model provider

Project-specific implementation details must be defined separately through repository conventions, skills, instructions, or approved project documentation.

---

# 2. Core Principles

## 2.1 Minimum Sufficient Process

Use enough process to provide confidence, traceability, and safety.

Do not add process steps that do not provide meaningful value for the risk or complexity of the change.

The workflow may scale according to:

- Change size
- Risk
- Security impact
- Architectural impact
- Consumer impact
- Production impact

However, required quality and approval gates must not be silently bypassed.

## 2.2 Minimum Sufficient Context

Use the minimum context required to perform the task correctly.

Do not automatically load:

- The entire repository
- All historical conversations
- All documentation
- All previous features
- All architecture decisions

Start with the current task and progressively retrieve additional context only when required.

## 2.3 Explicit State

The current state of work must be clear.

A feature must not silently move from one stage to another.

Each meaningful transition should identify:

- Previous state
- New state
- Responsible role
- Validation result
- Reason
- Required next action

## 2.4 Evidence Over Assumption

Do not assume that:

- A build passed
- Tests passed
- A ticket was checked
- A PR was created
- An external system was queried
- A deployment succeeded

Use available evidence.

If evidence is unavailable, state the limitation explicitly.

## 2.5 Human Decisions Are Explicit

AI agents may assist with analysis, implementation, testing, and review.

AI agents must not silently:

- Override human decisions
- Accept significant security risks
- Resolve material requirement conflicts
- Change protected delivery policies
- Bypass required approval gates
- Automatically merge changes unless explicitly authorized

When a material decision cannot be safely made, transition to:

`BLOCKED_FOR_HUMAN`

---

# 3. AI Context, Memory, Token, and MCP Management

AI-assisted development must optimize for both **engineering quality and efficient use of AI resources**.

The objective is:

> Use the minimum sufficient context, the appropriate memory layer, the lowest-cost capable model, and approved tools or MCP integrations where authoritative information is required.

## 3.1 Progressive Context Discovery

Context must be loaded progressively:

1. Understand the current task.
2. Read the current feature or requirement.
3. Identify affected areas.
4. Load relevant decisions.
5. Inspect relevant code or artifacts.
6. Retrieve additional context only if needed.

Recommended context priority:

1. Current task and acceptance criteria
2. Current feature specification
3. Relevant decisions and constraints
4. Affected code, components, or artifacts
5. Applicable repository conventions
6. Historical context only when necessary

Do not repeatedly load the same large context when a concise artifact or summary is sufficient.

## 3.2 Appropriate Memory Usage

| Information Type | Preferred Location |
|---|---|
| Current task details | Working/session context |
| Feature requirements | Official feature specification |
| Feature-specific decisions | Feature decision artifact |
| Architecture decisions | ADR or architecture documentation |
| Repository-wide rules | Canonical repository instructions |
| Temporary debugging information | Working/session context |
| Stable reusable preferences | Appropriate LLM persistent memory where available |
| External system information | Retrieve through approved tools/MCP when needed |

Rules:

1. Do not use persistent LLM memory as a replacement for version-controlled repository knowledge.
2. Do not store temporary or short-lived information as durable project knowledge.
3. Do not duplicate information across multiple memory layers without a clear reason.
4. The repository remains the source of truth for project-specific engineering decisions.

## 3.3 Context Summarization and Handoffs

When work passes between agents, do not transfer the entire conversation or execution history unless necessary.

Create a compact handoff containing:

- Feature / Work Item
- Current State
- Completed Work
- Key Decisions
- Affected Files / Components
- Validation Evidence
- Known Issues
- Open Questions
- Next Responsible Role
- Recommended Next Action

The receiving agent should retrieve source artifacts when necessary rather than relying on a large copied conversation.

Critical information must not be lost through summarization, including:

- Acceptance criteria
- Security decisions
- Human decisions
- Critical constraints
- Known failures
- Compatibility requirements

## 3.4 Token Efficiency Rules

Tokens must be treated as an engineering resource.

The goal is:

> Use the minimum sufficient context and output required to achieve the required confidence and quality.

Agents should:

- Read targeted files rather than entire directories.
- Retrieve relevant sections of large files when supported.
- Avoid repeating already established information.
- Reuse canonical artifacts.
- Use concise structured outputs where appropriate.
- Avoid unnecessary boilerplate.
- Avoid duplicate analysis.
- Stop exploration once sufficient evidence exists.
- Summarize completed work for handoff.

Agents should not:

- Dump the entire repository into context.
- Repeatedly read unchanged large documents.
- Generate duplicate documentation.
- Ask multiple agents to independently perform identical work without justification.
- Continue exploratory analysis after sufficient evidence has been obtained.

## 3.5 Model Selection

Use the **lowest-cost model capable of completing the task with the required level of quality, reliability, and safety**.

Consider:

- Complexity
- Reasoning requirements
- Risk
- Security sensitivity
- Production impact
- Cost
- Latency
- Required output quality

Guidance:

### Low complexity

Examples:

- Metadata extraction
- File classification
- Formatting
- Checklist validation
- Simple transformations

Use an efficient lower-cost model where appropriate.

### Medium complexity

Examples:

- Feature analysis
- Test generation
- Standard implementation
- Implementation planning
- Code review of limited scope

Use a capable general-purpose model.

### High complexity or high risk

Examples:

- Architecture design
- Security-sensitive changes
- Complex debugging
- Multi-system reasoning
- High-impact production decisions

Use a higher-capability model and increase validation.

Model capability must be selected according to the task, not by default preference.

## 3.6 Tool and MCP Readiness Check

Before manually reconstructing information from an external system, determine whether an appropriate approved tool, connector, API integration, or MCP server is available.

Potential external capabilities include:

- Issue tracking
- Source control
- Pull requests
- CI/CD
- Documentation
- Monitoring
- Logs
- Databases
- Cloud platforms
- Security scanning
- Feature flags
- Design systems

At workflow initialization or when a stage requires external information:

1. Identify the required external capability.
2. Check available tool or MCP integrations.
3. Use targeted retrieval when an appropriate integration is available.
4. If unavailable, determine the fallback.
5. Configure, request human action, use manual input, or record the limitation as appropriate.

## 3.7 MCP Configuration Rules

Agents must not assume an MCP or tool integration exists.

Before requiring information from an external system:

1. Identify the required external system.
2. Check whether an approved integration is configured.
3. Verify that required permissions are available.
4. Use the integration when appropriate.
5. If unavailable, determine whether:
   - The integration is optional.
   - Manual input is sufficient.
   - A fallback mechanism exists.
   - Configuration is required.
   - Human intervention is required.

Examples:

- Ticket requirements → Check issue tracker integration.
- PR creation → Check source control integration.
- Build status → Check CI/CD integration.
- Production investigation → Check monitoring/logging integration.
- Architecture references → Check documentation integration.

The workflow must never claim that an external system was queried when the required integration was unavailable.

## 3.8 Tool-First Retrieval

When authoritative information exists in an approved external system, prefer targeted retrieval over manual reconstruction.

Examples:

- Requirement or ticket → Retrieve from issue tracking system.
- PR status → Retrieve from source control system.
- Build result → Retrieve from CI/CD system.
- Production errors → Retrieve from monitoring/logging system.

External information does not automatically override approved repository decisions.

Conflicts between sources must be explicitly identified.

## 3.9 Execution Budget and Escalation

For complex or multi-agent workflows, execution should have reasonable limits.

Possible limits include:

- Maximum context size
- Maximum retries
- Maximum rework loops
- Maximum parallel agents
- Maximum model usage cost
- Maximum execution time

If a meaningful budget is exceeded:

1. Stop.
2. Summarize the current state.
3. Record evidence.
4. Identify the remaining problem.
5. Escalate for human decision.

Quality, security, and approval requirements must never be bypassed solely to reduce cost or token usage.

---

# 4. Mandatory Workflow Rules

1. Every feature or material change must have a traceable requirement or intent.
2. No implementation begins without sufficient requirements.
3. Every feature has exactly one official feature specification.
4. Material assumptions and decisions must be recorded.
5. Work must occur in an isolated branch or approved equivalent workspace.
6. No hidden branchless implementation work.
7. Architecture-impacting changes require design consideration.
8. Applicable automated validation must be run.
9. QA and review failures must explicitly route to rework.
10. Human approval is required before final delivery steps.
11. Final delivery creates a draft pull request or equivalent change request.
12. Changes must not automatically merge unless explicitly authorized by project policy.
13. Secrets must never be committed.
14. Material deviations from approved design must be recorded and reviewed.
15. External information must be retrieved through appropriate configured integrations when available.
16. Workflow execution must remain traceable.

---

# 5. Canonical Feature Workflow

The default workflow is:

1. Feature Request / Intent / Ticket
2. Branch or Isolated Workspace Setup
3. Tool and MCP Readiness Check
4. Requirements Analysis
5. Feature Specification
6. Definition of Ready
7. Architecture and Design
8. Architecture Review
9. Implementation Planning
10. Development
11. Automated Quality Validation
12. QA Validation
13. Build / Package Verification
14. Final Review
15. Human Approval
16. Commit + Push
17. Draft Pull Request / Change Request

Stages may be proportionate to change complexity, but required gates must remain explicit.

---

# 6. Feature State Machine

Use the following default states:

- INTAKE
- BRANCH_READY
- SPECIFIED
- READY_FOR_DEVELOPMENT
- DESIGNED
- ARCH_REVIEW_PASSED
- PLANNED
- IMPLEMENTED
- AUTOMATED_CHECKS_PASSED
- QA_PASSED
- BUILD_VERIFIED
- REVIEW_PASSED
- HUMAN_APPROVED
- DELIVERED

Additional states:

- BLOCKED_FOR_REWORK
- BLOCKED_FOR_HUMAN
- CANCELLED

No state transition should occur silently.

---

# 7. Branch and Workspace Setup

Before implementation:

1. Identify the work item.
2. Confirm the intended branch or isolated workspace.
3. Ensure work is traceable to the feature.
4. Follow repository branch naming conventions.
5. Do not directly modify protected mainline branches unless explicitly authorized.

The workflow must not assume a specific Git provider.

---

# 8. Requirements and Feature Specification

Every feature must have exactly one official specification.

The specification should include:

- Feature identifier
- Problem or objective
- Scope
- Out of scope
- Functional requirements
- Acceptance criteria
- Non-functional requirements where applicable
- Assumptions
- Constraints
- Dependencies
- Open questions
- Definition of Done

The specification is the primary source for validating feature completion.

---

# 9. Definition of Ready

Implementation must not begin until the work is sufficiently understood.

At minimum, verify:

- The problem is clear.
- Scope is sufficiently defined.
- Acceptance criteria exist.
- Dependencies are identified.
- Major open questions are resolved or explicitly accepted.
- Required external systems or integrations are identified.
- Required approvals are known.

Possible results:

- READY_FOR_DEVELOPMENT
- BLOCKED_FOR_REWORK
- BLOCKED_FOR_HUMAN

---

# 10. Architecture and Design

Architecture or design work is required when appropriate to the impact of the change.

Consider:

- Component boundaries
- Data and state impact
- API or contract changes
- Integration impact
- Security
- Performance
- Scalability
- Reliability
- Failure handling
- Compatibility
- Operational requirements
- Rollback or mitigation

Do not create unnecessary design documentation for trivial changes.

The design artifact should be proportional to complexity.

---

# 11. Architecture Review

Architecture review validates:

- Requirement coverage
- Design completeness
- Maintainability
- Compatibility
- Security considerations
- Operational readiness
- Significant risks
- Alignment with existing architecture

Possible results:

- PASS
- FAIL
- NEEDS_HUMAN_DECISION

A failure must route back to design.

---

# 12. Implementation Planning

The implementation plan should identify:

- Steps required
- Affected components
- Dependencies
- Data or contract changes
- Tests required
- Validation required
- Deployment considerations
- Rollback or mitigation where applicable

The planning stage must not silently introduce material architectural changes.

Material deviations must return to the appropriate design stage.

---

# 13. Development

Development must:

- Follow repository conventions.
- Follow approved specifications and decisions.
- Minimize unnecessary scope expansion.
- Add or update appropriate tests.
- Preserve compatibility where required.
- Avoid unapproved dependencies.
- Record material deviations.

The developer must stop and escalate when:

- Requirements materially conflict.
- Architecture assumptions become invalid.
- Security risks are discovered.
- Required information cannot be obtained.
- A significant design change becomes necessary.

---

# 14. Automated Quality Validation

Run all applicable repository-defined checks.

Possible checks include:

- Build or compilation
- Formatting
- Linting
- Static analysis
- Automated tests
- Dependency validation
- Secret detection
- Security scanning
- Contract validation
- Architecture validation
- Infrastructure validation

The specific commands are project-specific.

The workflow rule is:

> Applicable validation must be explicit and must not be silently skipped.

---

# 15. QA Validation

QA must validate the feature against:

- Acceptance criteria
- Definition of Done
- Happy paths
- Failure paths
- Edge cases
- Regression risks

QA should use the lowest-cost validation method that provides sufficient confidence.

Possible methods include:

- Automated tests
- Integration validation
- Contract validation
- End-to-end validation
- Manual exploratory testing

Failure routes explicitly to rework.

---

# 16. Build and Package Verification

Before review, verify that applicable build or packaging requirements pass.

The specific commands are defined by the repository.

A successful implementation without successful applicable build verification is not ready for delivery.

---

# 17. Final Review

The final review must use a structured checklist.

At minimum review:

- Acceptance criteria
- Specification alignment
- Scope control
- Implementation quality
- Design alignment
- Testing
- Security
- Secrets
- Dependencies
- Compatibility
- Persistent state or migration safety
- API/event/contract impact
- Observability
- Documentation
- Repository rules
- Known risks

Every checklist item must have one status:

- PASS
- FAIL
- NEEDS_HUMAN_DECISION

---

# 18. Human Approval Gate

Human approval is required before final delivery steps.

The approval should confirm:

- Required validation is complete.
- Known risks are understood.
- Required decisions have been made.
- Delivery is authorized.

If approval is not available:

`BLOCKED_FOR_HUMAN`

Do not silently continue.

---

# 19. Commit, Push, and Draft PR

After approval:

1. Commit changes according to repository conventions.
2. Push the feature branch.
3. Create a draft pull request or equivalent change request.
4. Include relevant validation evidence.
5. Link the feature specification or work item where applicable.

Default rule:

> Final delivery creates a draft PR or equivalent. It does not automatically merge.

---

# 20. Failure and Rework Loops

Failures must always result in explicit routing:

- Specification Failure → BA / Requirements
- Definition of Ready Failure → BA / Architect / Human
- Architecture Review Failure → Architecture
- Planning Design Gap → Architecture
- Implementation Failure → Development
- Automated Validation Failure → Development
- QA Failure → Development
- Build Failure → Development
- Review Failure → Development
- Security Decision Required → Human / Appropriate Security Review
- Execution Budget Exceeded → BLOCKED_FOR_HUMAN

No failed stage may silently advance.

---

# 21. Testing Strategy

Use the lowest-cost testing approach that provides sufficient confidence.

Applicable testing may include:

- Unit
- Integration
- Component
- Contract
- End-to-End
- Performance
- Security
- Architecture
- Infrastructure

Not every change requires every test type.

Testing depth should consider:

- Risk
- Complexity
- Blast radius
- Consumer impact
- Production criticality

---

# 22. Compatibility and Migration Safety

When changing persistent state, APIs, events, schemas, files, or other consumer-facing contracts, evaluate:

- Backward compatibility
- Consumer impact
- Versioning
- Migration strategy
- Data integrity
- Rollback
- Partial failure
- Deployment ordering

Migration safety is not limited to relational databases.

---

# 23. Security and Secrets

All changes must follow applicable security requirements.

At minimum:

- Secrets must never be committed.
- Sensitive information must not be unnecessarily exposed.
- Dependencies should be evaluated where applicable.
- Authentication and authorization impact should be considered.
- Material security risks require explicit review.
- Security risk acceptance requires human authorization.

Security controls should be proportional to the risk.

---

# 24. Observability and Operational Readiness

For production-impacting changes, consider:

- Logging
- Metrics
- Tracing
- Health checks
- Error monitoring
- Dashboards
- Alerts
- Runbooks

Ask:

> How will the team know whether this feature is functioning correctly after release?

Observability requirements should be proportional to operational impact.

---

# 25. Execution Logging and Evidence

Maintain:

`pipeline/ExecutionLog.md`

For each significant workflow transition, record:

- Feature identifier
- Previous state
- Current state
- Responsible role
- Relevant artifacts
- Validation performed
- Result
- Known failures
- Human decisions
- Next action

The execution history should answer:

> What happened, what evidence exists, why is the work in its current state, and what must happen next?

Do not create excessive logs for trivial internal actions.

---

# 26. AI-Assisted Development Rules

AI-generated work must follow the same standards as human-generated work.

AI-generated changes must:

- Follow repository conventions.
- Respect approved architecture.
- Pass applicable validation.
- Include appropriate tests.
- Respect security rules.
- Avoid secrets.
- Avoid unnecessary dependencies.
- Remain traceable.

AI must not silently:

- Override approved requirements.
- Override architecture decisions.
- Bypass quality gates.
- Bypass human approval.
- Perform destructive production actions without explicit authorization.
- Merge changes automatically unless explicitly authorized.

---

# 27. Definition of Done

A feature is complete only when applicable requirements are satisfied.

Default Definition of Done:

- [ ] Official feature specification exists.
- [ ] Acceptance criteria are satisfied.
- [ ] Required design decisions are documented.
- [ ] Required implementation is complete.
- [ ] Appropriate tests are added or updated.
- [ ] Applicable automated checks pass.
- [ ] QA validation passes.
- [ ] Applicable build/package verification passes.
- [ ] Final review passes.
- [ ] Security and compatibility concerns are addressed.
- [ ] Operational requirements are addressed where applicable.
- [ ] Material deviations are documented.
- [ ] Required human approval is obtained.
- [ ] Changes are committed and pushed.
- [ ] Draft PR or equivalent change request is created.

---

# 28. Continuous Improvement

The workflow is a feedback system:

Development
→ Validation Feedback
→ Review
→ Release
→ Production Signals
→ Defects / Incidents / Developer Feedback
→ Root Cause or Bottleneck Analysis
→ Improve Workflow, Automation, Testing, Architecture, Documentation, Developer Experience, Tooling, AI Context Strategy, and MCP Integrations
→ Improved Engineering System

The objective is not to add process.

The objective is:

> Faster feedback, lower friction, safer changes, better use of engineering and AI resources, and increasing confidence in delivery.

---

# 29. Recommended Repository Structure

```text
AGENTS.md
CLAUDE.md

pipeline/
  orchestration.md
  features/
  decisions/
  templates/
  ExecutionLog.md

docs/
  architecture/
  adr/
  reviews/
  runbooks/
  incidents/
  postmortems/
```

The repository may extend this structure, but should avoid creating multiple competing workflow documents.

---

# 30. Entry Point Guidance

The repository entry instruction should remain short and directional.

Example:

```markdown
# Repository Agent Instructions

Read this file first.

Before starting material work:

1. Read `pipeline/orchestration.md`.
2. Identify the current feature or work item.
3. Read the official feature specification.
4. Read relevant decisions and constraints.
5. Check applicable tools or MCP integrations when external information is required.
6. Load only the minimum context necessary for the current task.
7. Follow the workflow state and quality gates.
8. Record material execution evidence.
9. Stop at required human approval gates.

Do not duplicate the complete SDLC workflow here.

The canonical workflow is:

`pipeline/orchestration.md`
```

---

## Core Rule

> **Use the minimum sufficient context, appropriate memory, the lowest-cost capable model, targeted tool or MCP retrieval, explicit quality gates, and traceable artifacts to deliver software safely and efficiently.**
