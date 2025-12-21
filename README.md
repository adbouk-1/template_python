# template_python
Template for using uv, pre-commit with ruff, pylint, codespell configured

Overview
--------
This repo is a reusable Python project template that includes linting and formatting via pre-commit hooks (ruff, pylint, codespell, and an `uv` lock hook). The sections below explain how to set up a local development environment on macOS (zsh), install pre-commit, and run the usual developer commands (format, lint, test).


Quick setup using uv (macOS, zsh)
--------------------------------
This project includes `uv`-related hooks and a lockfile. The steps below use `uv` to manage and run developer tooling. If you don't already have `uv` installed, install it with `pipx` (recommended) or pip.

1. Install uv (recommended via pipx):

```bash
# install pipx if you don't have it
python3 -m pip install --user pipx
python3 -m pipx ensurepath
pipx install uv
```

Or with pip:

```bash
python3 -m pip install --user uv
```

2. Install project dependencies from the lockfile (or create one):

```bash
# Install from the lockfile (preferred)
uv install

# If you need to create/update the lockfile after changing pyproject.toml:
uv lock
```

3. Run pre-commit and other tooling through uv so they use the same environment:

```bash
# Install the git hook
uv run pre-commit install
# Optionally install hook environments locally
uv run pre-commit install --install-hooks
# Run all hooks across the repository
uv run pre-commit run --all-files
```

4. Run tests and linters via uv:

```bash
uv run pytest -q
uv run pre-commit run ruff --all-files
uv run pre-commit run pylint --all-files
```

Notes
-----
- `uv run <cmd>` executes `<cmd>` in the virtual environment resolved by `uv` so you don't need to manually activate `.venv`.
- If you prefer traditional venv workflows or need to debug installation issues, you can still create/activate a `.venv` and use `pip` directly, but using `uv` ensures consistency with the lockfile and with the repo's pre-commit `uv-lock` hook.

Notes about `uv`
-----------------
- This template includes a pre-commit hook for `uv` (the `uv-lock` hook) which keeps the `uv` lockfile in sync. If you use the `uv` dependency manager, follow the `uv` project docs for installing and initializing `uv` in your repo. The pre-commit hook will ensure the lockfile is updated automatically on commits where applicable.

Linting, formatting, and testing
--------------------------------
- To run all formatters/linters configured as pre-commit hooks locally:

```bash
pre-commit run --all-files
```

- You can run specific hooks (for example `ruff`) via:

```bash
pre-commit run ruff --all-files
```

- Run tests with pytest:

```bash
pytest -q
```
