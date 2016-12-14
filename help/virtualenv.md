# Virtualenv

Virtualenv - https://virtualenv.pypa.io/ - user-managed python environment which
simplifies development.

Between virtualenv and [pip][pip] you can reliably configure dependencies across
collaborator development environments.  This is good for projects which depend
on python dependencies.

### Virtualenv Helpful Commands

Intialize a virtualenv.

```
virtualenv --python=$(type -p python2.7) .venv
```

Use virtualenv.

```
source .venv/bin/activate
```

You're now using a virtual environment just for python and your dependencies.
pip installing packages will only affect the virtual environment.

> Note: some Linux distrobutions have a bad version of `pip` so it is
> recommended that you upgrade `pip` in your virtualenv.
>
>     pip install -U pip

### pip requirements

When you feel your python dependencies are in a good place, it is recommended to
"freeze" these dependencies.   This allows other collaborators to install them
within their virtualenv and be able to completely reproduce your python
environment.

Create a `requirements.txt`.

    pip freeze > requirements.txt

If you have a [python `requirements.txt`][pip-reqs] configured then you can
install them with:

    pip install -r requirements.txt


[pip]: https://pypi.python.org/pypi/pip
[pip-reqs]: https://pip.readthedocs.io/en/1.1/requirements.html
