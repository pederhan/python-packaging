# Hatch

- [x] Supports `pyproject.toml`
- [x] PEP 621 compliant
- [x] Virtual Environment management
- [ ] Dependency resolution
- [ ] Locking/pinning
- [x] Building
- [x] Reproducible builds
- [x] Publishing

| Stat            | Value                                   |
|-----------------|-----------------------------------------|
| First published | 2018-12-29                              |
| Last updated    | 2022-08-28                              |
| GitHub stars    | 3,000                                   |
| GitHub repo     | https://github.com/pypa/hatch           |


Hatch is a "modern, extensible Python project manager."[^1] It has support for creating projects, building and publishing packages, and managing virtual environments. It utilizes `pyproject.toml` and is PEP 621 compliant. It does not, however, contain a dependency resolver or any way to add dependencies via its CLI.

Hatch features a number of ways to control project generation using configurable templates. These templates include automatically adding license files, READMEs, test directories and even GitHub actions workflows.

## PEP Compliance

Hatch utilizes `pyproject.toml` and is PEP 621 compliant.

## Project Metadata

```toml
# pyproject.toml

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my-cool-django-app"
version = "42"
# ...
```

## Dependency Specification

Uses standard [PEP 621](https://www.python.org/dev/peps/pep-0621/) dependency specification. 

```toml
# pyproject.toml

# ...

[project]
# ...
dependencies = ["django"]

[project.optional-dependencies]
dev = ["pytest"]
```

## Usage with Other Tools



## Negatives

Hatch does not have a dependency resolver or any way to add dependencies via its CLI. It requires a manual workflow of manually adding dependencies to `pyproject.toml`. In this regard, it's simply a modern replacement for existing workflows where manual editing of `setup.py` and `requirements.txt` was required.

## Summary

Hatch is a mature and well-supported tool for building and publishing Python projects. It is able to read from `pyproject.toml` and is PEP 621 compliant. It is a project management tool as well as a build system, and is able to create reproducible builds and publish packages to PyPI. 

Its configuration options and templates enable powerful workflows that are useful when creating new projects.

In many ways Hatch can do everything that `Poetry` and `PDM` can, except for dependency resolution. If you are ok with specifying dependencies manually, Hatch is an excellent tool.