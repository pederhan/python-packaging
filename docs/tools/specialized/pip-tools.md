
# pip-tools

- [x] Supports `pyproject.toml`
- [x] PEP 621 compliant
- [ ] Virtual Environment management
- [ ] Dependency resolution*
- [x] Locking/pinning
- [ ] Building
- [ ] Reproducible builds
- [ ] Publishing

| Stat            | Value                                   |
|-----------------|-----------------------------------------|
| First published | 2012-09-26                              |
| Last updated    | 2022-06-30                              |
| GitHub stars    | 6,200                                   |
| GitHub repo     | https://github.com/jazzband/pip-tools   |


https://pip-tools.readthedocs.io/en/latest/

pip-tools is a tool that is able to pin dependencies and generate `requirements.txt` files. It is not able to build packages, or publish them. It is a useful tool for pinning dependencies in order to ensure deterministic builds. `pip-tools` can read from `pyproject.toml`.

`pip-tools` is best used in conjunction with tools such as `Flit` and `Hatch`, which handle the building and publishing of packages.


* Only pins packages and creates `requirements.txt`, `dev-requirements.txt`, etc.
* Supports pyproject.toml

## PEP Compliance

## Project Metadata

N/A

## Dependency Specification

Uses standard [PEP 621](https://www.python.org/dev/peps/pep-0621/) dependency specification. 

Example from `pip-tools`'s documentation:

```toml
# pyproject.toml

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my-cool-django-app"
version = "42"
dependencies = ["django"]

[project.optional-dependencies]
dev = ["pytest"]
```

## Extras

Able to create pinned `dev-requirements.txt`, `test-requirements.txt`, etc. for use with `pip install -r` from `pyproject.toml`.

## Usage with Other Tools

`pip-tools` is best used in conjunction with tools such as `Flit` and `Hatch`, which handle the building and publishing of packages. It is not a replacement for a full-featured dependency resolver such as `Poetry` or `PDM`.

## Negatives

The tool is limited, and is not a full replacement for any of the other tools mentioned here. This is not a negative per se, but it is important to understand what the tool is and is not capable of doing.

## Summary

This is a tool best used in conjunction with a tool such as `Hatch` or `flit`. `pip-tools` can handle the pinning of dependencies specified in `pyproject.toml`, while `Hatch` and `flit` can handle the building and publishing of packages. It is a bit more of a manual process than the all-in-one tools, but it is a useful tool for pinning dependencies in order to ensure deterministic builds, if that is a requirement for your project.