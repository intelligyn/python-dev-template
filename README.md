# Python Development Template

A template repository for setting up Python projects with consistent developer tooling, linting, and quality checks.

## Purpose

This template provides:

- Standardized developer setup instructions
- Pre-configured linting and type checking tools (`ruff`, `mypy`, `pylint`, `pydoclint`)
- `pre-commit` hooks configuration
- Common `Makefile` targets
- CI/CD workflow templates

## Usage

### Option 1: Use as GitHub Template

1. Click *"Use this template"* button on GitHub
2. Create your new repository from this template
3. Customize project-specific content (see **Customization** section)

### Option 2: Clone and Customize

```bash
git clone https://github.com/intelligyn/python-dev-template.git your-project-name
cd your-project-name
# Remove .git and initialize new repository
rm -rf .git
git init
# Customize files as needed
```

## What's Included

### Documentation

- `docs/setup/2000-instruction-developer-setup.md` - Developer environment setup instructions
- `docs/setup/2000-instruction-ready-repository.md` - Repository initialization guide

### Template Files

- `templates/.pre-commit-config.yaml` - Pre-commit hooks configuration
- `templates/.markdownlint.yaml` - Markdown linting configuration
- `templates/Makefile.template` - Common Makefile targets
- `templates/pyproject.toml.template` - Python project configuration
- `templates/.github/workflows/ci.yml.template` - CI workflow template

## Customization

After creating your repository from this template:

1. **Update project name** in:
   - `README.md`
   - `pyproject.toml` (project name, description)
   - Documentation files

2. **Add project-specific content**:
   - Regulatory context (if applicable)
   - Project-specific service names
   - Custom dependencies

3. **Configure CI/CD**:
   - Update workflow files as needed
   - Configure repository secrets

## Tools Included

- **ruff** - Fast Python linter and formatter
- **mypy** - Static type checker
- **pylint** - Code quality checker
- **pydoclint** - Docstring linter
- **pre-commit** - Git hooks framework
- **markdownlint** - Markdown linter

## Requirements

- Python 3.12+
- uv (Python package manager)
- Docker (for containerized development)
- Git
