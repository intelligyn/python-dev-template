# Ready new repo for python development

Note: This instruction extends [Developer setup](2000-instruction-developer-setup.md) and assumes developer setup has been done previously.

## Install dependencies

All configuration files are already included in the repository. You just need to customize placeholders and install dependencies:

1. Open terminal
2. Run: `uv sync`

This will install all dependencies including dev dependencies (ruff, mypy, pylint, pydoclint, pre-commit, pytest) that are already defined in `pyproject.toml`.

## Customize configuration files

Replace placeholders in the following files:

1. **`pyproject.toml`**:
   - Replace `{your-project-name}` with your project name
   - Replace `{Your project description}` with your description
   - Replace `{0.1.0}` with your initial version
   - Add your project dependencies

2. **`Makefile`** (if using Docker Compose):
   - Replace `{service1}`, `{service2}`, etc. with your service names

3. **`.github/workflows/ci.yml`** (optional):
   - Replace `{3.12}` with your Python version if different

## Setup pre-commit

1. Validate install: `uv run pre-commit --version`
2. Run: `uv run pre-commit install`
3. Verify: `uv run pre-commit run --all-files`

## Local CI checks

You can run CI-equivalent checks locally using:

```bash
make check
```

This will run all linting, type checking, and tests locally before pushing.
