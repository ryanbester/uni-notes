---
title: "1.13. Evidence Acquisition: Hard Drives"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.13. Evidence Acquisition: Hard Drives

## Methodology

1. Acquire an image/copy of the original seized evidence (ensure that you don't alter it)
2. Authenticate that the image is the same and that the original has not changed
3. Analyse the data on the copy only

Forensic acquisition should be performed correctly, otherwise it may invalidate the results of later analysis.

## Imaging Variables

Several different variables could affect the imaging process.

This ranges from the imaging method to different storage technologies.

![Imaging Variables](/img/cyber-security/y1/imaging-variables.png)

## Imaging

- **Physical acquisition**: A bit-for-bit copy of the original hard drive
    - This is the preferred and gold standard for forensic acquisition
    - Includes slack and unallocated space
    - Error handling
- **Logical imaging**: Acquires only the logical drive
    - Many logical partitions per physical drive
    - A logical partition can span many physical drivers, this is particularly useful in RAID configurations for reconstruction

An external hard drive reader can be used for acquisition.

## Acquisition Formats

- **Raw Format**: (for example, output from `dd`)
    - Bit-by-bit copy of the drive
    - Generates the same size image as original
- **E01**:
    - Expert Witness format (Encase format)
    - A container of evidence and metadata (including hash values)
    - Can be compressed
- **AFF**:
    - Advanced Forensic format
    - A container of evidence and metadata
- **Ex01**:
    - Format for Encase v7
    - More extensible than E01
    - A container of evidence and metadata (including hash values)

## Output Data Destination

- **To a disk**:
    - What happens when the destination disk is bigger than the source disk?
    - What if the acquisition system mounts the destination disk?
- **To a file**:
    - Easy to know the boundaries of the data, and the OS will not try to mount it automatically
    - Images can be compressed, password protected, and broken into smaller pieces

## Integrity of Evidence

It is important that the data is not modified in any way during forensic extraction and analysis.

### Write Blockers

A device which allows the drive to be read without allowing the possiblity of accidentally writing data.

They can be hardware- or software-based, and can also provide protection by limiting the speed of the drive attached to the blocker.

#### Hardware Write Blockers

- Sits in connection between the computer and storage device
- Monitors the commands that are being issued and prevents the write command

![Hardware Write Blocker](/img/cyber-security/y1/hardware-write-blocker.gif)

#### Software Write Blockers

- Modifies the interrupt table, which is used to locate the code for a given BIOS service

![Software Write Blocker](/img/cyber-security/y1/software-write-blocker.gif)

### One-way Hash Function

- To ensure integrity a mechanism is employed that can create a **fingerprint** of the data
- Hash functions allow a fixed length output to be created from a variable length input
- The slightest change in the file will yield a completely different hash value
