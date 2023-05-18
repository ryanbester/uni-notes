---
title: "1.19. File Allocation"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.19. File Allocation

## File Systems

A file system is underlying structure a computer uses to organise data on a storage device. It:

- Provides data storage and retrieval
- Associates file names with data
- Organises files into parent directories
- Stores file attributes (metadata), such as modify, access, creation (MAC) times, size, and permissions
- Maintains a list of unallocated data units

Examples of file systems include: FAT32, NTFS, HFS+, ext4

### File System Behaviours

File systems all handle the following operations:

- Create
- Delete
- Open
- Close
- Read
- Write
- Rename
- Change Attributes

## Link to Forensics

The attributes provided by a file system can provide evidence of criminal activity.

- **File content**: Directly useful in most cases
- **Name**: Provides indication on what the file is about
- **MAC times**: Can be used to perform timeline analysis

The raw data itself can also be analysed, such as slack space analysis and data carving.

## File Creation

When a new file is created, or an existing file is made larger, the file system finds unallocated space and allocates it to the file.

There are different allocation strategies, such as first available, next available, or best fit.

## Sectors and Clusters

A **sector** is the smallest addressable storage unit on the storage device

- This is typically 512 bytes
- The optimal method of storing a file in in a contiguous series
- A 600-byte file quires 1+n sectors

A **cluster** is the smallest unit at the OS level

- Can consist of one or more consecutive sectors
- The number of sectors in a cluster is always an exponent of 2


The command `fsutil fsinfo ntfsinfo c:` can be used to show the sector/cluster usage on Windows.

## Storing Data with Bitmaps

A bitmap is a data structure which has a bit for each cluster on the device

1 marks the cluster as allocated, whereas 0 marks the cluster as unallocated.

- **Advantages**:
    - Simple
    - Fast allocation check
    - Fast deletion
    - Fixed cost
    - Low storage overhead (0.003% for NTFS)
- **Disadvantages**:
    - Wasteful on larger disks
    - Poor scalability
    - Disk fragmentation

## Content Allocation Strategies

- **First Available**:
    - Searches sequentially for an available cluster, starting with the first in the file system
- **Next Available**:
    - Starts the search with the cluster that was most recently allocated
- **Best Fit**:
    - Searches for consecutive clusters that fit the needed amount of data

Best Fit reduces the risk of data fragmentation.

## Back to Forensics

- Data is not deleted when pressing delete
    - The cluster is just flagged as free
    - The data can be retrieved until the cluster is overwritten
- A large file may take time to be completely overwritten
- A small file may escape being overwritten depending on the allocation strategy

## Slack Space

Slack space occurs when the size of a file is not an exact multiple of a cluster size.

**RAM slack** is the area from the end of the file to the end of that sector.

**File slack** is the area from the end of RAM slack to the end of the cluster.

Data can be hidden in the slack space with appropriate applications, such as `bmap`.

## Master Boot Record

**MBR** is used to store essential information about the structure of a hard disk.

It is always located at cylinder 0, head 0, sector 0, and is where the BIOS can find information on how to proceed boot up and loading the OS.

The MBR is split into three parts:

- **Boot Code (446 bytes)**: When this code is executed, it hands over control to the consecutive boot (active) partition in order for the OS to be loaded.
- **Partition Table (64 bytes)**: Contains the information about the partitions on the disk, one of them will be marked as active.
- **MBR Signature (2 bytes)**: Always `0x55 AA`

![MBR Structure](/img/cyber-security/y1/mbr-structure.png)

## Partition Table

- The first partition table starts at address 0x1be in the MBR
- Each entry consists of 16 bytes and all multi-byte fields and little-endian
- Boot flag (Active: `0x80`, Inactive: `0x00`)
- Partition types, including FAT 21 (`0x01`), FAT 16 (`0x04`), Extended (`0x05`), and NTFS (`0x07`)

![MBR Partition Structure](/img/cyber-security/y1/mbr-partition.png)
