# Ansible

Ansible - https://www.ansible.com/ - configuration management tool.  You can
also find ansible tutorials and documentation at their website under the
documentation section.

### Ansible Helpful Commands

Read local documentation for ansible commands.

```bash
ansible-doc --help
ansible-doc --list
ansible-doc shell
```

Sample inventory file.

```ini
[myself]
127.0.0.1
```

Execute a command on ansible inventory.

```bash
ansible myself -i inventory -m 'shell' -a 'echo hello'
```

More verbose for failures.

```bash
ansible myself -i inventory -m 'shell' -a 'exit 1' -vvvv
```

Executing a module on inventory.

```bash
ansible-doc maven_artifact
ansible myself -i inventory -m 'maven_artifact' -a "artifact_id=structs version=1.2 group_id=org.jenkins-ci.plugins dest=. repository_url=http://repo.jenkins-ci.org/public/ state=present"
```

Creating a role.

```
$ ansible-galaxy init ansible-myrole
$ cd ansible-myrole/
$ ls -F
README.md defaults/ files/ handlers/ meta/ tasks/ templates/ tests/ vars/
```

* `defaults/` are variables meant to be overridden in the role.
* `files/` hold files used to be copied to the remote machine.
* `handlers/` are "notified" actions that run after all tasks have been completed.  A handler could be, for example, restarting a service.
* `tasks/` which run to configure a system.
* `templates/` which store jinja2 templates.
* `tests/` which store tests for testing a role.
* `vars/` are static variables in the role.

Roles are typically used to configure a service where playbooks configure servers using roles.
