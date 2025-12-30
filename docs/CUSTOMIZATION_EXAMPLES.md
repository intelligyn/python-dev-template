# Customization Examples

This document provides examples of how to customize the template for different project types.

## Example 1: Simple Python Library

**Use Case:** A standalone Python library with minimal dependencies.

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
```

## Example 2: Multi-Service Application

**Use Case:** An application with multiple services, each with different dependencies.

```toml
[project]
name = "my-microservices-app"
version = "1.0.0"
description = "Microservices application with API and worker services"
readme = "README.md"
requires-python = ">=3.12"

dependencies = [
  "pydantic>=2.5.0",
  "python-dotenv>=1.0.0",
]

[dependency-groups]
api = [
  "fastapi>=0.104.0",
  "uvicorn[standard]>=0.24.0",
]

worker = [
  "celery>=5.3.0",
  "redis>=5.0.0",
]
```

**Makefile customization:**

```makefile
SERVICES := api worker scheduler
```

## Example 3: Regulated Software (Medical Device)

**Use Case:** Software requiring regulatory compliance.

**Documentation customization:**

```markdown
**Regulatory Context:** EU MDR / IEC 62304
**Applicable System:** Medical Device Software v2.0

## 10. Constraints
- No PHI stored or processed locally
- All changes must follow QMS change control process
```

**CI workflow enhancement:**

```yaml
- name: Security Scan
  run: uv run pip-audit

- name: Generate SBOM
  run: uv export --format requirements-txt > sbom.txt
```

## Custom Tool Configuration

### Stricter Type Checking

```toml
[tool.mypy]
strict = true  # Enable all strict checks
```

### Custom Ruff Rules

```toml
[tool.ruff]
line-length = 88  # Black-compatible

lint.select = [
  "E", "F", "I", "B", "UP", "SIM", "RUF",
]
```

## Tips

1. **Start Simple**: Begin with minimal customization
2. **Test Thoroughly**: Run `make check` after customization
3. **Document Changes**: Keep notes on why you customized certain parts

For more detailed examples, see the [Usage Guide](USAGE.md).
