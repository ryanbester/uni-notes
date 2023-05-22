---
title: "4. Subnetting"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 4. Subnetting

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/sai/y1/tb2/4-subnetting)

## IP Address Problem

- Class A and B networks are too big
    - Very few LANs have close to 64,000 hosts
    - For electrical/LAN limitations, performance, or administrative reasons
- Address space depletion
    - Running out of Class A and B addresses, since Class C is too small for most domains
- Clsas B sparsely populated, but people refuse to give it back
- Large forwarding tables
    - 2 million possible Class C groups

## Solutions

- **Short-term solutions**:
    - Subnetting
    - Classless Inter-Domain Routing (CIDR), RFC 1518
    - New allocation policy (RFC 2050)
    - Private IP addresses set aside for intranets
- **Long-term solution**:
    - IPv6, with much bigger address space (128-bit)

## Subnet and Classless Addressing

- Not part of the original scheme
- Invented to prevent address exhaustion
- Allows the boundary between prefix and suffix to occur on an arbitrary bit boundary
- Requires auxiliary information to indentify the boundary

## Subnetting

- Goal: to extend address space
- Subnet addressing introduces another hierarchical level
- Transparent to remote networks
- Simplifies management of multiplicity of LANs
- Technique:
    - Assign single network prefix to site
    - Divide suffix into two parts: network at site and host
- Typical use: divide Class B addresses

## Address Mask

- Accompanies the IP address
- 32-bit binary value
- Specifies prefix/suffix boundary
    - 1s cover prefix (network)
    - 0s cover suffix (host)
- Masking used to find subnet number
- Performing a bitwise logical AND operation between the IP address and the subnet mask results in the Network Address or Number
    - For example: the Class B mask is 255.255.0.0

## Subnetting (Continued)

- Take a **network address** and break it up into subnets that can be assigned to individual physical networks
- Define a **subnet mask** to help create a new level of hierarchy in the addressing scheme
- The bitwise AND of the subnet mask with the full address gives the subnet number
- Group physically close networks to share a single Network ID
- Subnetting is not visible to the outside world. An organisation decides internally how to implement subnetting

![Subnetting](/img/sai/y1/subnetting.png)

## Subnetting Example

- Assume an organisation was assigned address 150.100
- Assume < 100 hosts per subnet
- So we need 7 host bits
- Therefore network mask is `11111111 11111111 11111111 10000000` or `255.255.255.128`
- Apply the subnet mask to IP addresses to find corresponding subnet

Example: find subnet for 150.100.12.176

```
IP Address : 10010110 01100100 00001100 10110000
Mask       : 11111111 11111111 11111111 10000000
AND        : 10010110 01100100 00001100 10000000
Subnet     : 150.100.12.128
```

## Calculating Available Subnets/Hosts

- To calculate the number of subnets (avoid the zero and broadcast subnet) or nodes, use the formula: **2<sup>n</sup> - 2**, where **n** is the number of bits in either field
- To calculate the number of subnets when using Classless routing protocol, RIP V2, EIGRP, or OSPF, use: **2<sup>n</sup>**
- Number of subnets * number of nodes per subnet = total number of nodes in class

### Example 1

```
IP Address : 10001100.10110011.11011100.11001000    140.179.220.200
Mask       : 11111111.11111111.11100000.00000000    255.255.224.000
AND        : 10001100.10110011.11000000.00000000    140.179.192.000
```

- 3-bit subnet mask is used
- Subnet address is calculated to be 140.179.192.000, as shown above
- Number of subnets = 2<sup>3</sup> - 2 = 6

### Example 2

- You are assigned a Class C network number: `200.133.175.0`
- You want to utilise this network across multiple small groups within your organisation
- Number of nodes you'll get without subnetting: 2<sup>8</sup> - 2 = 254
- You decide to break the network into 14 smaller subnets
    - To get 14 subnets, you need a subnet mask of 4 bits
    - Hosts per subnet: 2<sup>4</sup> - 2 = 14

## Routing with Subnets

- IP layer in hosts and routers maintain a **routing table**
- **Originating host**: to send an IP packet, consult routing table:
    - If destination host is in the same network, send packet directly uing appropriate network interface
    - Otherwise, send packet indirectly; typically, routing table indicates a default router
- **Router**: Examine IP destination address in arriving packet:
    - If destination IP address not own, router consults routing table to determine next-hop and associated network interface, then forwards packet

### Routing Table Example

| SubnetNumber | SubnetMask | NextHop |
|:-------------|:-----------|:--------|
| 128.96.34.0 | 255.255.255.128 | eth0 |
| 128.96.34.128 | 255.255.255.128 | eth1 |
| 128.96.33.0 | 255.255.255.0 | R2 |

## Additional Points

- The subnet mask does not need to align on byte boundaries
- It is possible to put multiple subnets on the same physical network, but hosts may then have to go through a router to talk to each other
- From outside the subnetted domain, the whole thing is viewed as a single network. For this reason, subnets should be kept geographically close
