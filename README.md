# Ansible Role: Enable Huge Pages

Enable Huge Pages on Linux.

Travis status:   [![Build Status](https://travis-ci.org/KAMI911/ansible-role-hugepages.svg?branch=master)](https://travis-ci.org/KAMI911/ansible-role-hugepages)
Code Climate status: [![Code Climate](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/badges/gpa.svg)](https://codeclimate.com/github/KAMI911/ansible-role-hugepages)
Test Coverage status: [![Test Coverage](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/badges/coverage.svg)](https://codeclimate.com/github/KAMI911/ansible-role-hugepages/coverage)

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

Specify the number of large Huge Pages or large pages. In the following example 6 GB of a 8 GB system are reserved for large pages (assuming a large page size of 2048k (Hugepagesize: 2048 kB), then 6g = 6 x 1024m = 6
6k / 2048k = 3072):

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - hugepages

## License

MIT / BSD

## Author Information

This role was created in 2016-2017 by Kálmán Szalai - KAMI
