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

* Run the Playbook as a non-root user with privileges to install build dependencies.

```
$ ansible-playbook --become-method sudo --ask-become-pass site.yml
```

* When re-running the Playbook, installing the dependencies can be skipped.

```
$ ansible-playbook --skip-tags become site.yml
```

## License

GPLv3
