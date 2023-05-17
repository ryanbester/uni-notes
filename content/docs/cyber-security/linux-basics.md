---
title: "1.2. Linux Basics"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.2. Linux Basics

## Introduction

An operating system provides a way to **interact with the hardware components** of the computer, and provides an **execution environment for applications**.

The following functions are providing by an OS:
- CPU Management
- Memory Management
- Device Drives
- IO Management
- Applications

## Linux Base File System

The Linux filesystem is structured in accordance to the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html).

| Path | Description |
|:-----|:------------|
| `/sbin` | Binaries needed for administration (*sudo binaries*) |
| `/bin` | All system binaries |
| `/boot` | Files required for booting (e.g. Linux kernel and system.map) |
| `/dev` | All devices |
| `/etc` | Configuration files |
| `/home` | User home directories |
| `/lib` | Shared libraries (.so files) (DLLs in Windows or dylibs in macOS) |
| `/mnt` or `/media` | User mounted filesystems |
| `/opt` | Additional add-on packages |
| `/root` | Home directory for root (admin) user |
| `/usr` | Shareable read-only directory |
| `/var` | Log files, MySQL/database files, web server data files, email inboxes, etc. |

## File Permissions

File permissions in Linux specify the access allowed at **owner**, **group**, and **global** level, plus some additional **special attributes**.

A typical permission, in string form, could look something like this: `-rw-r--r--`. This shows that:
- It is not a directory (otherwise first `-` would be `d`)
- The owner (user) has read-write access to the file
- The group the owner is in has read access
- Everyone (other) else has read access

<table>
    <thead>
        <tr>
            <th>Special Attributes</th>
            <th colspan="3">User</th>
            <th colspan="3">Group</th>
            <th colspan="3">Other</th>
        </tr>
        <tr>
            <th>d</th>
            <th>r</th>
            <th>w</th>
            <th>x</th>
            <th>r</th>
            <th>w</th>
            <th>x</th>
            <th>r</th>
            <th>w</th>
            <th>x</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>-</td>
            <td>r</td>
            <td>w</td>
            <td>-</td>
            <td>r</td>
            <td>-</td>
            <td>-</td>
            <td>r</td>
            <td>-</td>
            <td>-</td>
        </tr>
    </tbody>
</table>

`x` means Execute permission, which allows that scope to run executable scripts.

### Octal Permissions

When using commands in Linux, you will notice that internally permissions are stored as a 3 or 4 digit number. This is the permission in **octal form**.

For example:
- `644` would be `-rw-r--r--` (same as above)
- `777` would be `rwxrwxrwx`
- `000` would be `---------`

Generally the larger each digit the more open the permissions are.

To calculate the octal permission, for each scope (user, group, global), write the binary of each permission, then take the value of the resultant number (as shown in the image below).

![Octal Permissions Calculation](/img/cyber-security/y1/octal-permissions.png)

### Special Permissions

- `d`: Directory (`d---------`)
- `s`: SUID or SGID depending on usage:
    - `rws------`: **SUID**, the file will always execute as the **user** that owns the file, no matter what user executes it.
    - `---rws---`: **SGID**, the file will always execute as the **group** that owns the file.
- `t`: Sticky bit (`d------rwt`), allows only the owner of the directory to delete files within it.

## Logs

Linux stores logs of just about everything that happens on the system. This is useful for solving issues, and also forensics.

Logs are stored in the `/var/log` directory.

Common log files:
- `auth.log` or `secure`: shows login events
- `apt/history.log` or `yum.log`: shows package manager events
- `syslog` or `messages`: shows kernel messages

## Time

Time in Linux is stored as a **Unix timestamp**. This is the number of seconds passed since 1st January 1970.

File access, modification, and creation times can easily be changed in Linux, which can make forensics more difficult.
