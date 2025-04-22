# Python Package Template

A modern Python package template using [Copier](https://copier.readthedocs.io/en/stable/) for project scaffolding.

## Features

- Modern Python packaging with `pyproject.toml`
- Pyenv integration for Python version management
- UV integration for fast dependency management
- Docker support with multi-stage builds
- Clean project structure
- Automatic module and package name generation
- Automated project setup with Git, virtual environment, and development dependencies

## Template Defaults

This template provides the following defaults:

| Variable | Description | Default |
|----------|-------------|---------|
| `project_name` | Your project's name | (user input) |
| `module_name` | Python module name | `project_name` converted to snake_case |
| `package_name` | Python package name | `module_name` with underscores converted to hyphens |
| `python_version` | Python version to use | (user input) |
| `user_name` | Author name | (user input) |
| `user_email` | Author email | (user input) |
| `github_user` | GitHub username | (user input) |

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

This template integrates with [pyenv](https://github.com/pyenv/pyenv) for Python version management. When creating a project, you'll be prompted to select a Python version from those **dynamically detected** from your pyenv installation.

### How it works

The template uses the [copier-templates-extensions](https://github.com/copier-org/copier-templates-extensions) package with its `ContextHookExtension` to dynamically fetch Python versions from pyenv. The implementation:

1. Uses a Python function (`get_python_versions`) that can be imported directly in the YAML template
2. Checks if pyenv is installed on your system
3. If it is, fetches the list of available Python versions using `pyenv versions --bare`
4. Filters out system Python and non-CPython versions (like PyPy)
5. Returns the list of Python versions as choices for the `python_version` variable

This approach follows the recommended pattern from the [copier-templates-extensions documentation](https://github.com/copier-org/copier-templates-extensions#context-hook-extension).

The template will then:

1. Create a `.python-version` file with your selected Python version
2. Set the local Python version for the project using `pyenv local`
3. Use the selected Python version when creating the virtual environment

If pyenv is not installed, the template will fall back to a standard list of Python versions (3.8, 3.9, 3.10, 3.11, 3.12) and you'll receive instructions on how to install pyenv and set up your project with the correct Python version.

### Common Pyenv Commands

| Command | Description |
|---------|-------------|
| `pyenv install <version>` | Install a specific Python version |
| `pyenv versions` | List all installed Python versions |
| `pyenv local <version>` | Set the local Python version for the current directory |
| `pyenv global <version>` | Set the global Python version |
| `pyenv which python` | Show the full path to the current Python executable |

## UV Integration

This template uses [UV](https://github.com/astral-sh/uv), a fast Python package installer and resolver written in Rust. When you create a project with this template, the following UV-related tasks are automatically performed (if UV is installed):

1. A virtual environment is created with `uv venv --python <selected_version>`
2. The package is installed in development mode with `uv pip install -e .`
3. A lockfile is created with `uv lock`
4. Development dependencies are installed with `uv add --dev`

If UV is not installed, you'll receive instructions on how to install it and set up your project manually.

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
