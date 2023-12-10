**Ansible Role hashivault**
===========================

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=flat&logo=ansible&logoColor=white)
![GitHub License](https://img.shields.io/github/license/ironwolphern/ansible-role-hashivault)
![GitHub release (with filter)](https://img.shields.io/github/v/release/ironwolphern/ansible-role-hashivault)
![GitHub pull requests](https://img.shields.io/github/issues-pr/ironwolphern/ansible-role-hashivault)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/ironwolphern/ansible-role-hashivault)
![GitHub issues](https://img.shields.io/github/issues/ironwolphern/ansible-role-hashivault)
[![Ansible Lint](https://github.com/ironwolphern/ansible-role-hashivault/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/ironwolphern/ansible-role-hashivault/actions/workflows/ansible-lint.yml)
![Dependabot](https://badgen.net/github/dependabot/ironwolphern/ansible-role-hashivault)

This is a ansible role to install a Hashicorp Vault server with integrated storage in an standalone server.
For more information of this product visit https://www.vaultproject.io

*Requirements*
--------------

This role need the unzip, openssl package, if not installed in your OS, the role will install it. Some modules in role tasks need to be use with an ansible collection ***community.general*** for configure capabilities and ***community.crypto*** for create a private key and csr to deploy certificate with custom data.

You can install this collections with requirements file:
```shell
  ansible-galaxy collection install -r requirements.yml
```

Too the community.crypto modules need the following library installed:

cryptography >= 1.3

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

| **Parameter** | **Description** | **Type** | **Default** | **Options** | **Required** |
|---------------|-----------------|----------|:-----------:|:-----------:|:------------:|
| hashivault__tmp_dir | dir to download | string | /tmp/hashivault | | no |
| hashivault__install_dir | dir to install | string | /opt/vault | | no |
| hashivault__config_dir | dir to configure | string | /etc/vault.d | | no |
| hashivault__version | version of the server | number | 1.15.4 | | yes |
| hashivault__user | service user | string | vault | | no |
| hashivault__group | service group | string | vault | | no |
| hashivault__server_fqdn | Name of server in fqdn | string | vault.example.local | | yes |
| hashivault__init_key_shares | total keys seal | number | 5 | | no |
| hashivault__init_key_threshold | keys for unseal | number | 3 | | no |
| hashivault__kv_secret_engine_path | path for kv secret engine | string | secrets | | no |
| hashivault__snap_name | Name for backup file | string | backup | | no |
| hashivault__backup_minute | Minute for cron backup | number | 0 | | no |
| hashivault__backup_hour | Hour for cron backup | number | 0 | | no |
| hashivault__backup_weekday | Weekday for cron backup | number | * | | no |
| hashivault__backup_rotate_minute | Minute for cron backup rotate | number | 0 | | no |
| hashivault__backup_rotate_hour | Hour for cron backup rotate | number | 0 | | no |
| hashivault__backup_rotate_weekday | Weekday for cron backup rotate | number | 6 | | no |
| hashivault__backup_rotate | Rotate backups in days | number | 7 | | no |
| hashivault__restore_file_path | Path for restore backup | string | '' | | no |
| hashivault__debugger | Enable debugger | boolean | false | true/false | no |
| hashivault__tls_provider | Type tls provider | string | selfsigned | selfsigned/custom | no |
| hashivault__tls_type | Type of tls encrypt | string | RSA | RSA/DSA/ECC | no |
| hashivault__tls_size | Size of tls key | number | 4096 | | no |
| hashivault__tls_selfsigned_csr_country | Country for csr on selfsigned provider | string | ES | | no |
| hashivault__tls_selfsigned_csr_state | State for csr on selfsigned provider | string | Madrid | | no |
| hashivault__tls_selfsigned_csr_locality | Locality for csr on selfsigned provider | string | Madrid | | no |
| hashivault__tls_selfsigned_csr_organization | Organization for csr on selfsigned provider | string | My Company | | no |
| hashivault__tls_selfsigned_csr_ou | Department for csr on selfsigned provider | string | IT | | no |
| hashivault__tls_selfsigned_csr_sans | SANS for csr on selfsigned provider | list | [] | email, URI, DNS, RID, IP, dirName, otherName | no |

*Dependencies*
--------------

There are no dependencies.

*Example Playbook*
------------------

This is an example of use role with optionals and required parameters:

*play-vault.yml*
```yaml
- hosts: vault
  gather_facts: true
  roles:
  - role: ansible-role-hashivault
    vars:
      hashivault__version: 1.15.4
      hashivault__server_fqdn: vault.example.local
```

These are some examples of the use of this playbook with the different tags that can be used in this role:

Install and configure full
```bash
  ansible-playbook -i inventory play-vault.yml
```
Uninstall
```bash
  ansible-playbook -i inventory play-vault.yml -t uninstall
```
Set backup auto
```bash
  ansible-playbook -i inventory play-vault.yml -t backup_auto
```
backup manual with name
```bash
  ansible-playbook -i inventory play-vault.yml -t backup_manual -e hashivault__snap_name=my_backup
```
backup restore
```bash
  ansible-playbook -i inventory play-vault.yml -t restore -e hashivault__restore_file_path=my_backup.snap
```
Unseal instance
```bash
  ansible-playbook -i inventory play-vault.yml -t unseal
```

*Roadmap*
---------

For upcoming versions, integration with Let's Encrypt certificates is being developed as a server tls certificate.

*License*
---------

MIT

*Author Information*
--------------------

This role was created in 2023 by:

- Fernando Hernández San Felipe (ironwolphern@outlook.com)
