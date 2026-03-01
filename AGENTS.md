# Project Conventions

## Where Things Live
* `index.html` -> Main showcase for CSS classless experiment, demonstrating HTML elements with minimal styling.

## Rules

### Error Handling
* **Centralized Error Reporting:** The project MUST have a single, centralized error-reporting function (e.g., `reportError`, `captureException`, or equivalent). All code paths that handle unexpected errors MUST funnel through this function. Never call `console.error` or `Sentry.captureException` directly at the call site.
* **No silent failures:** Every `catch` block, every `.catch()`, every error callback that is not an expected/recoverable condition MUST call the centralized error-reporting function. "Out of scope" is not an excuse to swallow an error.
