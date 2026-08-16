# SKILLS Template and Examples

This file provides a template for authoring reusable, stack-specific skills under `.claude/skills/`.

## Skill Template

### Skill: <skill-name>

Purpose
- One-line summary of what the skill automates or documents (e.g., "Build and package verification for Java services").

Input
- Required files, environment, or state (e.g., `pom.xml`, Dockerfile, `JAVA_HOME`).

Output
- Expected artifacts or side-effects (e.g., built JAR, container image, verification report).

Commands / Implementation
- Copy the project-specific commands and example invocations.

Validation
- What checks must pass (e.g., `mvn -DskipTests=false verify` returns 0, container image builds successfully).

Observability
- Any logs, artifacts, or test results to include in `pipeline/ExecutionLog.md`.

Notes
- Keep the skill minimal and focused on automation or reproducible guidance.

## Example: build-code-skill

Purpose
- Build and produce a release artifact for the project.

Input
- Source code, dependencies, build config (e.g., `package.json`, `pom.xml`).

Output
- Build artifact (e.g., `dist/`, `target/`, container image), success/failure exit code.

Commands
- `npm ci && npm run build`
- or `mvn -B -DskipTests verify`

Validation
- Build completes with exit code 0.
- Expected artifacts exist.
