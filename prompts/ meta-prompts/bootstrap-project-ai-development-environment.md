# Prepare AI Development Environment Prompt

I opened this repository with OpenCode. I want you to prepare a project-specific AI-assisted development environment for this repository by creating or updating agent instructions, project standards, skill files, and focused documentation references.

The goal is to help AI agents working in this repository understand the project correctly and make consistent, safe, testable, and maintainable changes without relying on assumptions.

---

## Critical Rule: Do Not Assume

Do not assume any tool, command, framework, architecture, or workflow that is not supported by evidence in the repository.

If you are not certain about something:

- mark it as `unknown`, or
- ask the user before treating it as a project standard.

Never guess the following:

- build commands
- test commands
- lint or format commands
- runtime or framework
- deployment process
- database technology
- authentication or authorization approach
- CI/CD process

---

## Required Analysis Phase

Before creating or editing any files, analyze the repository.

Inspect these sources in priority order:

1. `README.md`
2. Existing agent instructions such as:
   - `AGENTS.md`
   - `CLAUDE.md`
   - Cursor rules
   - OpenCode configuration
   - Copilot instructions
3. Build and dependency files such as:
   - `package.json`
   - `pnpm-lock.yaml`
   - `yarn.lock`
   - `package-lock.json`
   - `pyproject.toml`
   - `requirements.txt`
   - `pom.xml`
   - `build.gradle`
   - `go.mod`
   - `Cargo.toml`
4. Task or command files such as:
   - `Makefile`
   - `justfile`
   - `scripts/`
5. CI/CD configuration such as:
   - `.github/workflows/`
   - `.gitlab-ci.yml`
   - deployment manifests
6. Existing `docs/` directory
7. Main source directories such as:
   - `src/`
   - `app/`
   - `packages/`
   - `services/`
   - `libs/`

During the analysis, identify:

- project language or languages
- frameworks and runtimes
- build system and dependency management
- local development workflow
- module, package, and folder structure
- test framework and test commands
- lint, format, static analysis, and quality tools
- CI/CD configuration and deployment flow
- database, migration, persistence, and transaction patterns
- authentication, authorization, and security approach
- API, controller, route, or public interface conventions
- logging, tracing, metrics, and observability patterns
- code style, naming, and architectural boundaries
- existing documentation, ADRs, task files, or specification files
- existing agent, Claude, Cursor, Copilot, or OpenCode instructions

---

## Uncertainty Handling

If one of the following cannot be found in the repository:

- standard test command
- standard build command
- standard lint command
- standard format command
- CI pipeline
- deployment flow

Do not invent it.

Instead, explicitly document it as one of the following:

- `No standard test command detected.`
- `No standard build command detected.`
- `No standard lint command detected.`
- `No standard format command detected.`
- `No CI pipeline found.`
- `No deployment flow detected.`

You may add a recommendation only if it is clearly labeled as a recommendation and not as an existing project standard.

---

## Expected Outputs

### 1. `AGENTS.md`

Create `AGENTS.md`, or update it if it already exists.

This file must be the main working contract for AI agents in this repository.

It must include at least these sections:

- Repository overview
- Project structure and modules
- Build, test, and development commands
- Documentation upkeep rule
- Lazy-read policy
- Referenced documents table
- Architecture and package rules
- Testing rules
- Code style and clean code rules
- Security rules
- Persistence and data rules
- Error handling rules
- Logging and observability rules
- Git workflow rules
- Agent-specific instructions
- Tool usage guidance, including IDE, MCP, or agent tooling if present
- Avoid overengineering rules

The commands in `AGENTS.md` must be based only on commands verified from the repository, such as:

- README instructions
- package manager scripts
- Makefile or justfile targets
- CI/CD configuration
- existing scripts

Do not write generic commands such as `npm test`, `mvn test`, or `gradle build` unless they are actually supported by repository files.

---

### 2. `.agents/` Directory Structure

Create a `.agents/` directory if it does not exist.

Create only the subdirectories that are useful for this repository.

Expected structure when skills are needed:

```text
.agents/
  skills/
    <skill-name>/
      SKILL.md
```

Do not create unused or placeholder directories.

---

### 3. Project-Specific Skills

Create project-specific skill files under:

```text
.agents/skills/<skill-name>/SKILL.md
```

Only create a skill if it represents a repeated workflow that is genuinely useful for this repository.

Possible skill candidates include:

- `fullcheck`: runs the repository's full verification flow and summarizes results
- `branch-review`: reviews the current branch against the main branch for bugs, regressions, missing tests, and quality issues
- `feature-analysis`: converts an issue, task, or user request into an actionable technical plan
- `test-strategy`: determines the correct test level and commands for a change
- `release-check`: performs release or deployment readiness checks
- `migration-review`: reviews database migrations or schema changes against project rules

Do not create skills that do not match the actual repository structure or workflow.

Each skill file must use this format:

```markdown
---
name: skill-name
description: When this skill should be used and what user request should trigger it.
---

# Skill Title

This skill's purpose.

## When to Use

Describe the situations where this skill should be used.

## Workflow

1. Steps to perform.
2. Files to read or commands to run.
3. Decision points.

## Output

Describe how the agent should report results to the user.

## Verification

Describe how to verify that the skill was completed successfully.
```

Skill contents must be specific to this repository. Do not copy generic instructions from another project.

---

### 4. Focused `docs/` References

Create or update only the documentation files that are meaningful for this repository.

Possible files include:

- `docs/architecture.md`
- `docs/build.md`
- `docs/testing.md`
- `docs/clean-code.md`
- `docs/persistence.md`
- `docs/api.md`
- `docs/security.md`
- `docs/exception-handling.md`
- `docs/logging.md`
- `docs/ci-cd.md`
- `docs/frontend.md`
- `docs/database-migrations.md`
- `docs/caching.md`
- `docs/observability.md`

Create only the documents that have a real counterpart in the repository.

Each document must be:

- short
- practical
- specific to this repository
- based on real files, commands, and patterns
- useful for agent decision-making

Do not write general software engineering advice.
Do not repeat the codebase.
Document decision rules, boundaries, conventions, and workflows.

---

### 5. Lazy-Read Policy

`AGENTS.md` must define a lazy-read policy.

Agents must not read all documentation upfront.

Agents should read a document only when its topic affects the current task.

However, if a code change touches an area covered by a referenced document, the relevant document must be read before making the change.

---

### 6. Referenced Documents Table

`AGENTS.md` must contain a `Referenced Documents` table with this exact structure:

```markdown
| Topic | Document | When to Read | Summary |
|---|---|---|---|
```

Rules:

- Every document listed in the table must actually exist.
- Every `When to Read` entry must be action-oriented and specific.
- Do not list documents that were not created or do not already exist.
- Do not tell agents to read all documents by default.

Example style:

```markdown
| Testing | `docs/testing.md` | Read before adding, changing, or deleting tests, or before modifying code with test impact. | Test framework, verified commands, test structure, and expectations. |
```

---

## Standards to Convert into Agent Rules

Based on the actual repository, convert the following areas into clear rules that agents can apply:

- architecture and package boundaries
- module dependencies
- public API or route conventions
- test requirements
- fixture, mock, and integration test conventions
- error handling approach
- logging approach
- persistence and transaction rules
- database migration rules, if applicable
- security and secret handling rules
- frontend rules, if applicable
- CI/CD and release rules, if applicable
- naming and code style conventions

Only document a standard if it is supported by repository evidence.
If a standard is missing, label it as missing or unknown instead of inventing one.

---

## Command Documentation Rules

Document only commands that are verified from repository files.

Acceptable command sources:

- `README.md`
- `package.json` scripts
- `Makefile`
- `justfile`
- scripts in `scripts/`
- CI/CD pipeline files
- framework-specific config files if they clearly define commands

For each command, document:

- purpose
- exact command
- when to run it
- whether it is expensive
- whether it requires external services
- whether it modifies files

If a command is missing, state that no standard command was found.

---

## Documentation Upkeep Rule

Add a documentation upkeep rule to `AGENTS.md`.

Agents must update documentation when they change behavior that affects documented project standards.

Examples:

- If build commands change, update `docs/build.md` and `AGENTS.md`.
- If test structure changes, update `docs/testing.md`.
- If API conventions change, update `docs/api.md`.
- If persistence patterns change, update `docs/persistence.md` or `docs/database-migrations.md`.
- If logging or error handling changes, update the relevant document.

Agents should not create documentation churn for small implementation-only changes that do not affect project standards.

---

## Tool Usage Guidance

If the repository contains tool-specific configuration or instructions, document when agents should use them.

Examples:

- OpenCode configuration
- MCP tools
- Cursor rules
- Claude Code instructions
- Copilot instructions
- local scripts
- code generation tools

If no such tooling is detected, state that no repository-specific agent tooling was found.

---

## Avoid Overengineering Rules

Add repository-specific rules that prevent unnecessary complexity.

At minimum, include these constraints:

- Prefer the smallest safe change that satisfies the task.
- Follow existing patterns before introducing new abstractions.
- Do not add new dependencies unless the repository already supports the need or the user approves it.
- Do not introduce compatibility layers, shims, fallbacks, or dual behavior unless there is concrete repository evidence that they are required.
- Do not create generic helper layers without at least two real call sites or an explicit architectural pattern in the repository.
- Do not broaden the scope of a task without user approval.

---

## Work Order

Follow this order:

1. Inspect the repository root.
2. Inspect README, existing agent instructions, build files, and configuration files.
3. Identify project type, runtime, modules, and main development flow.
4. Inspect existing documentation.
5. Determine which focused `docs/` files are actually needed.
6. Draft or update `AGENTS.md` based on repository evidence.
7. Create or update only meaningful `docs/` files.
8. Create only useful `.agents/skills/*/SKILL.md` files.
9. Verify that every referenced document in `AGENTS.md` exists.
10. Verify that all documented commands are supported by repository files.
11. Verify that no invented standards, tools, or workflows were added.
12. Report the result without committing changes.

---

## Quality Checklist

Before finishing, verify:

- `AGENTS.md` is sufficient as the single entry point for agents.
- The referenced documents table contains only existing files.
- Every `When to Read` entry is clear and actionable.
- Skill descriptions are specific enough for an agent to know when to use them.
- Commands are based on actual repository files.
- Instructions are project-specific rather than generic boilerplate.
- New files are not unnecessarily long.
- Unknown items are labeled clearly instead of being guessed.
- No commits were created.

---

## Final Report Format

At the end, report only the following sections:

### Created / Updated Files

For each file:

- path
- short description

### Key Standards Added

Briefly list the main standards added for agents.

### Unknown / Needs Clarification

List anything that could not be verified from the repository or requires user decision.

---

## Important Constraint

Do not commit anything.
Only create or edit files, then report what changed.
