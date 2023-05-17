---
title: "1.15. Evidence Acquisition: RAM"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.15. Evidence Acquisition: RAM

Live forensics is when **live** system data is extracted before pulling the cord

This allows information stored in volatile memory to be retrieved, such as memory, and process and network information.

Live forensics is not a pure forensic response as it will have minor and undetermined impacts on the underlying operating state of the machine.

## Why Live Forensics?

- Minimal downtime (mission critical systems)
- Provides context for static analysis
- Some data is only stored in RAM (e.g. encryption keys, private browsing)
- Long data lifetime, even after days
- Evolution of the enterprise network (e.g. logon remotely)
- Evolution of data storage:
    - Terabytes of data on hard drive
    - Gigabytes of data in RAM

## Evidence Contained in RAM

- Running processes and services
- System information, such as time elapsed since last reboot
- Open network connections
- Recent web browsing activities, including private mode
- Unpacked/decrypted versions of protected programs
- Webmail and social networking logon sessions
- Running malware/Trojans

## Issues for Consideration

- Legal process
- Integrity (RAM forensics leaves footprint)
- Destroy evidence (accidentally or anti-forensics)
- Weigh the risk to the investigation
- Important/urgency (information on bomb threat vs evidence of fraud)

## Order of Volatility

1. Register, cache
2. Main physical memory
3. Virtual memory
4. Network status
5. Running processes
6. Hard drive
7. External storage media

## Acquisition

- The most volatile data should be collected first
- Two strategies:
    - Collect all and examine later
    - Use various tools to probe different aspects of the running system
- Tools are placed on a USB/DVD with a second drive used as the storage
