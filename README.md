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

## Usage

### Option 1: Use as GitHub Template (Recommended)

1. Click **"Use this template"** button on GitHub
2. Create your new repository from this template
3. Clone your new repository locally
4. Follow the customization steps below

### Option 2: Clone and Customize

```bash
git clone https://github.com/intelligyn/python-dev-template.git your-project-name
cd your-project-name
# Remove .git and initialize new repository
rm -rf .git
git init
git add .
git commit -m "Initial commit from template"
# Customize files as needed
```

## Quick Start

After creating your repository from this template:

1. **Copy template files to project root:**
   ```bash
   cp templates/.pre-commit-config.yaml .
   cp templates/.markdownlint.yaml .
   cp templates/Makefile.template Makefile
   cp templates/pyproject.toml.template pyproject.toml
   cp templates/.github/workflows/ci.yml.template .github/workflows/ci.yml
   ```

2. **Customize `pyproject.toml`:**
   - Replace `{your-project-name}` with your project name
   - Update `{Your project description}` with your description
   - Add your project dependencies

3. **Initialize the project:**
   ```bash
   uv init
   uv add --dev ruff mypy pylint pydoclint pre-commit pytest pytest-html
   uv sync
   ```

4. **Set up pre-commit hooks:**
   ```bash
   uv run pre-commit install
   uv run pre-commit run --all-files
   ```

5. **Verify everything works:**
   ```bash
   make check
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

## Customization Guide

### 1. Project Identity

Replace placeholders marked with `**{placeholder}**` throughout the template:

**In `pyproject.toml`:**
```toml
name = "{your-project-name}"  # Replace with actual project name
description = "{Your project description}"  # Replace with description
```

**In documentation files:**
- `docs/setup/2000-instruction-developer-setup.md`: Replace `**{Project name}**`, `**{Your system/project name}**`
- Update regulatory context if applicable: `**{Add your regulatory context if applicable, e.g., EU MDR / IEC 62304}**`

### 2. Dependencies

**Add runtime dependencies:**
```toml
dependencies = [
  "dependency1>=1.0.0",
  "dependency2>=2.0.0",
]
```

**Add dependency groups** (if using multiple services/components):
```toml
[dependency-groups]
service1 = [
  "service1-dependency>=1.0.0",
]
service2 = [
  "service2-dependency>=2.0.0",
]
```

### 3. Makefile Customization

**Update service names:**
```makefile
SERVICES := {service1} {service2} test
```

**Add project-specific targets:**
```makefile
# Your custom targets
deploy:
	@echo "Deploying..."

test-integration:
	uv run pytest tests/integration/
```

### 4. CI/CD Workflow

**Update Python version** (if different from 3.12):
```yaml
python-version: "{3.12}"  # Update if needed
```

**Add project-specific CI steps:**
```yaml
- name: Custom step
  run: your-command-here
```

### 5. Documentation Customization

**Update developer setup instructions:**
- Replace `**{Project name}**` with your project name
- Update `**{Add project-specific constraints}**` with your constraints
- Customize `**{your change control process}**` with your process

**Example customization:**
```markdown
**Regulatory Context:** EU MDR / IEC 62304
**Applicable System:** My Medical Device Software

## 2. Scope

Applies to:
- All My Medical Device Software developers
```

## Examples

### Example 1: Simple Python Library

```toml
[project]
name = "my-python-lib"
description = "A simple Python library"
dependencies = [
  "requests>=2.31.0",
]
```

### Example 2: Multi-Service Application

```toml
[project]
name = "my-microservices-app"
dependencies = []

[dependency-groups]
api = [
  "fastapi>=0.104.0",
  "uvicorn>=0.24.0",
]
worker = [
  "celery>=5.3.0",
]
```

### Example 3: Medical Device Software

```markdown
**Regulatory Context:** EU MDR / IEC 62304
**Applicable System:** Medical Device Software v1.0

## 10. Constraints
- No PHI stored or processed locally
- Device must remain security compliant
- Only approved versions allowed
```

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

We welcome contributions to improve this template! To propose changes:

1. **Create an issue** describing the change or improvement
2. **Fork the repository** and create a feature branch
3. **Make your changes** and test them
4. **Submit a pull request** with:
   - Clear description of changes
   - Rationale for the change
   - Examples if adding new features

### Contribution Guidelines

- Keep changes generic and reusable across projects
- Update documentation when adding new features
- Test changes by creating a test repository from your fork
- Follow the existing code style and structure

## Versioning

This template uses semantic versioning. Check [releases](https://github.com/intelligyn/python-dev-template/releases) for version history.

**Version format:** `v1.0.0` (Major.Minor.Patch)

- **Major**: Breaking changes that require manual updates
- **Minor**: New features or improvements (backward compatible)
- **Patch**: Bug fixes and minor updates

### Updating from Template

When a new version is released:

1. Review the [changelog](https://github.com/intelligyn/python-dev-template/releases)
2. Compare your customized files with the new template version
3. Manually merge changes into your project
4. Test thoroughly before committing

## Support

For questions or issues:

- Open an [issue](https://github.com/intelligyn/python-dev-template/issues) on GitHub
- Check existing [discussions](https://github.com/intelligyn/python-dev-template/discussions)

## License

[Add your license here - template users should specify their own license]
