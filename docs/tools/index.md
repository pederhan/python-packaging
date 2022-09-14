# Packaging and Project Management Tools

Packaging Python projects and managing virtual environments has become a lot easier in recent years if you know what you're doing, but if you don't, it can tend to look like an ocean of tools doing a lot of the same things. This section aims to clarify the differences between the various tools and how they fit together.

The most popular tools are looked at in turn to evaluate their strengths and weaknesses, and how they can be used together. 

Skip to [TL;DR](#tldr) for a summary of the findings of this section.

Otherwise, head to the [next page](./all-in-one/index.md) for a more in-depth look at the various tools available for packaging and project management.

## TL;DR

What follows is a brief overview of the differences between the tools that are evaluated, as well as their popularity.

### Features


|           | pyproject.toml   | PEP 621 Compliant | Virtual Environment Management | Dependency Resolution | Pinning          | Building         | Reproducible Builds | Publishing       |
|-----------|------------------|-------------------|--------------------------------|-----------------------|------------------|------------------|---------------------|------------------|
| Poetry    | :material-check: |                   | :material-check:               | :material-check:      | :material-check: | :material-check: |                     | :material-check: |
| PDM       | :material-check: | :material-check:  | :material-check:               | :material-check:      | :material-check: | :material-check: | :material-minus:    | :material-check: |
| Pipenv    |                  |                   | :material-check:               | :material-check:      | :material-check: |                  |                     |                  |
| Flit      | :material-check: | :material-check:  |                                |                       |                  | :material-check: | :material-check:    | :material-check: |
| pip-tools | :material-check: | :material-check:  |                                |                       | :material-check: |                  |                     |                  |
| Hatch     | :material-check: | :material-check:  | :material-check:               |                       |                  | :material-check: | :material-check:    | :material-check: |

### Popularity

These graphs show the number of stars on GitHub for each tool in relation to publication time. The graphs are generated using [star-history](https://star-history.com/).

#### Comparison Using Absolute Publication Time

This chart shows the popularity of each tool in relation to its publication time. The x-axis shows the date of publication, and the y-axis shows the number of stars on GitHub.

[![Star History Chart](https://api.star-history.com/svg?repos=python-poetry/poetry,pdm-project/pdm,pypa/flit,pypa/hatch,pypa/pipenv&type=Date)](https://star-history.com/#python-poetry/poetry&pdm-project/pdm&pypa/flit&pypa/hatch&pypa/pipenv&Date)

#### Comparison Using Relative Publication Time

This chart shows the popularity of the tools in relation to the time since their publication. The x-axis shows number of years since publication, and the y-axis shows number of stars on GitHub.

[![Star History Chart](https://api.star-history.com/svg?repos=python-poetry/poetry,pdm-project/pdm,pypa/flit,pypa/hatch,pypa/pipenv&type=Timeline)](https://star-history.com/#python-poetry/poetry&pdm-project/pdm&pypa/flit&pypa/hatch&pypa/pipenv&Timeline)
    

## Unmentioned Tools

### Twine

### Enscons

Tool for building source distributions and wheels without `setuptools`, including ones that require C extensions.

PyPI link: https://pypi.org/project/enscons/


## Further Reading

Below are the most relevant PEPs with regards to modern packaging and building of Python projects with `pyproject.toml` as well as other relevant reading material.

### PEPs

* [PEP 518](https://www.python.org/dev/peps/pep-0518/) - Specifying Minimum Build System Requirements for Python Projects
* [PEP 621](https://www.python.org/dev/peps/pep-0621/) - Storing project metadata in pyproject.toml

### Relevant Links

* [Full list of modern packaging PEPs](https://peps.python.org/topic/packaging/#:~:text=Stufft-,Finished%20PEPs,-\(done%2C%20with%20a) (508 and onwards)
* [Clarifying PEP 518 (a.k.a. pyproject.toml)](https://snarky.ca/clarifying-pep-518/)
* [pyproject.toml specification](https://packaging.python.org/en/latest/specifications/declaring-project-metadata/)
* [TIL: pip-tools Supports pyproject.toml](https://hynek.me/til/pip-tools-and-pyproject-toml/)
* [Hypermodern Python](https://github.com/cjolowicz/cookiecutter-hypermodern-python)
---
1. Insofar as GitHub stars are a good metric to determine this.
2. https://pypi.org/project/darker/#:~:text=command%20line%20options-,Editor%20integration,-Many%20editors%20have
3. https://moyix.blogspot.com/2022/09/someones-been-messing-with-my-subnormals.html#:~:text=I%20actually%20started,home%20directory.%20Convenient!
