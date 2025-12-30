# Ready new repo for python development

Note: This instruction extends [Developer setup](2000-instruction-developer-setup.md) and assumes developer setup has been done previously.

## Initialize uv

1. Open terminal
2. Run `uv init`

## Add linting and type checking tools

1. Open terminal
2. Run: `uv add --dev ruff mypy pylint pydoclint pre-commit`
3. Run: `uv sync`

## Setup pre-commit

1. Validate install: `uv run pre-commit --version`
2. Copy `.pre-commit-config.yaml` from `templates/` directory to project root:
   ```bash
   cp templates/.pre-commit-config.yaml .
   ```
3. Copy `.markdownlint.yaml` from `templates/` directory to project root:
   ```bash
   cp templates/.markdownlint.yaml .
   ```

4. Run: `uv run pre-commit install`

5. Verify: `uv run pre-commit run --all-files`

## Setup project configuration

1. Copy `pyproject.toml.template` from `templates/` directory to `pyproject.toml` in project root
2. Customize `pyproject.toml`:
   - Update project name and description
   - Add your project dependencies
   - Adjust Python version if needed
   - Customize tool configurations as needed

## Setup Makefile (optional)

1. Copy `Makefile.template` from `templates/` directory to `Makefile` in project root
2. Customize `Makefile`:
   - Add your service names
   - Add project-specific targets
   - Configure Docker compose files if used

## Setup CI workflow (optional)

1. Copy `ci.yml.template` from `templates/.github/workflows/` to `.github/workflows/ci.yml` in your repository
2. Customize the workflow:
   - Adjust Python version if needed
   - Add project-specific CI steps
   - Configure branch names

## Local CI checks

You can run CI-equivalent checks locally using:

```bash
make check
```

This will run all linting, type checking, and tests locally before pushing.
