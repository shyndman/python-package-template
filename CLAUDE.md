# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Copier template for generating modern Python packages. The template creates projects with pyproject.toml configuration, UV for dependency management, pyenv for Python version management, and Docker support.

## Common Commands

- **Create a new project from this template**: `copier copy gh:shyndman/python-package-template path/to/new/project`
- **Update existing project from template**: `copier update` (run in the generated project directory)
- **Preview template generation**: `copier copy --pretend gh:shyndman/python-package-template path/to/new/project`
- **Generate project with defaults**: `copier copy --defaults gh:shyndman/python-package-template path/to/new/project`

## Template Architecture

### Core Files Structure
- `copier.yml`: Template configuration, questions, and post-generation tasks
- `template/`: Contains all Jinja2 template files (`.j2` suffix)
- `template/helpers/`: Jinja2 include files for default value generation

### Template Variables and Defaults
- `project_name`: User-provided project name
- `module_name`: Auto-generated from project_name (snake_case conversion)
- `package_name`: Auto-generated from module_name (kebab-case conversion)
- `python_version`: Default 3.11
- Author details: Default to Scott Hyndman's information
- `include_ci_workflow`: Include CI workflow with Ruff, Pyright, and pytest (default: true)
- `include_docker_workflow`: Include Docker build and publish workflow (default: false)
- `launch_claude_code`: Launch Claude Code after project generation (default: true)
- `claude_design_session`: Have Claude help design project README and description (default: true)

### Generated Project Features
- Modern Python packaging with pyproject.toml
- UV integration for fast dependency management
- Pyenv integration with `.python-version` file
- Ruff configuration for linting and formatting (100 char line, 2-space indent)
- Pyright configuration for type checking
- Docker multi-stage build support
- Pre-commit and direnv integration (if available)
- Optional GitHub Actions workflows:
  - CI workflow with Ruff, Pyright, and pytest (with GitHub annotations)
  - Docker build and publish to ghcr.io
- Basic test suite with import and version tests
- Claude Code integration for seamless development experience

### Post-Generation Tasks
The template automatically:
1. Installs specified Python version via pyenv
2. Initializes git repository
3. Installs UV package manager
4. Syncs dependencies with `uv sync --all-extras --all-groups --no-binary`
5. Sets up pre-commit hooks (if available)
6. Allows direnv configuration (if available)
7. Launches Claude Code with optional design session to help create README and package description

### Jinja2 Template Helpers
- `template/helpers/module-default.j2`: Converts project_name to snake_case
- `template/helpers/package-name.j2`: Converts module_name to kebab-case

## Development Notes

- Template files use `.j2` suffix for Jinja2 templating
- Helper templates are excluded from generated projects via `_exclude` configuration
- The `src` directory structure uses `{{module_name}}` placeholder for dynamic module naming
- Post-generation tasks handle environment setup automatically