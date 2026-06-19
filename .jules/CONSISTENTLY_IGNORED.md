## IGNORE: Modifying README.md while documenting conventions

**- Pattern:** Updating `README.md` to add links to `AGENTS.md` or document project conventions.
**- Justification:** Scope expansion. Project conventions should be documented exclusively in `AGENTS.md`, without modifying product documentation like `README.md` unless explicitly requested.
**- Files Affected:** `README.md`

## IGNORE: Applying security fixes to dummy HTML elements

**- Pattern:** Adding security attributes like `method="POST"`, `rel="noopener noreferrer"`, or SRI attributes to elements.
**- Justification:** `index.html` is a static CSS showcase containing dummy elements for visual demonstration. Security vulnerabilities on these elements are false positives.
**- Files Affected:** `index.html`

## IGNORE: Moving or wrapping index.html content without build config updates

**- Pattern:** Moving `index.html` to `src/index.html` or wrapping its content in `<section>` tags.
**- Justification:** Moving the entrypoint or changing its structure without simultaneously updating reference paths and providing a build configuration breaks deployments.
**- Files Affected:** `index.html`, `src/index.html`

## IGNORE: Using unpinned dependencies or downgraded actions

**- Pattern:** Specifying `"latest"` for tools in `mise.toml` or using downgraded GitHub Actions like `mise-action@v2` or `actions/checkout@v4`.
**- Justification:** Tools must be pinned to exact versions in `mise.toml`. Downgrading dependencies is strictly prohibited unless explicitly requested.
**- Files Affected:** `mise.toml`, `.github/workflows/*.yml`

## IGNORE: Defining dummy test scripts in mise.toml

**- Pattern:** Adding dummy scripts like `test = "echo ..."` or `test = "grep ..."` in `mise.toml`.
**- Justification:** The `mise.toml` configuration must use wildcard dependencies (e.g., `[task]:*`) for `install`, `test`, and `codegen` tasks instead of dummy echo/grep scripts.
**- Files Affected:** `mise.toml`

## IGNORE: Removing commented-out example code from the static showcase

**- Pattern:** Deleting commented-out HTML or script tags from the showcase file.
**- Justification:** The file is a showcase/template, and commented code is intentional for examples or future use.
**- Files Affected:** `index.html`
