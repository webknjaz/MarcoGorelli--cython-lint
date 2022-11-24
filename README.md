[![Build Status](https://github.com/MarcoGorelli/cython-lint/workflows/tox/badge.svg)](https://github.com/MarcoGorelli/cython-lint/actions?workflow=tox)
[![Coverage](https://codecov.io/gh/MarcoGorelli/cython-lint/branch/main/graph/badge.svg)](https://codecov.io/gh/MarcoGorelli/cython-lint)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/MarcoGorelli/cython-lint/main.svg)](https://results.pre-commit.ci/latest/github/MarcoGorelli/cython-lint/main)

cython-lint
===========

A tool and pre-commit hook to lint Cython files.

## Installation

```console
$ pip install cython-lint
```

## Usage as a pre-commit hook

See [pre-commit](https://github.com/pre-commit/pre-commit) for instructions

Sample `.pre-commit-config.yaml`:

```yaml
-   repo: https://github.com/MarcoGorelli/cython-lint
    rev: v0.8.1
    hooks:
    -   id: cython-lint
    -   id: double-quote-strings
```

## Command-line example

```console
$ cython-lint my_file_1.pyx my_file_2.pyx
my_file_1.pyx:54:5: 'get_conversion_factor' imported but unused
my_file_2.pyx:1112:38: 'mod' defined but unused
my_file_3.pyx:4:9: dangerous default value!
my_file_3.pyx:5:9: comma after base type in definition
```


## Configuration

The following configuration options are available:
- exclude lines by including a ``# no-cython-lint`` comment (analogous to ``# noqa`` in ``flake8``);
- use the command-line argument ``--max-line-length`` to control the maximum line length used by pycodestyle;
- use the command-line argument ``--no-pycodestyle`` if you don't want the pycodestyle checks.

## Which checks are implemented?

- variable defined but unused
- variable imported but unused
- comma after base type definition (e.g. ``cdef ndarray, arr``)
- f-string without placeholders
- dict key repeated
- dict key variable repeated
- if-statement with tuple condition (always true...)
- assert statement with tuple condition (always true...)
- dangerous default value
- repeated element in set
- ``.strip``, ``.rstrip``, or ``.lstrip`` used with repeated characters
- comparison between constants
- late-binding closures https://docs.python-guide.org/writing/gotchas/#late-binding-closures
- ``pycodestyle`` nitpicks, which you can turn off with ``--no-pycodestyle``

In addition, the following automated fixers are implemented:

- double-quote-strings (replace single quotes with double quotes, like the ``black`` formatter does)

More to come! Requests welcome!
