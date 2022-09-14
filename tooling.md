# Improving Development Tooling with pre-commit



## pre-commit

[pre-commit](https://pre-commit.com/) is a tool for running linting, formatting, and other one-off actions consistently across developer environments and in CI. This is a great way to ensure that code is formatted consistently and that it passes linting checks before it is committed, and can also be run in CI to ensure changes are consistent with the project's style. 

### How It Works

Central to pre-commit is the concept of "hooks" which are predefined scripts that are run against the code. There are many hooks available for pre-commit, and you can also write your own. pre-commit hooks come in the form a GitHub repository URL and an optional set of configuration options. The hooks are run in the order that they are defined in a `.pre-commit-config.yaml` file located in the repository root. 

Example configuration file:

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v3.2.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
  - repo: https://github.com/psf/black
    rev: 22.3.0
    hooks:
      - id: black
```

**Note:** pre-commit is not a replacement for a CI system. It is a tool for running checks and formatting on your code before it is committed. It can, however, be run in CI to ensure that the comitted code is consistent with the style of the project.

### Differences Between pre-commit and Git Hooks

[Git has support](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) for shell script hooks, but they are not as flexible as pre-commit hooks. For example, you can't run a Git pre-commit hook on a subset of files, or run a Git pre-commit hook on files that are not staged for commit. 

Furthermore, Git hooks are not run in CI unless they are distributed with the application, and even then, running them in CI is not a straight-forward process.

<!-- TODO: add paragraph/section about running all hooks on all files when adding pre-commit to ensure consistency across all files. Needs .gitblameignore. -->

<!-- NOTE: add section on pre-commit.ci? -->

### pre-commit hooks

Some of the most popular pre-commit hooks include:


intro
#### Black

**Categories:** Formatter, Linter

Black has become the [de-facto standard](https://star-history.com/#psf/black&hhatto/autopep8&google/yapf&Date) Python formatter in recent years<sup>1</sup>, and is even an official PSF project.

The problem with Black is that it runs on _entire files_, and as such it could cause a lot of headaches when small code changes have a large effect on the overall codebase due to Black formatting every modified file. One can partially circumvent this problem by formatting the entire codebase in a single commit and adding a `.gitblameignore` to ignore the blame info in the commit, but it's still not ideal (or is it?).

Black is available as a pre-commit hook.


#### Darker

**Categories:** Formatter, Linter

The solution to the problem of not formatting entire files is the formatter [darker](https://github.com/akaihola/darker).

From its description:

> This utility reformats and checks Python source code files. However, when run in a Git repository, it only applies reformatting and reports errors in regions which have changed in the Git working tree since the last commit.

Darker is a superset of Black, wihch means that it by default runs Black on only the changed regions of the file, but also supports formatting entire files just like Black. Its formatting style is identical to Black. Darker is available as a pre-commit hook and is also compatible with Visual Studio Code and PyCharm's formatter integrations.


#### Flake8

**Categories:** Linter

Flake8 is a linter that catches various errors and violations (documented [here](https://flake8.pycqa.org/en/latest/user/error-codes.html)). It catches things like unused imports, unused variables, duplicate assignments, and more. 

Source: https://github.com/PyCQA/flake8

#### Pylint

**Categories:** Linter

Pylint is a linter similar to Flake8 that catches some errors that Flake8 does not (and vice versa). 

Source: https://github.com/PyCQA/pylint

#### Mypy

**Categories:** Linter, Type Checker

MyPy is a static type checker for Python. 
It is available as a pre-commit hook.

Source: https://github.com/python/mypy


#### isort / reorder_python_imports

**Categories:** Formatter, Linter

isort and python_reorder_imports are tools that sort imports in Python files. They both ensure module imports are divided into 3 blocks (stdlib, 3rd party, 1st party), that imports are sorted within those blocks, that duplicate imports are removed, and more.

The main difference between the two is that reorder_python_imports uses static analysis more extensively to determine the import order. Furthermore, reorder_python_imports has a more opinionated import style to ensure that merge conflicts happen less often. 


isort:

```diff
-from typing import Dict, List
+from typing import Dict, List, Tuple
```

reorder_python_imports:

```diff
from typing import Dict
from typing import List
+from typing import Tuple
```

Source (isort): https://github.com/PyCQA/isort
Source (reorder_python_imports): https://github.com/asottile/reorder_python_imports




#### pyupgrade

**Categories:** Formatter, Linter

Upgrades Python syntax. Given a minimum supported Python version, it will upgrade the syntax of the code to use newer features of the language. For example, it will convert literals, comprehensions, type annotations and more to use the newer syntax. 

Source: https://github.com/asottile/pyupgrade

<!-- #### safety

Checks for insecure dependencies. See [Dependency Management](#dependency-management) for more details. -->


