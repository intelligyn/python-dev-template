# Customization Examples

This document provides real-world examples of how to customize the template for different project types.

## Example 1: Simple Python Library

**Use Case:** A standalone Python library with minimal dependencies.

### pyproject.toml

```toml
[project]
name = "my-awesome-lib"
version = "0.1.0"
description = "A simple Python library for awesome things"
readme = "README.md"
requires-python = ">=3.12"

dependencies = [
  "requests>=2.31.0",
]

[dependency-groups]
dev = [
  "mypy>=1.19.0",
  "pre-commit>=4.5.0",
  "pydoclint>=0.8.3",
  "pylint>=4.0.4",
  "pytest",
  "pytest-html>=4.1.1",
  "ruff>=0.14.8",
]
```

### Makefile

```makefile
SHELL := /bin/bash
.SHELLFLAGS := -euo pipefail -c

.PHONY: help check test build

help:
	@echo "Available targets:"
	@echo "  make check    Run all quality checks"
	@echo "  make test     Run tests"
	@echo "  make build    Build distribution"

check:
	uv sync --group dev --frozen
	uv run pre-commit run -a
	mkdir -p verification-history
	uv run pytest

test:
	uv run pytest

build:
	uv build
```

## Example 2: Multi-Service Microservices Application

**Use Case:** An application with multiple services, each with different dependencies.

### pyproject.toml

```toml
[project]
name = "my-microservices-app"
version = "1.0.0"
description = "Microservices application with API and worker services"
readme = "README.md"
requires-python = ">=3.12"

dependencies = [
  # Shared dependencies
  "pydantic>=2.5.0",
  "python-dotenv>=1.0.0",
]

[dependency-groups]
api = [
  "fastapi>=0.104.0",
  "uvicorn[standard]>=0.24.0",
  "sqlalchemy>=2.0.0",
]

worker = [
  "celery>=5.3.0",
  "redis>=5.0.0",
  "psycopg2-binary>=2.9.0",
]

dev = [
  "mypy>=1.19.0",
  "pre-commit>=4.5.0",
  "pydoclint>=0.8.3",
  "pylint>=4.0.4",
  "pytest",
  "pytest-html>=4.1.1",
  "ruff>=0.14.8",
]
```

### Makefile

```makefile
SHELL := /bin/bash
.SHELLFLAGS := -euo pipefail -c
COMPOSE := docker compose

DEV_FILES := -f compose.dev.yml
PROD_FILES := -f compose.prod.yml

SERVICES := api worker scheduler

.DEFAULT_GOAL := help

define assert-service
	@if ! printf "%s\n" "$(SERVICES)" | tr ' ' '\n' | grep -qx "$*"; then \
		echo "ERROR: Unknown service '$*'"; \
		echo "Allowed services: $(SERVICES)"; \
		exit 1; \
	fi
endef

.PHONY: help check dev-up dev-down dev-logs

help:
	@echo "Development:"
	@echo "  make dev-up          Start all services"
	@echo "  make dev-down        Stop all services"
	@echo "  make dev-logs        View logs"
	@echo ""
	@echo "Quality:"
	@echo "  make check           Run all checks"

check:
	uv sync --group dev --frozen
	uv run pre-commit run -a
	mkdir -p verification-history
	uv run pytest

dev-up:
	$(COMPOSE) $(DEV_FILES) up -d

dev-down:
	$(COMPOSE) $(DEV_FILES) down

dev-logs:
	$(COMPOSE) $(DEV_FILES) logs -f
```

## Example 3: Medical Device Software (Regulated)

**Use Case:** Software as a Medical Device (SaMD) requiring regulatory compliance.

### Documentation Customization

**docs/setup/2000-instruction-developer-setup.md:**

```markdown
# Developer Setup Development Environment Instruction

**Regulatory Context:** EU MDR / IEC 62304
**Applicable System:** Medical Device Software v2.0

## 2. Scope

Applies to:
- All Medical Device Software developers
- macOS, Linux, and Windows with wsl development laptops

Does not apply to:
- Production systems
- Clinical systems
- Customer-operated systems

## 10. Constraints

- No PHI stored or processed locally
- Cloud sync folders must not contain source code
- Only approved versions allowed
- Device must remain security compliant
- All changes must follow QMS change control process
```

### pyproject.toml

```toml
[project]
name = "medical-device-software"
version = "2.0.0"
description = "Medical Device Software for patient monitoring"
readme = "README.md"
requires-python = ">=3.12"

dependencies = [
  "pydicom>=2.4.4",
  "pynetdicom>=2.0.2",
]

[dependency-groups]
dev = [
  "mypy>=1.19.0",
  "pre-commit>=4.5.0",
  "pydoclint>=0.8.3",
  "pylint>=4.0.4",
  "pytest",
  "pytest-html>=4.1.1",
  "ruff>=0.14.8",
]
```

### CI Workflow Enhancement

Add verification steps:

```yaml
- name: Security Scan
  run: |
    uv run pip-audit

- name: Generate SBOM
  run: |
    uv export --format requirements-txt > sbom.txt

- name: Archive Artifacts
  uses: actions/upload-artifact@v4
  with:
    name: verification-artifacts
    path: |
      verification-history/
      sbom.txt
```

## Example 4: Data Science Project

**Use Case:** A data science project with ML dependencies.

### pyproject.toml

```toml
[project]
name = "ml-prediction-service"
version = "0.1.0"
description = "Machine learning prediction service"
readme = "README.md"
requires-python = ">=3.12"

dependencies = [
  "numpy>=1.24.0",
  "pandas>=2.0.0",
  "scikit-learn>=1.3.0",
  "fastapi>=0.104.0",
]

[dependency-groups]
training = [
  "jupyter>=1.0.0",
  "matplotlib>=3.7.0",
  "seaborn>=0.12.0",
]

dev = [
  "mypy>=1.19.0",
  "pre-commit>=4.5.0",
  "pydoclint>=0.8.3",
  "pylint>=4.0.4",
  "pytest",
  "pytest-html>=4.1.1",
  "ruff>=0.14.8",
]
```

### Makefile

```makefile
.PHONY: train model-serve

train:
	uv run python scripts/train_model.py

model-serve:
	uv run uvicorn api.main:app --reload
```

## Example 5: Custom Tool Configuration

### Stricter Type Checking

```toml
[tool.mypy]
python_version = "3.12"
strict = true  # Enable all strict checks
warn_return_any = true
warn_unused_configs = true
```

### Custom Ruff Rules

```toml
[tool.ruff]
line-length = 88  # Black-compatible

lint.select = [
  "E",   # pycodestyle errors
  "F",   # pyflakes
  "I",   # isort
  "B",   # flake8-bugbear
  "UP",  # pyupgrade
  "SIM", # flake8-simplify
  "RUF", # Ruff-specific rules
]

lint.ignore = [
  "E501",  # Line too long (handled by formatter)
]
```

### Custom Pylint Configuration

```toml
[tool.pylint.'MESSAGES CONTROL']
disable = [
  "missing-function-docstring",
  "missing-module-docstring",
  "too-few-public-methods",
  "too-many-arguments",  # Add this
]

[tool.pylint.format]
max-line-length = 100
```

## Tips for Customization

1. **Start Simple**: Begin with minimal customization and add complexity as needed
2. **Keep It Generic**: If you find yourself making the same changes across projects, consider proposing them to the template
3. **Document Changes**: Keep notes on why you customized certain parts
4. **Test Thoroughly**: After customization, run `make check` to ensure everything works
5. **Version Control**: Commit customization changes incrementally for easier rollback

## Contributing Examples

If you have a useful customization example, consider contributing it:

1. Fork the repository
2. Add your example to this file
3. Submit a pull request

Your example should:
- Be clear and well-documented
- Show a real-world use case
- Include complete, working configurations

