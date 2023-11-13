# Documentation

This repository contains the documentation of the T2-Project.

The documentation is generated with [Sphinx](https://www.sphinx-doc.org/en/master/) and hosted with [Read the Docs](https://docs.readthedocs.io/en/stable/).

It can be found here: [https://t2-documentation.readthedocs.io/](https://t2-documentation.readthedocs.io/)

## Local Build

Install dependencies ([using pip and venv](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)):

```sh
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
```

Build:

```sh
make html
```
