# Project Conventions (`AGENTS.md`)

This file is the source of truth for project conventions, operational memory, and execution rules. For every file you touch, you must obey instructions in any `AGENTS.md` file whose scope includes that file.

## Operational Memory & Path-to-Responsibility Mapping

- `src/index.html` -> Main frontend entrypoint, functioning as a classless CSS showcase structured with semantic HTML `<section>` tags.
- `.github/workflows/autorelease.yml` -> The sole CI/CD GitHub Actions workflow. Enforces a strict execution sequence: Install -> Codegen -> PR if Diff -> CI -> Release -> Artifacts.
- `mise.toml` -> Strict tool management configuration. Supports CI via wildcard dependencies (e.g., `[task]:*`) for `install`, `test`, and `codegen` tasks.
- `.jules/CONSISTENTLY_IGNORED.md` -> Negative memory. Consult before planning work to avoid submitting rejected changes/patterns.
- `.jules/sentinel.md` -> Security fixes and learnings journal. Append entries as: `- YYYY-MM-DD: [the class of issue and how to spot it]`.

## Tooling & CI

- **Mise First:** The project strictly uses `mise` for tool management (e.g., Node.js 20.14.0).
  - Tools must be pinned to exact versions in `mise.toml` (no latest or LTS).
  - When creating or updating a local `mise.toml` file, you must execute `mise trust` to bypass untrusted configuration errors.
  - To install `mise` during an active session without triggering blocklist errors for `sh`/`bash`: `export MISE_INSTALL_PATH=/usr/local/bin/mise && curl -sSfL https://mise.run | sudo -E MISE_INSTALL_PATH=$MISE_INSTALL_PATH sh`.
  - Bootstrap scripts like `install-mise.sh` must never be committed.
- **Task Execution:**
  - Standard CI and tests are executed via `mise run ci` and `mise run test`.
- **Linting & Formatting:**
  - All code linting and formatting must be handled exclusively by `workspaced` via `mise` (using the `github:lucasew/workspaced` backend). Do not install or configure individual linters manually.

## Error Handling

- **Centralized Error Reporting:** All errors must be handled through a centralized error-reporting function.
- Empty catch blocks are strictly forbidden.
- Direct `console.error` or `Sentry.captureException` calls at the call site are strictly forbidden.

## Frontend Verification

- Frontend modifications must be visually verified using Playwright.
- Install dependencies: `pip install pytest-playwright && playwright install chromium`.
- Execute a temporary Python script to capture screenshots and videos of the relevant user journey.
- Ensure file paths in the script reference `/app` as the workspace root (e.g., `page.goto("file:///app/index.html")`).

## Security

- **Vulnerability Escalation:** If a Critical or High vulnerability requires more than 50 lines to fix properly, do not silently drop it. Escalate by opening a PR with a `// SECURITY: [severity] — [description]` comment at the vulnerable site and document the full scope in the PR body.
- **Security Headers:** Avoid adding security headers (like Content-Security-Policy) blindly. They are low priority and dangerous to inject without tracing their impact.
- **Logging:** Security fixes and learnings must be logged in `.jules/sentinel.md`.

## Execution Guardrails & Scope

- Modifications must be strictly restricted to the allowed paths defined by the active agent (e.g., `src/**`, `tests/**`, `.jules/**`).
- Forbidden paths (`install-mise.sh`, `bin/**`, `tmp/**`) must never be changed unless explicitly authorized.
- Mandatory pre-commit checks (`git diff --name-only`) must be run to verify this execution guardrail.

## Pull Requests

- Must use the exact title format specified by the active agent (e.g., '📝 Docs: [Description]', '🛟 Arrumador: [Description]', or '🛡️ Sentinel: [Severity] [Description]').
- Must include the following mandatory sections in the body: `Assumptions`, `Alternatives Not Chosen`, `How To Pivot`, and `Next Knobs`.
