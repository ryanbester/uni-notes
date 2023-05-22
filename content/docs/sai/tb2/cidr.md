---
title: "6. Classless Inter-Domain Routing"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 6. Classless Inter-Domain Routing

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/sai/y1/tb2/6-cidr)

## Classless Addressing

**Classless Addressing** was invented to prevent IPv4 address exhaustion.

It allows the boundary between prefix and suffix to occur on an arbitrary bit boundary.

Requires additional information to identify the bounday.

## Address Assignment Efficiency

- 2-host network: assigned a Class C address
    - Efficiency: 2/254 = 0.78%
- 256-host network: assigned a Class B address
    - Efficiency: 256/65,534 = 0.039%
- 4000-host network: assigned a Clsas B address
    - Efficiency: 4000/65,534 = 6.1%

## Autonomous Systems and Interdomain Routing

- In order to provide network scalability, we approach the problem of routing using a hierarchial view of the system
- We define **domains** or **autonomous systems** as interconnected collections of physical networks
- Inside an AS, routers use protocols such as RIP or OSPF
- Once ASes are interconnected, we can define another level of routing

## Example

- Say Network A wants 4000 IP addresses
- With a Class B address this would be 4/64 = 6.1% utilisation, which is a waste of a Class B address
- Another option would be to give Network A 16 random Class C addresses, but this could be too much routing overhead

This is where CIDR comes into play:

- With CIDR: Create a new class with a 20-bit Network ID
    - For example: `<192.4.16.0, 255.255.240.0>` or `192.4.16/20`

## CIDR

The goal of CIDR is to minimise the number of routes that a router needs to know while keeping address assignment efficiency high by giving out contiguous blocks of Class C addresses.

![CIDR Example](/img/sai/y1/cidr-example.png)

- Allows an arbitrary split between the network and host part of an IP address
    - Does not use classes to determine Network ID
    - Uses common part of address as the network number
    - Uses slash notation
        - For example: addresses 192.4.16 - 192.4.31 have the first 20 bits common. This becomes the network number so `192.4.16/20`
        - This means that the boundary between prefix and suffix occurs after the first 20 bits
- Each network can be as large or small as needed
    - Assign contiguous blocks of Class C addresses
    - IP address assignment reflects physical topology of network
    - Each block must contain a number of Class C networks that is a power of 2
- Enables more efficient usage of address space and router tables
    - Use interdomain routing that understands classless addresses - routes according to prefix of address, not class
    - Use single entry for range in forwarding tables
    - Combined forwarding entries when possible
- CIDR deals with the Routing Table Explosion Problem
    - Pre-CIDR: Network with range of 16 contiguous Class C blocks requires 16 entries
    - Post-CIDR: Network with range of 16 contiguous class C blocks requires 1 entry

## CIDR vs Subnetting

- **CIDR**: Group multiple addresses within a single network authority
- **Subnetting**: Share one (network) address among multiple (physical) networks
    - Simplifies routing
    - Improves addressing (as it groups networks together)

![CIDR vs Subnetting](/img/sai/y1/cidr-vs-subnetting.png)

## Address Resolution Protocol (ARP)

The **Address Resolution Protocol** is used by a sending host when it wants the hardware address for a destination when it knows the IP address.

ARP is a broadcast protocol; every host on the network receives the request.

Each host checks the request against it's IP address - the right one responds.

ARP does not need to be done every time an IP datagram is sent, the hosts remember the hardware addresses of each other.

Part of the ARP protocol specifies the receiving host should also remember the IP and hardware addresses of the sending host.

![ARP](/img/sai/y1/arp.png)

## Reverse Address Resolution Protocol (RARP)

**Reverse Address Resolution Protocol** is used to find out the IP address of a host given a hardware address.

Reverse address resolution is needed by diskless workstations when booting.

![RARP](/img/sai/y1/rarp.png)
