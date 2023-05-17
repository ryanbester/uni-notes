---
title: "1.16. Hashing"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.16. Hashing

**Hash functions** allow a fixed length output to be produced from a variable length input (strings, files, or disks)

Popular hashing algorithms include:

- MD5 (Message Digest 5) 128-bit
- SHA-1 (Secure Hash Algorithm) 160-bit
- SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)

## Key Characteristics

- Given `M`, it is easy to compute `h` such that `H(M) = h`
- Given `h`, it is hard to computer `M` (one-way or trapdoor property)
- Given `M`, it is hard to find another message `M`, such that `H(M) = H(M)` (Strong Collision Resistance)
- Changing one bit of input changes ~50% of the output bits

`MD5(password) = 5f4dcc3b5aa765d61d8327deb882cf99`

`MD5(Password) = dc647eb65e6711e155375218212b3964`

## Usage of Hashing

- Digital Forensics:
    - Verify the integrity of images
    - Data filtering: National Software Reference Library (NSRL) database
- Security:
    - Paswords
    - Antivirus

## Tools

- md5sum
- md5deep suite
- hashdeep
- ssdeep
- certUtil
- HashTab
- HashMyFiles
- FTK Imager
