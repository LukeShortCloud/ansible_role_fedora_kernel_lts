# ansible-role-fedora-kernel-lts

An Ansible role for automating the build of the LTS Linux kernel RPMs for Fedora.

## Requirements

* Ansible 2.4

## Role Variables

* kernel_version_major = The major Linux LTS kernel version.
* kernel_version_minor = The minor Linux LTS kernel version.
* git_branch = The branch from "fedora-kernel-lts" that correlates to the major Linux LTS kernel version.
* rpmbuild_sources_dir = The path to the "SOURCES" directory that will be used by rpmbuild.

## Dependencies

None.

## Example Playbook

* An example "site.yml" Playbook file.

```
---
- hosts: localhost
  roles:
    - ansible-role-fedora-kernel-lts
```

* Run the Playbook as the local non-root user with privileges to run commands as sudo.

```
$ ansible-playbook --ask-become-pass site.yml
```

## License

GPLv3
