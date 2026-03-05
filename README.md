# Experimento de CSS classless para a homepage

## Purpose

This project is an experiment and a showcase of a classless CSS framework (e.g. water.css) utilizing standard, semantic HTML elements. It demonstrates how a web page can look attractive and properly formatted without littering the HTML with custom CSS classes.

## Layout

- `index.html`: The main frontend entrypoint. It acts as a comprehensive classless CSS showcase, properly structured using standard semantic HTML `<section>` tags.
- `renovate.json`: Configuration file for Renovate dependency updates.

## Tooling

This project uses `mise` for tool management (e.g., Node.js). Tools are pinned to exact versions in `mise.toml`. Standard continuous integration and testing tasks are executed via `mise run ci` and `mise run test`. Ensure you have `mise` installed and activated in your environment.

## Contribution

When contributing, ensure:
1. All changes respect the "classless CSS" philosophy.
2. Tools are appropriately managed via `mise`.
3. Error handling follows the centralized error-reporting pattern, no empty catch blocks.

For more detailed conventions and operational memory, refer to `AGENTS.md` which serves as the source of truth for repository guidelines.
