# Ansible Hashicorp Vault Demo

## Prerequisites

- VirtualBox, tested with 6.1.50
- Vagrant, tested with 2.4.1

## Instructions

``` bash
vagrant up
vagrant ssh acs
ansible-playbook playbook-install-vault.yml
```

When using vscode you can use the provided terminal profiles to quickly open an SSH session to the acs VM or the vault VM.

After running the playbook-install-vault, Vault has been installed and configured with:

- the KV v2 secrets engine, at the path 'secret',
- a policy 'read_secret_policy' that can only read secrets from the path 'secret',
- an approle 'read_secret_approle' that uses this policy.

To see the approle in action, run

``` bash
ansible-playbook playbook-use-secret.yml
```

To clear everything up, on the host run

``` bash
vagrant destroy -f
```
