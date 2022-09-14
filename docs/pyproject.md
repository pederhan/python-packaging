# pyproject.toml

`pyproject.toml` is the modern replacement for `setup.py`,`setup.cfg`, `requirements.txt` and `MANIFEST.in`. It is a file that contains metadata about the project, as well as a list of build dependencies,build instructions, and tool configuration.

It is a TOML configuration file, which means it does not present a risk of arbitrary code execution like `setup.py`<sup>[n](https://moyix.blogspot.com/2022/09/someones-been-messing-with-my-subnormals.html#:~:text=I%20actually%20started,home%20directory.%20Convenient!)</sup> when reading project metadata. 

The file can specify build dependencies without running any Python code; it is purely declarative. This is important because it allows the build dependencies to be specified in a way that is compatible with all Python packaging tools, including tools that do not use `setuptools`.

The `pyproject.toml` file unifies multiple facets of project packaging and development. It is a single source of truth for the project metadata, build dependencies, build instructions, as well as tool configuration.

The following sections are based on [PEP 517](https://peps.python.org/pep-0517/), [PEP 518](https://peps.python.org/pep-0518/) and [PEP 621](https://peps.python.org/pep-0621/), which together make up the PEPs  that define `pyproject.toml`.


## Build system specification

```toml
# pyproject.toml

[build-system]
requires = ["setuptools>=42", "wheel"]
build-backend = "setuptools.build_meta"

# ...
```



## Metadata specification

```toml
# pyproject.toml

# ...

[project]
name = "my-package"
version = "0.1.0"
description = "A short description of my package"
authors = [
    {name = "Author Name", email = "user@example.com"},
]
readme = "README.md"
requires-python = ">=3.6"
license = {file = "LICENSE"}
classifiers = [
    "Development Status :: 3 - Alpha",
    "Intended Audience :: Developers",
    "License :: OSI Approved :: MIT License",
    "Programming Language :: Python :: 3",
    "Programming Language :: Python :: 3.6",
    "Programming Language :: Python :: 3.7",
    "Programming Language :: Python :: 3.8",
    "Programming Language :: Python :: 3.9",
]
keywords = ["keyword1", "keyword2", "keyword3"]
```

The `[project]` table contains the project metadata for the project. The full specification for the project metadata can be found [here](https://packaging.python.org/en/latest/specifications/declaring-project-metadata/).


## Dependency specification

```toml
# pyproject.toml

# ...

[project]
# ...
dependencies = [
    "package1",
    "package2>=2.0",
    "package3[extra1,extra2]",
    "package4==0.4.0; python_version<'3.7'"
]

optional-dependencies = {
    "extra1": ["package5"],
    "extra2": ["package6"],
}
```

This is the standard dependency specification when building a project with `setuptools`. The full specification for the dependency specification can be found [here](https://packaging.python.org/en/latest/specifications/declaring-project-metadata/#dependencies-optional-dependencies).

Other build tools usually use their own dependency specification for optional dependencies (and sometimes core dependencies), but they will still ultimately live inside the `pyproject.toml` file.


## Tool configuration

`pyproject.toml` is able to unify the configuration options for a multitude of tools including build tools, linters, formatters, and more. This allows the configuration for all of these tools to be specified in a single file, as opposed to having one file for each tool. This makes it easier to manage tool configuration.

Examples of tools that support `pyproject.toml` include:

* Pytest
* Coverage.py
* Tox
* MyPy
* Black
* Flake8
* And more...

Example:
    
```toml
# pyproject.toml

# ...

[tool.isort]
profile = "black"

[tool.pytest.ini_options]
asyncio_mode = "auto"

[tool.mypy]
strict = true
exclude = ["tests/"]
```

## Full pyproject.toml Example

The following shows a full example of a `pyproject.toml` file that contains all of the above sections.


```toml
```