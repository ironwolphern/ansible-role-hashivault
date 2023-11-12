:construction: ***DEVELOPING*** :construction:

**Ansible Role hashivault**
===========================

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=flat&logo=ansible&logoColor=white)
![License](https://badgen.net/github/license/ironwolphern/ansible-role-hashivault)
![Release](https://badgen.net/github/release/ironwolphern/ansible-role-hashivault)
![PRs](https://badgen.net/github/prs/ironwolphern/ansible-role-hashivault)
![Issues](https://badgen.net/github/issues/ironwolphern/ansible-role-hashivault)
[![Ansible Lint](https://github.com/ironwolphern/ansible-role-hashivault/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/ironwolphern/ansible-role-hashivault/actions/workflows/ansible-lint.yml)
![Dependabot](https://badgen.net/github/dependabot/ironwolphern/ansible-role-hashivault)

This is a ansible role to install a Hashicorp Vault server with integrated storage in an standalone server.  
For more information od this product visit https://www.vaultproject.io

*Requirements*
--------------

This role need the unzip package, if not installed in your OS, the role will install it.  
The recommended server features for lab are:

For lab enviroment:

  - 1 CPU
  - 4 GB of Memory
  - 50 GB of storage

For production aprox:

  - 2 CPUs
  - 8 GB of Memory
  - 100 GB of storge

*Role Variables*
----------------

This is a list of required and optinal variables and parameters for this role:

| **Parameter**                  | **Description**            | **Type** |     **Default**     |**Required**|
|--------------------------------|----------------------------|----------|:-------------------:|:----------:|
| hashivault__install_dir        | dir to install             |  string  | /opt/vault          |     no     |
| hashivault__config_dir         | dir to configure           |  string  | /etc/vault.d        |     no     |
| hashivault__version            | version of the server      |  number  | 1.15.1              |     yes    |
| hashivault__user               | service user               |  string  | vault               |     no     |
| hashivault__group              | service group              |  string  | vault               |     no     |
| hashivault__server_fqdn        | Name in fqdn               |  string  | vault.example.local |     yes    |
| hashivault__init_key_shares    | total keys seal            |  number  | 5                   |     no     |
| hashivault__init_key_threshold | keys for unseal            |  number  | 3                   |     no     |
| hashivault__snap_name          | Name for backup            |  string  | backup              |     no     |
| hashivault__restore_file_path  | Path for restore backup    |  string  | ''                  |     no     |


*Dependencies*
--------------

There are no dependencies.

*Example Playbook*
------------------

This is an example of use role with optionals and required parameters:

*play-hv.yml*
```yaml
    - hosts: vault
      roles:
        - hashivault
      vars:
        hashivault__version: 1.15.1
        hashivault__server_fqdn: vault.example.local
```

These are some examples of the use of this playbook with the different tags that can be used in this role:

Install and configure full
```bash
  ansible-playbook -i inventory play-hv.yml
```
Uninstall
```bash
  ansible-playbook -i inventory play-hv.yml -t remove
```
Set backup auto
```bash
  ansible-playbook -i inventory play-hv.yml -t backup_auto
```
backup manual with name
```bash
  ansible-playbook -i inventory play-hv.yml -t backup_manual -e hashivault__snap_name=my_backup
```
Unseal instance
```bash
  ansible-playbook -i inventory play-hv.yml -t unseal
```

*License*
---------

MIT

*Author Information*
--------------------

This role was created in 2023 by:

- Fernando Hernández San Felipe (ironwolphern@outlook.com)
