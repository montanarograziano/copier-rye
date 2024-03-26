<div align="center">

[![rye-managed](https://img.shields.io/badge/rye-managed-green)](https://rye-up.com)
[![pre-commit enabled](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![documentation mkdocs](https://img.shields.io/badge/documentation-mkdocs%20material-0094F5)](https://www.mkdocs.org/)

</div>

`copier-rye` is a [Copier](https://copier.readthedocs.io/en/stable/) template ideated to speed up the development process of Python applications. No more configuration hassle and boilerplate!

## ⚡ Features

`copier-rye` offers a production-ready development environment, with many useful features like formatting, linting, pre-commit hooks, and documentation already set up. Here's an overview of the features:

- [`rye`](https://rye-up.com) is a comprehensive project and package management solution for Python.
- [`just`](https://github.com/casey/just/) is a modern rewrite of `make` in Rust 🦀
- [`pre-commit`](https://github.com/pre-commit/pre-commit) validates your commits.
- [`ruff`](https://github.com/charliermarsh/ruff) provides static code analysis and a code and import formatting using [`black`](https://github.com/psf/black) and [`isort`](https://github.com/PyCQA/isort) styles.
- [`mypy`](https://github.com/python/mypy/) validates your type hints.
- [`pytest`](https://github.com/pytest-dev/pytest) runs your test suite.
- [`mkdocs`](https://github.com/mkdocs/mkdocs) builds your documentation, while [`mkdocs-material`](https://github.com/squidfunk/mkdocs-material) provides an elegant theme. [`mike`](https://github.com/jimporter/mike) takes care of versioning your docs.
- [`commitizen`](https://github.com/commitizen-tools/commitizen) ensures you follow [Conventional commit style](https://www.conventionalcommits.org/en/) and generates your release changelogs according to [SemVer](https://semver.org/)

> **Note**
>
> **Developer guidelines**
>
> - The template adopts to the `src` layout.
> - `mypy` is configured with a strict ruleset. The recommended approach to loosen those constraints is by temporary per-module ignores.
> - `google` is the docstring style of choice.
> - `ruff` is used to format the code using `black` style, while imports are sorted with `isort` style.
> - Releases follow [Semantic Versioning](https://semver.org/).
> - Commit follow the [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/) specification.

> **Note**
>
> **`just` a command runner**
>
> `just` recipes will save you a ton of time! Install [just](https://github.com/casey/just/tree/master#installation). To see the available recipes, run the following:
>
> ```bash
> just
> ```

## 🛠️ How to

Install [`rye`](https://pdm.fming.dev/latest/#installation) and [`just`](https://github.com/casey/just#installation):

```bash
curl -sSf https://rye-up.com/get | bash # For Linux/ Mac Users

# for example, on macOS
brew install just
```

### Optional: Install uv
For blazingly fast dependency install you can set `rye` to use `uv` under the hood when retrieving dependencies:
First of all, install `uv`.
```bash
pipx install uv
```

> **Warning**
>
> 🔎 Why `pipx`?
> `pip install --user` is not recommended, as it does not ensure dependency isolation. For this purpose, the [Python Packaging Authority (PyPA)](https://www.pypa.io/en/latest/) advises to use [`pipx`](https://pypa.github.io/pipx/). `pipx` installs and runs python CLIs in isolated environments. To install it, follow the instructions [here](https://pypa.github.io/pipx/#install-pipx).

Then, configure `rye` to use uv:
```bash
rye config --set-bool behavior.use-uv=true
```

### Create a New Project

If you want to create a new package, or any coding project, you just have to run two short commands.

1. Initialise the template:

```bash
copier copy --trust gh:montanarograziano/copier-rye my-project
```


2. Initialize GitHub repository locally (necessary to install pre-commit hooks) and install all default dependencies, running the following `just` recipe:

```bash
just init
```

For this command to execute successfully, you need to have [`rye`](https://rye-up.com/) and the [Git](https://git-scm.com/) installed.

If you do not want to configure CI/CD on GitHub, you can simply run the following:

```
just install
```

## 🙋 FAQ

### How do I write conventional commits?

Conventional commits are enforced with [`commitizen`](https://commitizen-tools.github.io/commitizen/), which is configured as a `pre-commit` hook at pre-push time. **In other words, if you attempt to push to a remote repo and your commit messages do not follow the conventional commits, the push will be rejected**. However, `commitizen` also offers a git command to commit with the conventional commit specification with a terminal UI. With `just`, you can simply run the following:

```bash
just commit
```

Or even the shorter `just c`. A prompt will guide you through the commit.

## 📝 Template fields

```json
{
  "project_name": "",
  "project_description": "",
  "author_fullname": "",
  "author_email": "",
  "author_username": "",
  "repository_provider": "",
  "repository_namespace": "",
  "repository_name": "",
  "copyright_holder": "",
  "copyright_holder_email": "",
  "copyright_date": "",
  "copyright_license": "",
  "ensure_python_version": "3.10",
  "python_package_distribution_name": "",
  "python_package_import_name": ""

}
```
- `project_name`: the name of the project indicated in `pyproject.toml`.
- `project_description`: the description of the project indicated in `pyproject.toml`.
- `author_fullname`: the author full name.
- `author_email`: the author email address.
- `repository_provider`: the repository provider (e.g., *GitHub*, *GitLab*, *BitBucket*). Only GitHub is supported for now.
- `repository_namespace`: the repository namespace.
- `package_name`: the package name.
- `copyright_license`: the selected license.
- `ensure_python_version`: the minimal python version required for the project.
- `python_package_distribution_name`: the Python package distribution name (for `pip install NAME`).
- `python_package_import_name`: the Python package import name (for `import NAME` in Python code)

## 🤗 Contributing

PR and issues are always accepted, especially since this project is far from being mature.

### Development

1. Install `rye` and `just`.

2. Clone the repository:

```bash
# using github cli
gh repo clone montanarograziano/copier-rye

# using git (SSH recommended)
git clone git@github.com:montanarograziano/copier-rye
```

3. Install the dependencies:

```
just install
```

### Before submitting a PR

Run the following:

```
just pre-release
```

The following operations will be performed:

1. Format with `black` and `isort`.
2. Lint with `ruff`.
3. Run type checks with `mypy`.
4. Audit dependencies with `pip-audit`.
5. Check commit messages are consistent with Conventional Commits using `commitizen`.
6. Check whether a version bump is possible.
7. Run all tests.

## 📚 Credits

This template is heavly inspired by [@baggiponte](https://github.com/baggiponte) [Chef](https://github.com/baggiponte/chef/tree/main) (based on Cookiecutter) and [@pawamoy](https://github.com/pawamoy) [copier-uv](https://github.com/pawamoy/copier-uv) (based on Copier). They use respectively `pdm` and `uv` as packaging solution. Both are very well done and works great, and so...

### Why bother creating (yet another) template?

As of today, it seems that there are no **Copier** templates that uses `rye`, given the novelty of the project.
Furthermore, sometimes a feature is not implemented in any available template or you need a custom one.

Personally, I believe that leveraging templating to abstract on stuff like *dependency manager*, is a possible solution: give the user many choices and let him decide which one suits him best.

Feel free to contact to discuss more about this topic!
