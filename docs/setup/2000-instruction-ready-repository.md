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
2. Copy `.pre-commit-config.yaml` from `templates/` directory to project root, or create it with the following content:

   ```yaml
   repos:
     - repo: https://github.com/pre-commit/pre-commit-hooks
       rev: v6.0.0
       hooks:
         - id: end-of-file-fixer
         - id: trailing-whitespace

     - repo: https://github.com/igorshubovych/markdownlint-cli
       rev: v0.47.0
       hooks:
         - id: markdownlint
           args: [--fix]

     - repo: local
       hooks:
         - id: ruff-check
           name: ruff check
           entry: uv run ruff check --fix
           language: system
           types: [python]

         - id: ruff-format
           name: ruff format
           entry: uv run ruff format
           language: system
           types: [python]

         - id: mypy
           name: mypy
           entry: uv run mypy
           language: system
           pass_filenames: false

         - id: pydoclint
           name: pydoclint
           entry: uv run pydoclint src tests
           language: system
           pass_filenames: false

         - id: pylint
           name: pylint
           entry: uv run pylint src tests
           language: system
           types: [python]
           pass_filenames: false
   ```

3. Copy `.markdownlint.yaml` from `templates/` directory to project root, or create it with:

   ```yaml
   default: true

   # Disable:
   MD013: false  # line-length
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
