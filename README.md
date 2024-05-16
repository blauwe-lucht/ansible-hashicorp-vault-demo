# Ansible Hashicorp Vault Demo

## Prerequisites

- VirtualBox, tested with 6.1.48
- Vagrant, tested with 2.4.1

## Instructions

``` bash
vagrant up
vagrant ssh acs
ansible-playbook playbook-install-vault.yml
```

When using vscode you can use the provided terminal profiles to quickly open an SSH session to the acs VM or the vault VM.
