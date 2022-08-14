# Ansible role for building and running gitlab-ce.
=================================================

**summary**
This role is for building and running gitlab-ce (the docker container version). 
Look in the tasks directory for each configuration.
All configurations are held atomically via their own files.

## Necessary preparations
A docker runtime environment must exist on the system.
Or use: https://github.com/conloos/ansible-docker

## Variables that have to be defined

| variable | description | mandantory |
| -------- | ----------- | ---------- |
| gitlab_ce_version_tag | Docker conainer TAG to pull. | False - predefined |
| gitlab_ce_persistent_path | Path to the persisten storage for docker container. | False - predefined |
| gitlab_ce_hostname | FQDNn of the host. | True |
| ssl_crt_path | Path to the ssl-crt for the webserver. | False |
| ssl_key_path | Path to the ssl-key for the webserver. | False |

# example playbook
```
---
- hosts: 
    - example.com
  become: true
  vars:
    gitlab_ce_hostname: example.com
  vars_files:
    - group_vars/vault.yml
  tasks:
  roles:
    - ansible-gitlab_ce
```