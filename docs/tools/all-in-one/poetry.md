# Poetry

- [x] Supports `pyproject.toml`
- [ ] PEP 621 compliant
- [x] Virtual Environment management
- [x] Dependency resolution
- [x] Locking/pinning
- [x] Building
- [ ] Reproducible builds
- [x] Publishing


| Stat            | Value                                   |
|-----------------|-----------------------------------------|
| First published | 2018-02-28                              |
| Last updated    | 2022-08-31                              |
| GitHub stars    | 21,700                                  |
| GitHub repo     | [https://github.com/python-poetry/poetry](https://github.com/python-poetry/poetry) |


## Introduction

Poetry is the most popular Python packaging tool in recent years. It is a tool that, like `Pipenv`, combines `pip` and `virtualenv` to automatically create virtual environments, resolve dependencies, and install them. Furthermore, it is also able to build packages and publish them to PyPI. It is an all-in-one tool that is able to do everything that `Pipenv` can do, and more. 

Poetry can build Python source and wheel distributions and publish them to PyPI. The distributions it builds include automatically generated metadata, such as `PKG-INFO` and `setup.py` files, which ensure compatibility with older versions of `pip`.

It is also able to generate a `requirements.txt` file for use with installations that do not require packaging, such as Docker images.

Its performance is better than that of `Pipenv`, but not as fast as `PDM`.[^1] Speed of tooling is not paramount, as it is only run occasionally, but it is still worth noting.


## PEP Compliance

Poetry supports `pyproject.toml`, but does not fully implement PEP 621. It is able to read the `pyproject.toml` file, but it uses its own dependency specification, which is in turn built using the `poetry-core` build system (not `setuptools`). 

It stores all project metadata under `[tool.poetry[.key]]` tables in the `pyproject.toml` file. The key names are for the most part identical to the PEP621 specification. To specify optional (non-distributed) dependencies Poetry uses something called "dependency group" tables in the form of `[tool.poetry.group.<groupname>.dependencies]`.

Distributed optional dependencies are specified in the `[tool.poetry.extras]` table. The key names are the same as the group names, and the values are lists of dependencies. See [Extras](#extras) for more information

## Project Metadata

Poetry's equivalent of the `[project]` table is `[tool.poetry]`. As a result of this non-standard approach, the project metadata cannot be read without installing Poetry when working with the package source code. 

However, this information is included in the generated `setup.py` in the distributions built by Poetry. This means that `pip` is able to read the project metadata natively when installing package distributions built with Poetry. The end user will not notice any difference in the installation process.


```toml
# pyproject.toml
[build-system]
requires = ["poetry-core>=1.0.0"]
build-backend = "poetry.core.masonry.api"

[tool.poetry]
name = "my-package"
version = "0.1.0"
description = "A short description of my package"
license = "MIT"
authors = ["Author Name <user@example.com>"]
maintainers = [
    "Author Name <user2@example.com>",
    "Author Name <user3@example.com>",
]
readme = "README.md"
homepage = "https://example.com"
repository = "https://github.com/user/example"
documentation = "https://example.com/docs"
keywords = ["keyword1", "keyword2"]
classifiers = [
    "Topic :: Software Development :: Build Tools",
    "Topic :: Software Development :: Libraries :: Python Modules"
]
```

Poetry uses the non-standard fields `homepage`, `repository` and `documentation`, which are usually found under the `[project.urls]` table in PEP 621. 

See [PDM: Project Metadata](../pdm/#project-metadata) for more information on how this information is specified in accordance with the spec.

## Dependency Specification
Example of the Poetry dependency specification:

```toml
# pyproject.toml

# ...

[tool.poetry.dependencies]
requests = "^2.13.0"

[tool.poetry.group.test]
optional = true

[tool.poetry.group.test.dependencies]
pytest = "^7.0.0"
pytest-mock = "*"
```
The code snippet demonstrates specification of required dependencies as well as optional dependencies with dependency groups. 


Required dependencies are added via the following command:

```bash
poetry add requests
```

Optional dependencies (dependency groups) are added via the following command:

```bash
poetry add pytest --group test
```

The `optional` key in the `[tool.poetry.group.test]` table is used to specify whether the dependency group is optional or not.

Dependency groups are resolved and installed by default unless  `optional = true` is added to its group table. This can be a bit confusing, since one would expect dependencies specified apart from the `dependencies` table to be optional by default, but they are _NOT_. 

Dependency groups are simply a way to label dependencies, not a way to specify optional dependencies/extras in the same way as PEP 621. This is a bit confusing, but it is possible to use the `extras` table to specify extras.

When using the Poetry CLI, optional dependency groups can be installed using the `--with` flag. This can be useful in CI workflows, where you want certain optional packages for workflows such as documentation generation or testing, but you don't want to expose these dependencies as installable extras to the end user.

Example:

```bash
poetry install --with test
# required dependencies + testing dependencies are installed
pytest
```

## Extras

Dependency groups do not specify the traditional "extras" that can be installed with pip using the `package[extra]` syntax. Instead, extras are specified in the `[tool.poetry.extras]` table.

```toml
# pyproject.toml

[tool.poetry]
name = "my-package"

[tool.poetry.dependencies]
requests = "^2.13.0"
psycopg2 = { version = "^2.9", optional = true }
mysqlclient = { version = "^1.3", optional = true }

[tool.poetry.extras]
mysql = ["mysqlclient"]
pgsql = ["psycopg2"]
databases = ["mysqlclient", "psycopg2"]
```

To add a dependency as an extra, the following command is used:

```bash
poetry add --optional mysqlclient
```

The extra table then has to be manually updated to include the dependency and given an extra name. There is no CLI option for this.

When published, the package can then be installed with pip using the `[extra]` syntax:

```bash
pip install my-package[mysql]
```

## Usage with Other Tools

Poetry is an all-in-one-tool, and as such it is not necessary to use it with other tools. Also, given its non-compliant approach to project metadata, it is dubious whether it's possible to use it with other tools that require the project metadata to be available in the `pyproject.toml` file.<sup>[n]<sup>


## Negatives

With the release of version 1.2.0, the `Poetry` developers attempted to implement a random "brownout" that would cause `Poetry` installations to intermittently fail in CI when installed via a deprecated installation method. This affected previous versions as well, breaking people's CI builds of old versions with the installation script.[^2] This sort of action speaks poorly of the developers' judgement, and lessens the community's trust in them with regards to future changes. They walked back on the decision, but it still reflects poorly on the developers.

Furthermore, Poetry's lack of PEP compliance makes it more difficult to use alongside other tools.


## Summary

Poetry is a battle tested tool that is ever-growing in popularity. It is on track to eclipse `Pipenv` in popularity in under 5 years of existence. It supports the new `pyproject.toml` format, and is good choice for self-contained projects that do not rely on other packaging and project management tools. It has a robust CLI that is easy to use.

However, it is not compliant with PEP 621, and as such it is likely not possible to use it with other tools that require the project metadata to be available in the `pyproject.toml` file.[^3] This is a major drawback, and it is not clear whether the developers are willing to change this. Furthermore, it is unclear what the long term implications of this non-compliance will be.

As long as Poetry is the only packaging and dependency management tool used in a project, it is a good choice. However, if you want to use other packaging or build tools in conjunction with a dependency management tool, [PDM](pdm.md) might be a better option. 

<!-- Footnotes -->
[^1]: [A Review: Pipenv vs. Poetry vs. PDM](https://dev.to/frostming/a-review-pipenv-vs-poetry-vs-pdm-39b4). Note: this was written by the developer of PDM, so take it with a grain of salt.
[^2]: [refactor: rework deprecation of get-poetry.py to include CI brownout and restructured messaging](https://github.com/python-poetry/poetry/pull/6297)
[^3]: This claim has not been verified.