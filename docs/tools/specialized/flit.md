# Flit

- [x] Supports `pyproject.toml`
- [ ] Virtual Environment management
- [ ] Dependency resolution
- [ ] Locking/pinning
- [x] Building[*](https://flit.pypa.io/en/latest/rationale.html#:~:text=If%20your%20package%20needs%20a%20build%20step%2C%20you%20won%E2%80%99t%20be%20able%20to%20use%20Flit.)
- [x] Reproducible builds
- [x] Publishing

| Stat            | Value                                   |
|-----------------|-----------------------------------------|
| First published | 2015-03-16                              |
| Last updated    | 2022-02-23                              |
| GitHub stars    | 1,800                                   |
| GitHub repo     | https://github.com/pypa/flit            |



Flit is a tool used to build packages deterministically and reproducibly. It is able to build and publish packages using `pyproject.toml`. It is not able to resolve dependencies, lock them, or create virtual environments. Flit is an official PyPA project, and is used by certain large projects such as [`FastAPI`](https://github.com/tiangolo/fastapi). 

Given that it does not support dependency resolution, it 

## PEP Compliance

Flit is compliant with [PEP 517](https://www.python.org/dev/peps/pep-0517/), [PEP 518](https://www.python.org/dev/peps/pep-0518) and [PEP 621](https://www.python.org/dev/peps/pep-0621/).
## Project Metadata

Project metadata is specified in the `[project]` table in the `pyproject.toml` file, as specified by PEP 621.


```toml
# pyproject.toml

[build-system]
requires = ["flit_core >=3.2,<4"]
build-backend = "flit_core.buildapi"

[project]
name = "foobar"
authors = [{name = "Sir Robin", email = "robin@camelot.uk"}]
dynamic = ["version", "description"]

[project.urls]
Home = "https://github.com/sirrobin/foobar"

```

Example from the official [documentation](https://flit.pypa.io/en/stable/).

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

Flit can be used in conjunction with other tools that complements its functionality such as `pip-tools`. It can also be used as a build backend for `PDM`.

## Negatives

Flit is not able to build packages that require a build step, such as those that use Cython or C extensions. 

Not very actively maintained, with the last release being in February 2022.

## Summary

Due its relatively inactive development, [Hatch](hatch.md) is likely a better choice over Flit with regards to future-proofing. However, Flit is a good choice right now for those who are looking for a simple tool that is able to build and publish packages deterministically and reproducibly.