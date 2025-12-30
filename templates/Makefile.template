SHELL := /bin/bash
.SHELLFLAGS := -euo pipefail -c
COMPOSE := docker compose

# Add your compose files and services
DEV_FILES  := -f compose.dev.yml
PROD_FILES := -f compose.prod.yml

# Add your service names here
SERVICES := {service1} {service2} test

.DEFAULT_GOAL := help

# Service validation helper (optional)
define assert-service
	@if ! printf "%s\n" "$(SERVICES)" | tr ' ' '\n' | grep -qx "$*"; then \
		echo "ERROR: Unknown service '$*'"; \
		echo "Allowed services: $(SERVICES)"; \
		exit 1; \
	fi
endef

.PHONY: help check

help:
	@echo "Quality checks:"
	@echo "  make check                  Run CI-equivalent checks locally"
	@echo ""
	@echo "Add your project-specific targets here"

# -----------------
# QUALITY / CI mirror
# -----------------

check:
	uv sync --group dev --frozen
	uv run pre-commit run -a
	mkdir -p verification-history
	uv run pytest

# Add your project-specific targets below
# Examples:
# - Docker compose targets
# - Service-specific commands
# - Deployment targets

