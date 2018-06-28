# ansible-role-fedora-kernel-lts

An Ansible role for automating the build of the LTS Linux kernel RPMs for Red Hat Enterprise Linux and Fedora.

## Requirements

* Ansible 2.4

## Role Variables

* kernel_type = "lts" or "stable."
* kernel_version_major = The major Linux kernel version.
* kernel_version_minor = The minor Linux kernel version.
* kernel_version_patch = The patch Linux kernel version.
* git_repository_kernel = The Git repository to use for the upstream Fedora kernel.
* git_branch_kernel = The branch, commit, or tag to checkout from the Git repository.
* rpmbuild_sources_dir = The path to the "SOURCES" directory that will be used by rpmbuild.

## Dependencies

None.

## Example Playbook

* An example "site.yml" Playbook file.

```
---
- hosts: build_host
  roles:
    - ansible-role-fedora-kernel-lts
```

* Run the Playbook as a non-root user with privileges to install build dependencies.

```
$ ansible-playbook --become-method sudo --ask-become-pass site.yml
```

* Alternatively, build a newer stable release of the Linux kernel.

```
$ ansible-playbook --become-method sudo --ask-become-pass --extra-vars kernel_type=stable site.yml
```

* When re-running the Playbook, installing the dependencies can be skipped.

```
$ ansible-playbook --skip-tags become site.yml
```

## Contributing

For rebasing kernels and removing patches, use this Bash command to get all of the changelogs since the last release of the kernel used in ansible-role-fedora-kernel-lts. A lot of Fedora patches get backported into the upstream kernel. The example grabs all of the changelogs for 4.14.26 through 4.14.52.

```
$ for i in $(seq 26 52)`; do curl https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.14.$i >> /tmp/kernel.changelog; done
```

## License

GPLv3
