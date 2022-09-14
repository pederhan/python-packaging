
# Pipenv

- [ ] Supports `pyproject.toml`
- [ ] PEP 621 compliant
- [x] Virtual Environment management
- [x] Dependency resolution
- [x] Locking/pinning
- [ ] Building
- [ ] Reproducible builds
- [ ] Publishing


| Stat            | Value                          |
|-----------------|--------------------------------|
| First published | 2017-01-20                     |
| Last updated    | 2022-09-08                     |
| GitHub stars    | 23,300                         |
| GitHub repo     | [https://github.com/pypa/pipenv](https://github.com/pypa/pipenv) |


## Introduction

Pipenv was one of the first tools released to address the problems with Python packaging. It is a tool that combines `pip` and `virtualenv` into a single tool. It is able to resolve dependencies, lock them, and create a virtual environment with the correct dependencies installed. It is also able to generate a `requirements.txt` file for use with `pip`.

However, it is not able to build packages and does not support `pyproject.toml`. It is also famously slow when resolving numerous dependencies. <sup>[n](https://dev.to/frostming/a-review-pipenv-vs-poetry-vs-pdm-39b4)</sup>

Due to its lack of support for `pyproject.toml`, Pipenv can not be used in conjunction with the other tools in this section. It is also not able to build packages, so it is not possible to use it to build a package and then use another tool to publish it.

## Summary

Pipenv has been superceded by more modern tools such as Poetry and PDM both in terms of features and performance. New projects should probably not use this tool. It is only included here for completeness given its historical popularity.

