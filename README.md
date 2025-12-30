# Python Development Template

A template repository for setting up Python projects with consistent developer tooling, linting, and quality checks.

## Purpose

This template provides:

- Standardized developer setup instructions
- Pre-configured linting and type checking tools (`ruff`, `mypy`, `pylint`, `pydoclint`)
- `pre-commit` hooks configuration
- Common `Makefile` targets
- CI/CD workflow templates

Use this template to quickly bootstrap new Python projects with best practices and consistent tooling across your organization.

## Quick Start

1. Click **"Use this template"** button on GitHub to create your repository
2. Clone your new repository locally
3. Customize placeholders in `pyproject.toml`, `Makefile`, and documentation files
4. Run `uv sync` to install dependencies
5. Run `uv run pre-commit install` to set up hooks
6. Run `make check` to verify everything works

For detailed instructions, see [Usage Guide](docs/USAGE.md).

## What's Included

### Configuration Files

All configuration files are included in the repository root with placeholders:

- `pyproject.toml` - Python project configuration
- `Makefile` - Common Makefile targets
- `.pre-commit-config.yaml` - Pre-commit hooks
- `.markdownlint.yaml` - Markdown linting
- `.github/workflows/ci.yml` - CI workflow

### Documentation

- `docs/setup/2000-instruction-developer-setup.md` - Developer environment setup
- `docs/setup/2000-instruction-ready-repository.md` - Repository initialization guide
- `docs/USAGE.md` - Detailed usage instructions
- `docs/CUSTOMIZATION_EXAMPLES.md` - Customization examples

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

## Contributing

We welcome contributions! To propose changes:

1. Create an [issue](https://github.com/intelligyn/python-dev-template/issues) describing the change
2. Fork the repository and create a feature branch
3. Make your changes and test them
4. Submit a pull request

### Contribution Guidelines

- Keep changes generic and reusable across projects
- Update documentation when adding new features
- Test changes by creating a test repository from your fork

## Versioning

This template uses semantic versioning. Check [releases](https://github.com/intelligyn/python-dev-template/releases) for version history.

## Support

For questions or issues:

- Open an [issue](https://github.com/intelligyn/python-dev-template/issues) on GitHub
- Check existing [discussions](https://github.com/intelligyn/python-dev-template/discussions)

## License

[Add your license here - template users should specify their own license]
