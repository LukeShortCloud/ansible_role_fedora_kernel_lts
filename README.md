# ansible_role_fedora_kernel_lts

An Ansible role for automating the build of the LTS Linux kernel RPMs for Fedora.

Builds of this kernel are published to a Fedora Copr repository. Instructions on how to enable the repository and install the kernel can be found [here](https://copr.fedorainfracloud.org/coprs/ekultails/fedora_kernel_lts/).

## Requirements

* Ansible \>= 2.6

## Role Variables

Immutable (should not be changed unless rebasing ontop a new `X.Y` kernel):

* kernel_version_major = The major Linux kernel version.
* kernel_version_minor = The minor Linux kernel version.

Mutable (user configurable):

* kernel_version_patch = The patch Linux kernel version.
* git_repository_kernel = The Git repository to use for the upstream Fedora kernel.
* git_branch_kernel = The branch, commit, or tag to checkout from the Git repository.
* rpmbuild_sources_dir = The path to the "SOURCES" directory that will be used by rpmbuild.

## Dependencies

None.

## Example Playbook

* An example "site.yml" Playbook file. By default, source RPMs will built.

```
---
- hosts: build_host
  roles:
    - ansible_role_fedora_kernel_lts
```

* Run the Playbook as a non-root user with privileges to install build dependencies and then build the RPMs.

```
$ ansible-playbook --become-method sudo --ask-become-pass site.yml
```

* When re-running the Playbook, installing the dependencies can be skipped.

```
$ ansible-playbook --skip-tags become site.yml
```

* Optionally build the binary RPM.

```
$ ansible-playbook --skip-tags become --extra-vars rpmbuild_options="-bb --with baseonly --without debuginfo" site.yml
```

## Testing

```
$ molecule converge -- -vvv
$ molecule destroy
```

## Contributing

For rebasing kernels and removing patches, use this Bash command to get all of the changelogs since the last release of the kernel used in ansible-role-fedora-kernel-lts. A lot of Fedora patches get backported into the upstream kernel. The example grabs all of the changelogs for 4.19.15 through 4.19.20.

```
$ for i in $(seq 15 20); do curl https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.19.$i >> /tmp/kernel.changelog; done
```

## License

GPLv3
