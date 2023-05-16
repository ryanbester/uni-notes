---
title: "1.9. Hardening"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.9. Hardening

## Access Control

There are three main elements of access control in Unix:

- **Principles**: UIDs and GIDs, Superuser UID=0
- **Subjects**: Processes (PID) created by `exec()` or `fork()`
- **Objects**: Files (files, directories, drivers, etc)

## Service Enumeration

There are many ways to find out about the system:

`/usr/bin/uname -a`, `/usr/bin/df -ah`, `/usr/bin/env`, `/usr/bin/ps -ef | grep root`, `/usr/bin/ps -ef | /usr/bin/awk ‘{print $8}’ | /usr/bin/xargs -r ls -al 2>/dev/null`, `/usr/bin/systemctl list-unit-files (old versions are init/inet)`, `/usr/ls -al /etc/cron*`, `/sbin/ip -a`, `arp -a`, `route`, `more /etc/resolv.conf`, `netstat -antp || netstat -anupsudo -V`, `nmap -V ... etc`, `find / -name $search-term 2>/dev/null`, `top`, `lsmod`, `modinfo $modulename`, `history (~/.bash_history)`, etc

## Environment Variables

- **PATH**: Search path for shell commands
- **TERM**: Terminal type
- **HOSTNAME**: Name of Unix host
- **PRINTER**: Default printer
- **HOME**: Path to home directory
- **PS1**: Default prompt
- **IFS**: Characters separating command line arguments

## Hardening Methods

- Add new and manage existing defences
- Fix known vulnerabilities (install updates)
- Remove/turn off unneeded services
- Manage users and groups
- Manage access permissions

### OS Security

- Manage user accounts (SELinux)
- Updating the operating system
- Enabling a firewall
- Disabling guest accounts
- Monitoring logs
- Checking file permissions

### Australia Governement Guidance

- Use unique restricted users for key at-risk services
- Apply additional forms of security policy enforcement (SELinux or AppArmor)
- Implement appropriately hardened security configurations and permissions of key configuration files
- Perform tasks with least privileges
- Centralise auditing and analysis of system and application logs
- Disable unrequired operating system functionality
- Implement specific configurations based on server roles
- As far as practical, implement vendor security guidance for specific Linux distributions

### Hardening Standards

There are standards relating to proper system hardening, such as the [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/) and [NIST](https://nvd.nist.gov/config/cce/index).

### Password Policies

- Enable password policies (`/etc/pam.d/common-password`)
- Enforce password history of 3 (add `remember=3` to end of line with `pam_unix.so`)
- Enforce password length of 6 (add `minlen=6` to end of line with `pam_unix.so`)
- Enforce password complexity with one of each character (add `ucredit=-1 credit=-1 dcredit=-1 ocredit=-1` to end of line with `pam_cracklib.so`)
- Set password history (`/etc/login.defs`)
- Maximum password duration (`PASS_MAX_DAYS 90`)
- Minimum password duration (`PASS_MIN_DAYS 10`)
- Days before expiration to warn users to change password (`PASS_WARN_AGE 7`)

### Account Policies

At end of `/etc/pam.d/common-auth` add `auth required pam_tally2.so deny=3 onerr=fail unlock_time=1800`.

`deny=3` is the number of failed attempts before a lockout time of 30 mins (`unlock_time=1800`).

### Audit

[Lynis](https://cisofy.com/lynis/) is a tool that can be used for security auditing and compliance testing.

It checks the system for any security weaknesses and vulnerabilities, and checks against standards such as the CIA Benchmarks and NIST.

### User Database

Stored in `/etc/passwd`, each line contains the username, UID, GID, home directory, and default shell.

### SELinux

**SELinux** is a kernel level Mandatory Access Control (MAC) implementation for Linux. It was originally built for NSA.

There are three types of access control:
- **MAC - Mandatory Access Control**:
    - Cannot be bypassed
    - Only the owner of the system can grant access to others
- **DAC - Discretionary Access Control**:
    - Objects are owned by a principal, who can grant access to whomever they like
- **RBAC - Role Based Access Control**:
    - Access is granted based on your current role

### Apache Hardening

- Disable directory browsing
- Restricting access
- Disabling banners
- Configuring with an "apache" user

## Snort

[Snort](https://www.snort.org/) is a packet analysis tool for intrusion detection.

It sniffs the network traffic and checks for malicious traffic with pre-defined rules.

Operates in three parts:

- **Preprocessor**: Packets are examined
- **Detection**: Perform single tests on a single aspect of a packet
- **Output**: Report results to other plugins

## Tripwire

**Tripwire** is a tool which monitors when changes happen to a file. It is used as shown below:

`twadmin --create-polfile --cfgfile tw.cfg --site-keyfile site.key twpol.txt`

`tripwire --init --cfgfile /etc/tripwire/tw.cfg --polfile /etc/tripwire/tw.pol --site-keyfile /etc/tripwire/site.key --local-keyfile /etc/tripwire/site.key`

`tripwire --check`
