# Ansible role for building and running gitlab-ce.
=================================================

**summary**

This role is for building and running gitlab-ce (the docker container version). 
Look in the tasks directory for each configuration.
All configurations are held atomically via their own files.

***Optional Features***
* use ssl encryption
* configure gitlab to use email
* AD integration

## Necessary preparations
A docker runtime environment must exist on the system.
Or use: https://github.com/conloos/ansible-docker

## Variables that have to be defined

| variable | description | mandantory |
| -------- | ----------- | ---------- |
| gitlab_ce_hostname | FQDNn of the host. **Predefined**: ```{{ cloudinit_fqdn }}```. Overwrite if necessary.| False |
| gitlab_ce_version_tag | Docker conainer TAG to pull. **Predefined**: See at ```defaults/main.yml``` | False |
| gitlab_ce_persistent_path | Path to the persisten storage for docker container.  ```"/srv/gitlab"``` | False |
| ssl_crt_path | Path to the ssl-crt for the webserver. **Predefined**: ```/etc/ssl/{{ cloudinit_fqdn }}.crt```. Overwrite if necessary. | False |
| ssl_key_path | Path to the ssl-key for the webserver. **Predefined**: ```/etc/ssl/{{ cloudinit_fqdn }}.key```. Overwrite if necessary.  | False |


# AD integration
This Role have a basic LDAP integration.
Configuration options are limited to keep complexity at an acceptable level.
If you need an other setup please change the ```templates/gitlab.rb```.

You need an AD-User-Account: ***Please make sure to secure this account as much as possible. It makes sense to remove the user from the "Domain Users" group. If necessary (e.g. you use rfc2307 to manage posix account in the ad), a group without rights should be created and set as primary group.***

# ToDo
https://docs.gitlab.com/ee/administration/auth/ldap/
https://madafa.de/blog/set-up-gitlab-mit-active-directory-authentifizierung
http://repositories.compbio.cs.cmu.edu/help/administration/auth/how_to_configure_ldap_gitlab_ce/index.md *
https://www.ecanarys.com/Blogs/ArticleID/393/LDAP-Integration-with-Gitlab
https://www.thierolf.org/blog/2021/gitlab-ad-ldap-integration/

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