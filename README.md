# Python Package Template

A modern Python package template using [Copier](https://copier.readthedocs.io/en/stable/) for project scaffolding.

## Features

- Modern Python packaging with `pyproject.toml`
- Pyenv integration for Python version management
- UV integration for fast dependency management
- Docker support with multi-stage builds
- Clean project structure
- Automatic module and package name generation using Jinja templates
- Automated project setup with Git, virtual environment, and development dependencies
- Template configuration with `_subdirectory: template` and `_templates_suffix: .j2`
- Exclusion of helper templates from the generated project

## Template Defaults

This template provides the following defaults:

| Variable | Description | Default |
|----------|-------------|---------|
| `project_name` | Your project's name | (user input) |
| `module_name` | Python module name | `project_name` converted to snake_case |
| `package_name` | Python package name | `module_name` with underscores converted to hyphens |
| `python_version` | Python version to use | 3.11 |
| `user_name` | Author name | Scott Hyndman |
| `user_email` | Author email | scotty.hyndman@gmail.com |
| `github_user` | GitHub username | shyndman |

## Generated Project Structure

```
your-package-name/
├── Dockerfile
├── pyproject.toml
├── README.md
└── src/
    └── your_module_name/
        └── __init__.py
```

## Copier Cheatsheet

### Creating a New Project

To create a new project from this template:

```bash
# Install Copier if you don't have it
pip install copier

# Create a new project
copier copy gh:shyndman/python-package-template path/to/your/new/project
```

### Updating an Existing Project

If the template has been updated and you want to apply those updates to your project:

```bash
# Navigate to your project directory
cd path/to/your/project

# Update your project from the template
copier update
```

### Common Copier Commands

| Command | Description |
|---------|-------------|
| `copier copy <template> <destination>` | Create a new project from a template |
| `copier update` | Update an existing project with template changes |
| `copier recopy` | Regenerate a project, discarding any changes |
| `copier copy --data=answers.yml <template> <destination>` | Create a project using predefined answers |
| `copier copy --defaults <template> <destination>` | Create a project using default values |
| `copier copy --pretend <template> <destination>` | Preview what would be generated without making changes |

## Pyenv Integration

This template integrates with [pyenv](https://github.com/pyenv/pyenv) for Python version management. When creating a project, you'll be prompted to select a Python version to use with pyenv.

### How it works

The template will:

1. Install the selected Python version using pyenv if it's not already installed
2. Create a `.python-version` file with your selected Python version
3. Set the local Python version for the project using `pyenv local`

The default Python version is set to 3.11, but you can choose any version supported by pyenv during project creation.

### Common Pyenv Commands

| Command | Description |
|---------|-------------|
| `pyenv install <version>` | Install a specific Python version |
| `pyenv versions` | List all installed Python versions |
| `pyenv local <version>` | Set the local Python version for the current directory |
| `pyenv global <version>` | Set the global Python version |
| `pyenv which python` | Show the full path to the current Python executable |

## UV Integration

This template uses [UV](https://github.com/astral-sh/uv), a fast Python package installer and resolver written in Rust. When you create a project with this template, the following UV-related tasks are automatically performed:

1. UV is installed if not already present on your system
2. Dependencies are synchronized with `uv sync --all-extras --all-groups --no-binary`

This ensures that all dependencies are properly installed and managed using UV's fast resolver.

### Common UV Commands

| Command | Description |
|---------|-------------|
| `uv venv` | Create a virtual environment |
| `uv pip install -e .` | Install the package in development mode |
| `uv lock` | Create or update the lockfile |
| `uv add <package>` | Add a package to dependencies |
| `uv add --dev <package>` | Add a package to development dependencies |
| `uv run <script>` | Run a script in the virtual environment |
| `uv sync` | Sync the environment with the lockfile |

## Jinja Templates in This Project

This template uses Jinja2 for templating. Here's how Jinja includes are used in this project:

### Module Name Default

The default value for `module_name` is generated using a Jinja include:

```yaml
module_name:
    type: str
    help: What is your Python module name?
    default: "{%- include 'template/helpers/module-default.j2' -%}"
```

The included template (`module-default.j2`) converts the project name to snake_case:

```jinja
{#- For simplicity ... -#}
{{ project_name|lower|replace(' ', '_') }}
```

### Package Name Default

Similarly, the default value for `package_name` is generated using a Jinja include:

```yaml
package_name:
    type: str
    help: What is your Python package name?
    default: "{%- include 'template/helpers/package-name.j2' -%}"
```

The included template (`package-name.j2`) converts the module name to kebab-case:

```jinja
{#- For simplicity ... -#}
{{ module_name|lower|replace('_', '-') }}
```

### Useful Links

- [Copier Documentation](https://copier.readthedocs.io/en/stable/)
- [Copier GitHub Repository](https://github.com/copier-org/copier)
- [Jinja2 Template Documentation](https://jinja.palletsprojects.com/en/3.1.x/templates/)
- [Pyenv GitHub Repository](https://github.com/pyenv/pyenv)
- [Pyenv Commands](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md)
- [UV Documentation](https://docs.astral.sh/uv/)
- [UV GitHub Repository](https://github.com/astral-sh/uv)

## Contributing

If you'd like to contribute to this template, please feel free to submit a pull request or open an issue.

## License

This template is available under the MIT License.
