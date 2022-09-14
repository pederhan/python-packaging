# PDM

- [x] Supports `pyproject.toml`]
- [x] PEP 621 compliant
- [x] Virtual Environment management
- [x] Dependency resolution
- [x] Locking/pinning
- [x] Building
- [ ] Reproducible builds[^1]
- [x] Publishing

| Stat            | Value                                   |
|-----------------|-----------------------------------------|
| First published | 2021-04-12                              |
| Last updated    | 2022-08-30                              |
| GitHub stars    | 3,100                                   |
| GitHub repo     | [https://github.com/pdm-project/pdm](https://github.com/pdm-project/pdm)     |


PDM is an all-in-one tool in the vein of Poetry, but with a tighter PEP specfications compliance. It is able to resolve dependencies, lock them, and create a virtual environment with the correct dependencies installed. It is also able to export its dependencies and metadata as `requirements.txt` and `setup.py` in cases where this is required - though most of the time one will be building wheels and source distributions instead of manually exporting these files.

## PEP Compliance

Unlike Poetry, PDM seeks to be PEP compliant, and uses the `[project]` table to store project metadata and dependencies.

Furthermore, it includes opt-in support for the not-yet-accepted PEP 581, which introduces the `__pypackages__` directory (similar to `node_modules`) for storing dependencies.

In general, it seems like PDM seeks to be as PEP compliant as possible, and it is a good choice when working with other tools that require strict `pyproject.toml` PEP compliance.

## Project Metadata

PDM uses the standard `[project]` table to store project metadata. This means that the project metadata can be read without installing PDM when working with the package source code. 

```toml
# pyproject.toml

[build-system]
requires = ["pdm-pep517"]
build-backend = "pdm.pep517.api"

[project]
name = "my-package"
version = "1.0.0"
description = ""
authors = [{ name = "Author Name", email = "user@example.com" }]
requires-python = ">=3.10"
license = { text = "MIT" }
readme = "README.md"
keywords = ["keyword1", "keyword2"]
classifiers = [
    "Topic :: Software Development :: Build Tools",
    "Topic :: Software Development :: Libraries :: Python Modules"
]

[project.urls]
homepage = "https://example.com"
repository = "https://github.com/user/example"
documentation = "https://example.com/docs"
```

## Dependency Specification

Dependencies are specified in the `[project]` table under the `dependencies`and `optional-dependencies` keys, according to the PEP 621 specification.

Optional dependencies/extras are added via the CLI option `-G/--group`:

```bash
pdm add -G dev pytest
```

These are then exported to the generated `setup.py` as `extras_require`, meaning they can be installed with `pip install my-package[dev]`.

```toml
# pyproject.toml

# ...

[project]
# ...
dependencies = [
    "httpx",
    "fastapi",
]
[project.optional-dependencies]
dev = ["black", "mypy", "pytest", "pre-commit"]
docs = ["mkdocs", "mkdocs-material"]
```

If one wishes to not export these extras to `setup.py`, they can use the `--d/--dev` flag:

```bash
pdm add --dev pytest
```

This adds the dependency under the `[tool.pdm.dev-dependencies]` table, which is not exported to `setup.py`.

```toml
# pyproject.toml

# ...

[project]
# ...
dependencies = [
    "httpx",
    "fastapi",
]

[tool]
[tool.pdm]
[tool.pdm.dev-dependencies]
dev = [
    "pytest>=7.1.3",
]
```

## Extras

## Usage with Other Tools

Although PDM includes its own build system tool, `pdm-pep517`, it supports a multitude of build tools, including `setuptools`, `flit`, and `hatch`. Unlike Poetry, it is not tied a to specific proprietary build tool.

## Negatives

The developer is a Chinese resident and works for Crypto.com[^2]. Double whammy. However, the project is open source and the developer is active on GitHub. The project is also relatively new, so it's hard to tell how it will develop in the future.

## Summary

PDM is a robust and powerful tool that is PEP compliant and supports a multitude of build systems, which means it's not tied to a specific properietary build system like Poetry. Its CLI is also very intuitive and easy to use.

PDM is regularly updated, and the developer actively communicates on Twitter and GitHub.

The major drawbacks are its relative newness, its lack of popularity compared to Poetry, and the fact that the developer is a Chinese resident and works for Crypto.com. However, it seems unlikely that a dependency management and publishing tool should be subject to any political or legal restrictions as a result of the developer's nationality.

PDM is a tool that is worth keeping an eye on, and it's worth trying out if you're looking for a PEP compliant all-in-one dependency and project management tool that supports a multitude of build systems.

Is it ready for production? It seems so, but it needs to be tested more thoroughly.

[^1]: It is unclear whether the default build system `pdm-pep517` supports reproducible builds, but other supported build systems such as `flit` and `hatch` do.

[^2]: Spotted in the bio on [https://dev.to/frostming/a-review-pipenv-vs-poetry-vs-pdm-39b4](https://dev.to/frostming/a-review-pipenv-vs-poetry-vs-pdm-39b4). This information might be out-of-date.