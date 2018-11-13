# Ansible Role: Enable Huge Pages

Enable Huge Pages on Linux.

Travis status:   [![Build Status](https://travis-ci.org/KAMI911/ansible-role-hugepages.svg?branch=master)](https://travis-ci.org/KAMI911/ansible-role-hugepages)
Code Climate status: [![Code Climate](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/badges/gpa.svg)](https://codeclimate.com/github/KAMI911/ansible-role-hugepages)
Test Coverage status: [![Test Coverage](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/badges/coverage.svg)](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/coverage)

## Table of Contents

1. [Requirements][Requirements]
2. [Background][Background]
3. [Installation][Installation]
4. [Role Variables][Role Variables]
5. [Dependencies][Dependencies]
6. [Example Playbook][Example Playbook]
7. [Licensing][Licensing]
8. [Author Information][Author Information]
9. [Support][Support]
10. [Contributing][Contributing]
11. [Donation][Donation]

## Requirements

None.

## Background

Enabling huge pages provide extra performance for your application. Only few apllications are supporting huge pages. When a process uses some memory, the CPU is marking the RAM as used by that process. For efficiency, the CPU allocate RAM by chunks of 4K bytes (it's the default value on many platforms). Those chunks are named pages. Those pages can be swapped to disk, etc.

Since the process address space are virtual, the CPU and the operating system have to remember which page belong to which process, and where it is stored. Obviously, the more pages you have, the more time it takes to find where the memory is mapped. When a process uses 1GB of memory, that's 262144 entries to look up (1GB / 4K). If one Page Table Entry consume 8bytes, that's 2MB (262144 * 8) to look-up.

[Debian Wiki: Hugepages](https://wiki.debian.org/Hugepages)

### Applications that support huge pages:

* Java
* MySQL
* PostgreSQL
* Memcached
* KVM
* XEN

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    hugepages_system_group: hugepages

Name of group for access Huge Pages.

    hugepages_system_member: tomcat

User who is member of Huge Pages group.

    sysctl_d_path: "/etc/sysctl.d"

Location of sysctl.d folder.

    hugepages_sysctl_filename: "90-hugepages.conf"

Name of sysstl.d file.

    hugepages_number: 3072

Specify the number of large Huge Pages or large pages. In the following example 6 GB of a 8 GB system are reserved for large pages (assuming a large page size of 2048k (Hugepagesize: 2048 kB), then 6 GB = 6 x 1024 MB = 6291456 KB / 2048 KB = 3072):

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - hugepages

## Licensing

The lactransformer application and documantations are licensed under the terms of
the MIT / BSD, you will find a copy of this license in the
[LICENSE](LICENSE) file included in the source package.

## Author Information

This role was created in 2016-2018 by Kálmán Szalai - KAMI

## Support

If you have any question, do not hesitate and drop me a line.
If you found a bug, or have a feature request, you can [fill an issue](https://github.com/KAMI911/ansible-role-hugepages/issues).

### Using as a submudule of an AWX playbook

#### Add as a submodule

```
git submodule add --force git@github.com:KAMI911/ansible-role-hugepages.git roles/hugepages
```

#### Update as sumodule

Update only this submodule

```
git submodule update --remote roles/hugepages/
```

Update all submodules:

```
git submodule foreach git pull origin master
```

## Contributing

There are many ways to contribute to ansible-role-hugepages -- whether it be sending patches,
testing, reporting bugs, or reviewing and updating the documentation. Every
contribution is appreciated!

Please continue reading in the [contributing chapter](CONTRIBUTING.md).

### Fork me on Github

SSH:

    git@github.com:KAMI911/ansible-role-hugepages.git

HTTPS:

    https://github.com/KAMI911/ansible-role-hugepages

Add a new remote `upstream` with this repository as value.

```
git remote add upstream https://github.com/KAMI911/ansible-role-hugepages.git
```

You can pull updates to your fork's master branch:

```
git fetch --all
git pull upstream HEAD
```

## Donation

If you find this useful, please consider a donation:

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RLQZ58B26XSLA)

<!-- TOC URLs -->
[Requirements]: #requirements
[Background]: #background
[Installation]: #installation
[Role Variables]: #role_variables
[Dependencies]: #dependencies
[Example Playbook]: #example_playbook
[Licensing]: #licensing
[Author Information]: #author_information
[Support]: #support
[Contributing]: #contributing
[Donation]: #donation

