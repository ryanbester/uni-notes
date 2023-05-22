---
title: "2. IP Addressing"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 2. IP Addressing

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/sai/y1/tb2/2-ip-addressing)

## Internet Protocol (IP)

The **Internet Protocol** must be able to provide communications between hosts on different types of networks (different data-link implementations).

**IP Addresses** must include information about what network the receiving host is on to make routing feasible.

IP uses IP addresses to route information between networks, hence every device requires a unique address.

## IP Addresses

**IP Addresses** are different to the underlying data-link MAC address.

They are independent of hardware addressing and are only understood by software.

They are used by higher-layer protocols and applications.

Each host on the Internet has a unique 32-bit IP address (IPv4). It is divided into two parts:

- The prefix identifies the network (Network ID)
- The suffix identifies the host (Host ID)

### Network ID

**Network IDs** are assigned to organisations by a global authority:

- **American Registry for Internet Numbers (ARIN)** for the Americas
- **Réseaux IP Européens (RIPE)** for Europe, the Middle East, and Asia
- **Asia Pacific Network Information Centre (APNIC)** for Asia and Oceania

### Host ID

**Host IDs** are assigned locally by a system administrator and can be configured manually or through DHCP.

## Classful IP Addressing

Classful IP Addressing divides IP address into five groups.

- The initial bits determine the class
- The class determines the boundary between the prefix and suffix
- Three classes are used for networks. Class D and Class E are used for multicast and experimentation respectively.

![IP Address Classes](/img/sai/y1/ip-classes.png)

Larger prefix sizes allow for more networks. The more networks, the less hosts.

- **Total IP Addresses:** 4 billion:
    - **Class A**: 126 networks, 16M hosts
    - **Class B**: 16K networks, 64K hosts
    - **Class C**: 2M networks, 256 hosts

### Class A

126 networks with up to 16 million hosts.

1.0.0.0 - 127.255.255.255

- Start with binary 0
- All 0 reserved
- 01111111 (127) reserved for loopback
- Range 1.x.x.x to 126.x.x.x
- All allocated

### Class B

16,382 networks with up to 64,000 hosts.

128.0.0.0 - 191.255.255.255

- Start with binary 10
- Range 128.x.x.x to 191.x.x.x
- Second Octet also included in network address
- 2<sup>14</sup> = 16,384 Class B addresses
- All allocated

### Class C

2 million networks with up to 254 hosts.

192.0.0.0 - 223.255.255.255

- Start with binary 110
- Range 192.x.x.x to 223.x.x.x
- Second and third octet also part of network address
- 2<sup>21</sup> = 2,097,152 addresses
- Nearly all allocated

## Dotted Decimal Notation

IP Addresses are usually shown in **dotted decimal notation**.

```
10000000 10000111 01000100 00000101
128.165.68.5
```

This allows humans to avoid binary and makes it easier to type IP addresses.

## IP Address Assignment

An IP Address does not identify a specific computer, instead a connection between a computer and network.

A computer with multiple network connections (e.g. a router) must be assigned an IP address for each connection.

## Host and Network Addresses

- A single network interface is assigned a single IP address called the **host address**
- A host may have multiple interfaces and therefore multiple host addresses
- Hosts that share a network all have the same IP **network address** (the network ID)

## Special Addresses

- An **IP Broadcast Address** has a host ID of all 1s
- An IP address that has a host IDs of all 0s is called a network address and refers to an entire network
- Network addresses are not used in packets
- Loopback never leaves local computer

### Loopback Address

Addresses beginning with binary 01111111 or decimal 127 are **loopback addresses**.

They are reserved for loopback and internal testing on a local machine.

## Private IP Addresses

- Specific ranges of IP addresses set aside for use in private networks (RFC 1918)
- Use is restricted to private internets; routers in public Internet discard packets with these address
- Ranges
    - Range 1: 10.0.0.0 to 10.255.255.255
    - Range 2: 172.16.0.0 to 172.31.255.255
    - Range 3: 192.168.0.0 to 192.168.255.255
- Network Address Translation (NAT) is used to convert between private and global IP addresses.
