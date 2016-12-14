# Molecule-tested Ansible Infrastructure

Molecule provides a recommended way to configure and test infrastructure
configured by Ansible roles.  This is all in support of [immutable
infrastructure][ii].

This document should be referenced whenever creating new ansible roles.

# Technologies involved

* Ansible - https://www.ansible.com/ - configuration management tool.
* Git - https://git-scm.com/ - source code management.
* Molecule - https://molecule.readthedocs.io/ - testing convention tool for
  ansible roles.
* Python - https://www.python.org/ - scripting language used by Ansible and
  Molecule.
* Vagrant - https://www.vagrantup.com/ - VirtualBox provisioning layer.
* Virtualenv - https://virtualenv.pypa.io/ - user-managed python environment
  which simplifies development.

### See also

* [Ansible help](help/ansible.md).
* [Virtualenv help](help/virtualenv.md).
* [Molecule help](help/molecule.md).

# Best practices getting started

Whenever creating a role for the GIMP CI system or related projects, the
following best practices must be followed to keep the quality of the code high.

Molecule provides convention around unit testing roles, using vagrant or docker,
and setting up the scaffolding.

### Initial role creation.

Create a starting point for the role.  Start by installing all prereqs.

    virtualenv --python=$(type -p python2.7) .venv
    source .venv/bin/activate
    pip install -U pip
    pip install molecule
    pip install python-vagrant
    pip install -U ansible-lint

Create the initial scaffolding for the role.  All role names must begin with
`ansible-`.  This makes searching for them on GitHub much easier.

    molecule init --role ansible-myrole
    cd ansible-myrole

Freeze the python dependencies so that testing is repeatable.

    pip freeze > test-reqs.txt

Start developing the role and use `molecule converge` to keep testing.  When
ready, initialize the role as a git repository to be uploaded to the
[`gimp-ci`][gimp-ci] organization.

```bash
cat > .gitignore <<EOF
/.molecule
/.vagrant
/.venv
__pycache__
/playbook.retry
/.cache
*.pyc
EOF
git init
git add .
git commit -m 'initial commit'
```

Publish to [`gimp-ci`][gimp-ci] when you're ready.

    git remote add origin git@github.com:gimp-ci/ansible-<YOUR ROLE>.git
    git push origin -u master

# Documenting getting started

Remember, documentation is everything.  Don't forget to add to the `README.md`
file of your Ansible role how to get started with furthering development and
testing.  For example, a "Getting Started" section should contain the following.

    git clone <repository>
    cd ansible-myrole
    virtualenv --python=$(type -p python2.7) .venv
    source .venv/bin/activate
    pip install -U pip
    pip install -r test-reqs.txt
    #now ready for development or running
    molecule test

[gimp-ci]: https://github.com/gimp-ci
[ii]: https://www.oreilly.com/ideas/an-introduction-to-immutable-infrastructure
