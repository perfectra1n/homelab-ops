## My stupid notes

To run the `ping` module against every single item in the homelab inventory:

```sh
ansible -i inventory/homelab -m ansible.builtin.ping all
```

To see what's installed

```bash
ansible -vvv -i inventory/homelab -m package_facts all
```

So the `makefile` deletes the current `roles/galaxy` directory with `rm -rf roles/galaxy`.
Then it will install the roles into `roles/galaxy` with `ansible-galaxy install -r requirements.yml -p roles/galaxy/ --force`.

So everything is documented in `requirements.yml`, like:

```yml
---
- name: geerlingguy.docker
  version: 6.1.0
```

You can't include `hosts` in the YAML block when writing tasks, so you can't do something like:
```yml
- name: "Install Docker"
  hosts: all
  become: true

  roles:
    - role: galaxy/geerlingguy.docker
      tags:
        - setup-docker
        - setup-all
        - install-docker
        - install-all
```

In a task, but once you remove `hosts`, it works just fine.