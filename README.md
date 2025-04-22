# Python Package Template

A modern Python package template using [Copier](https://copier.readthedocs.io/en/stable/) for project scaffolding.

## Features

- Modern Python packaging with `pyproject.toml`
- Docker support with multi-stage builds
- Clean project structure
- Automatic module and package name generation

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

### Useful Links

- [Copier Documentation](https://copier.readthedocs.io/en/stable/)
- [Copier GitHub Repository](https://github.com/copier-org/copier)
- [Jinja2 Template Documentation](https://jinja.palletsprojects.com/en/3.1.x/templates/)

## Contributing

If you'd like to contribute to this template, please feel free to submit a pull request or open an issue.

## License

This template is available under the MIT License.
