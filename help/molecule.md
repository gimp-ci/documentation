# Molecule

Molecule - https://molecule.readthedocs.io/ - testing convention tool for
Ansible roles.  This help document will give you hints as to how to operate
Molecule when developing Ansible roles.

### Molecule Helpful Commands

```
molecule --help
```

Initialize an ansible role with a name.

```
$ molecule init --role ansible-myrole
$ ls -F ansible-myrole
README.md defaults/ handlers/ meta/ molecule.yml playbook.yml tasks/ tests/ vars/
```

The molecule role is pretty similar to the `ansible-galaxy` role.  There's a few
extra files.

* `README.md` is a [markdown formatted][markdown] README which can serve as
  initial documentation for the role.
* `molecule.yml` which describes the provisioning environment where tests will
  occur.  By default it uses Vagrant.  You will want to customize the vagrant
  box to use `debian/jessie64`.
* `playbook.yml` is used by `molecule.yml` to test the role.  It is an ansible
  playbook.
* `tests/test_default.py` is an initial test template which serves as a starting
  point for unit testing the infrastructure provisioned by the role.

Create and start your VirtualBox Debian Jessie machine.

    molecule create

Provision a VM using the Ansible role and configure it using Ansible.

    molecule converge

`molecule converge` command is useful for incrementally developing an Ansible
role.

`molecule test` is intended to run the full test suite on the role.  However, it
is recommended to define the sequence in the `molecule.yml` file.  The
recommended sequence is:

```yaml
molecule:
  test:
    sequence:
      - destroy
      - syntax
      - create
      - converge
      - idempotence
      - verify
```

[markdown]: https://daringfireball.net/projects/markdown/syntax
