Usage (localhost only):

```ansible-playbook init.yml -K```

Tools used:
1. Ansible.
2. Docker-compose.

To see, what does playbook do shortly - just read plan.txt.

The main target while completing the task was automation with stable, reproducible, idempotent (where it is needed) result.
So I used ansible to automate the task, and my knowledge of building the infrastructure from scratch. While using/developing playbooks correctly, ansible allows to abstract of OS. Also, ansible playbooks can be read and written easily, so it's my classic tool instead of BASH-scripting.

BASH-scripting was used in ansible playbook to speed up the process of writing the playbook. However, it's a nasty solution and I usually avoid it, where it is possible. I could use modules while creating cryptographic keys, for example, but didn't.

Dockerizing the app is not my wish, it's just a part of task, so there is no any other reason why I used it there. I could use additional nginx config, for example.

Features of my task implementation are:

    - always fresh certificates

    - symlinks to certificates (as it is implemented in certbot)

    - using collections to avoid user-interaction

    - ability to create any quantity of domains

    - templated nginx-config

    - as we are working on the client-server machine simultaneously, the playbook configures it to work with self-signed certificates

    - container's IPAddresses and names is not hardcoded to make config more flexible. You can create a lot of stacks with different containers

I'm sorry, but I cannot use "systemctl" or "service" utilities on my laptop, so I couldn't use this, for example:
```
  - name: Reload nginx
    service:
      name: nginx
      state: reloaded```