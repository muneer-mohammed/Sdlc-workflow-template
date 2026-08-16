# AGENTS & Agent Templates

This file contains copy-pasteable agent templates and examples to help authors create `.claude/agents/<agent>.md` files.

## Agent Template

### Agent: <agent-name>

Purpose
- One-line summary of ownership (e.g., "Produces and validates architecture design for features").

Input
- Required artifacts/state: `pipeline/features/FEATURE-<id>.md`, current feature state (e.g., SPECIFIED), relevant decisions.

Output
- Artifacts produced: `pipeline/decisions/FEATURE-<id>-decisions.md`, ADR entry, diagrams.
- Allowed next state(s): DESIGNED, ARCH_REVIEW_PASSED, or NEEDS_HUMAN_DECISION.

Workflow Steps
1. Read official feature spec and decisions.
2. Produce component-level design and list compatibility/migration concerns.
3. Document outputs in `pipeline/decisions/FEATURE-<id>-decisions.md`.
4. Run architecture-fitness checks (if available) and include results.
5. Submit for Architecture Review.

Validation Criteria
- Acceptance criteria mapped to implementation components.
- Migration and rollback strategies documented.
- Observability and security considerations present.

Known Constraints
- Technology-agnostic: avoid implementation-level instructions.
- Must not modify protected mainline code.

Required Artifacts
- `pipeline/decisions/FEATURE-<id>-decisions.md`
- ADRs for cross-cutting decisions
- Any diagrams or evidence used in review

Allowed State Transitions
- From: SPECIFIED, READY_FOR_DEVELOPMENT
- To: DESIGNED, ARCH_REVIEW_PASSED, NEEDS_HUMAN_DECISION

Escalation Rules
- If risk (security/performance) > medium, escalate to `security-agent`/`devops-agent` and mark `NEEDS_HUMAN_DECISION`.

## Example: ba-agent

### Agent: ba-agent

Purpose
- Produce the official feature specification from intake artifacts.

Input
- Issue or request
- Current feature state: INTAKE

Output
- `pipeline/features/FEATURE-<id>.md` (official spec)
- Allowed next states: SPECIFIED or NEEDS_HUMAN_DECISION

Workflow Steps
1. Gather inputs and stakeholder context.
2. Draft the feature specification using `pipeline/templates/feature-spec.template.md`.
3. Validate acceptance criteria and edge cases.
4. Mark Definition of Ready or escalate.

Validation Criteria
- Acceptance criteria exist and are testable.
- Scope is clear and dependencies identified.

Escalation
- If requirements are ambiguous, mark NEEDS_HUMAN_DECISION and request clarification.
