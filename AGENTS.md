# AGENTS.md

## Roles and Agents
- **📝 Docs**: Specialist agent focused on high-quality code documentation. Analyzes the codebase and adds/improves docstrings to generate value for both humans and LLMs.
- **🛟 Arrumador**: Agent responsible for configuring tooling, CI, and maintaining development workflows.
- **🛡️ Sentinel**: Agent responsible for security fixes and identifying vulnerabilities.
- **🛠️ Refactor**: Agent responsible for structural changes, semantic structures, and codifying conventions.

## Project Conventions
- **CI/CD Sequence:** The project enforces exactly one CI/CD GitHub Actions workflow (`.github/workflows/autorelease.yml`) that follows a strict execution sequence: Install -> Codegen -> PR if Diff -> CI -> Release -> Artifacts.
- **Tool Management:** The project strictly uses `mise` for tool management (e.g., Node.js 20.14.0). Tools must be pinned to exact versions in `mise.toml`. Bootstrap scripts like `install-mise.sh` must never be committed.
- **Task Dependencies:** The `mise.toml` configuration must use wildcard dependencies (e.g., `[task]:*`) for `install`, `test`, and `codegen` tasks.
- **CI Tasks:** Standard continuous integration and testing tasks are executed via `mise run ci` and `mise run test`.
- **Linting & Formatting:** All code linting and formatting must be handled exclusively by `workspaced` via `mise` (using the `github:lucasew/workspaced` backend). Do not install or configure individual linters manually.
- **Error Handling:** All errors must be handled through a centralized error-reporting function. Empty catch blocks and direct `console.error` or `Sentry.captureException` calls at the call site are strictly forbidden. If Sentry is not set up, it MUST log the error with enough context.
- **Negative Memory:** Before planning work, consult `.jules/CONSISTENTLY_IGNORED.md` to avoid submitting changes or patterns that have been consistently rejected by human reviewers.
- **Security Logs:** Security fixes and learnings must be logged in `.jules/sentinel.md` by appending a single-line journal entry in the format: `- YYYY-MM-DD: [the class of issue and how to spot it]`.
- **Frontend Entrypoint:** The main frontend entrypoint is `index.html`, which functions as a classless CSS showcase structured with semantic HTML `<section>` tags.
- **Execution Guardrails:** File modifications must be restricted to allowed paths (`src/**`, `tests/**`, `.jules/**`). Forbidden paths (`install-mise.sh`, `bin/**`, `tmp/**`) must not be changed.
- **Pull Requests:** PR titles must use the exact format specified by the active agent (e.g., '📝 Docs: [Description]'). PRs must include the following sections: 'Assumptions', 'Alternatives Not Chosen', 'How To Pivot', and 'Next Knobs'.

## Operational Memory (Path-to-Responsibility)
- `/index.html` -> Main frontend entrypoint, classless CSS showcase with semantic `<section>` tags.
- `.github/workflows/autorelease.yml` -> Enforced CI/CD GitHub Actions workflow.
- `mise.toml` -> Pinned tool versions and wildcard task dependencies (`install`, `test`, `codegen`).
- `.jules/CONSISTENTLY_IGNORED.md` -> Negative memory for patterns consistently rejected by human reviewers.
- `.jules/sentinel.md` -> Security journal for fixes and learnings.
- `src/**`, `tests/**`, `.jules/**` -> Allowed paths for code changes.
