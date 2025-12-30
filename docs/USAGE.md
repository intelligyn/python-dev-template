# Usage Guide

This guide provides detailed instructions for using the Python Development Template.

## Table of Contents

1. [Creating a New Repository](#creating-a-new-repository)
2. [Initial Setup](#initial-setup)
3. [Customization Points](#customization-points)
4. [Common Customizations](#common-customizations)
5. [Troubleshooting](#troubleshooting)

## Creating a New Repository

### Method 1: GitHub Template (Recommended)

1. Navigate to the [template repository](https://github.com/intelligyn/python-dev-template)
2. Click the green **"Use this template"** button
3. Fill in:
   - Repository name
   - Description
   - Visibility (Public/Private)
4. Click **"Create repository from template"**
5. Clone your new repository:

   ```bash
   git clone https://github.com/your-org/your-project-name.git
   cd your-project-name
   ```

### Method 2: Manual Clone

```bash
git clone https://github.com/intelligyn/python-dev-template.git your-project-name
cd your-project-name
rm -rf .git
git init
git add .
git commit -m "Initial commit from template"
git remote add origin https://github.com/your-org/your-project-name.git
git push -u origin main
```

## Initial Setup

### Step 1: Customize Placeholders

All configuration files are already included in the repository root. Simply replace placeholders:

**In `pyproject.toml`:**

- Replace `{your-project-name}` with your project name
- Replace `{Your project description}` with your description
- Replace `{0.1.0}` with your initial version
- Add your project dependencies

**In `Makefile` (if using Docker Compose):**

- Replace `{service1}`, `{service2}`, etc. with your service names

**In `.github/workflows/ci.yml` (optional):**

- Replace `{3.12}` with your Python version if different

### Step 2: Install Dependencies

```bash
# Install all dependencies (dev dependencies are already defined in pyproject.toml)
uv sync
```

### Step 3: Set Up Pre-commit Hooks

```bash
# Install pre-commit hooks
uv run pre-commit install

# Run pre-commit on all files to verify setup
uv run pre-commit run --all-files
```

### Step 4: Verify Setup

```bash
# Run all checks locally
make check
```

If everything passes, your setup is complete!

## Customization Points

### Required Customizations

These must be customized for every project:

1. **Project Name** - Replace `{your-project-name}` in:
   - `pyproject.toml`
   - `README.md`
   - Documentation files

2. **Project Description** - Replace `{Your project description}` in:
   - `pyproject.toml`
   - `README.md`

3. **Dependencies** - Add your project dependencies to `pyproject.toml`

### Optional Customizations

These can be customized based on project needs:

1. **Python Version** - Update if not using Python 3.12
2. **Service Names** - Update in `Makefile` if using Docker Compose
3. **Regulatory Context** - Add to documentation if applicable
4. **CI/CD Steps** - Add project-specific CI steps
5. **Tool Configuration** - Adjust linting/type checking rules

## Common Customizations

### Adding a New Dependency

```toml
# In pyproject.toml
dependencies = [
  "requests>=2.31.0",
  "pydantic>=2.5.0",
]
```

Then run:

```bash
uv sync
```

### Configuring Multiple Services

```toml
[dependency-groups]
api = [
  "fastapi>=0.104.0",
  "uvicorn>=0.24.0",
]
worker = [
  "celery>=5.3.0",
  "redis>=5.0.0",
]
```

### Adding Custom Makefile Targets

```makefile
# In Makefile
.PHONY: deploy test-integration

deploy:
 @echo "Deploying to production..."
 # Add your deployment commands

test-integration:
 uv run pytest tests/integration/
```

### Customizing Ruff Rules

```toml
# In pyproject.toml
[tool.ruff]
lint.select = [
  "E",   # pycodestyle errors
  "F",   # pyflakes
  "I",   # isort
  "B",   # flake8-bugbear
  "UP",  # pyupgrade
  "SIM", # flake8-simplify (add this)
]
```

### Adding CI Secrets

1. Go to repository Settings → Secrets and variables → Actions
2. Add required secrets (e.g., `PYPI_API_TOKEN`, `DOCKER_HUB_TOKEN`)
3. Reference in workflow:

   ```yaml
   - name: Publish
     env:
       TOKEN: ${{ secrets.PYPI_API_TOKEN }}
   ```

## Troubleshooting

### Pre-commit Hooks Not Running

```bash
# Reinstall hooks
uv run pre-commit uninstall
uv run pre-commit install

# Test manually
uv run pre-commit run --all-files
```

### uv Command Not Found

Install uv:

```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### Makefile Targets Not Working

Ensure you're using the correct Makefile:

```bash
# Check if Makefile exists
ls -la Makefile

# Use explicit path if needed
make -f Makefile check
```

### CI Workflow Failing

1. Check workflow logs in GitHub Actions
2. Verify Python version matches your local setup
3. Ensure all dependencies are in `pyproject.toml`
4. Check if secrets are configured (if needed)

### Type Checking Errors

```bash
# Run mypy with more verbose output
uv run mypy --show-error-codes src tests

# Ignore specific errors (add to pyproject.toml)
[tool.mypy]
ignore_errors = true  # Or use per-file ignores
```

## Next Steps

After completing setup:

1. Review and customize documentation files
2. Add your project-specific code
3. Configure CI/CD secrets if needed
4. Set up branch protection rules
5. Add project-specific tests

For more information, see the [main README](../README.md).
