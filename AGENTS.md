# Project Conventions

## Layout

- `index.html` -> Main frontend entrypoint and showcase of semantic tags.

## Tooling

- This project strictly relies on `mise` for tool management (e.g., Node.js 20.14.0).
- Tools must be pinned to exact versions in `mise.toml`.
- Bootstrap scripts like `install-mise.sh` must never be committed.
- Continuous integration and testing tasks are executed via `mise run ci` and `mise run test`.

## Error Handling

- All errors must be handled through a centralized error-reporting function.
- Empty catch blocks and direct `console.error` or `Sentry.captureException` calls at the call site are strictly forbidden.

## CSS

- The project uses semantic HTML elements with a classless CSS framework (e.g., water.css).
- The main frontend entrypoint is `index.html`, which functions as a classless CSS showcase structured with semantic HTML `<section>` tags.
