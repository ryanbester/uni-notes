---
title: "1. Network Services"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1. Network Services

[🔒 Resources](https://github.com/ryanbester/uni-resources/tree/main/osi/y2/net/1-network-services)

## DHCP

- DHCP (Dynamic Host Configuration Protocol) was introduced in **1993**
- An improvement over BOOTP
  - Supports temporary allocation (leases) of IP addresses
  - Clients of DHCP servers can acquire **all IP configuration parameters** needed to operate
  - Minimal human interaction
- DHCP is the preferred method for dynamic assignment of IP addresses
- Compatible with BOOTP clients

### Motivation

- Before DHCP, there were two main methods of configuring network devices;
  - **Manual Assignment**, where each device is configured manually
  - **Bootstrap Protocol (BOOTP)**, where each device is given an IP address by a central server
- DHCP improves this by adding configuration parameters, including:
  - IP Address
  - Router Address
  - Subnet Mask
  - DNS Server Address
  
### Initial Message Flow

```plaintext
+---------+                 +---------+         +---------+
| ServerA |                 | Client  |         | ServerB |
+---------+                 +---------+         +---------+
     |                           |                   |
     |              DHCPDISCOVER | DHCPDISCOVER      | -----------------------------------------------------\
     |<--------------------------|------------------>|-| Client attempts to discover available DHCP servers |
     |                           |                   | |----------------------------------------------------|
     |                           |                   |
     | DHCPOFFER                 |         DHCPOFFER | ----------------------------\
     |-------------------------->|<------------------|-| Servers reply with offers |
     |                           |                   | |---------------------------|
     |                           |
 -----------------------------------------------------------\
 | Client collects offers and decides which offer to accept |
 |----------------------------------------------------------|
     |                           |                   |
     |                           |                   |
     |               DHCPREQUEST | DHCPREQUEST       | -----------------------------------------------------------\
     |<--------------------------|------------------>|-| Client broadcasts request for one of the received offers |
     |                           |                   | |----------------------------------------------------------|
     |                           |                   |
     |-------------------------\ |           DHCPACK | --------------------------------------------------\
     || Configuration complete |-|<------------------|-| Server acknowledges client's user of IP address |
     ||------------------------| |                   | |-------------------------------------------------|
     :                           :                   :
     :                           :                   :
     |     --------------------\ | DHCPRELEASE       | -----------------------------------------------\
     |     | Graceful shutdown |-|------------------>|-| Client explicitly releases use of IP address |
     |     |-------------------| |                   | |----------------------------------------------|
     |                           |                   |
```

### IP Release and Renew

- An IP address is released when the client is **shut down** or **terminates the network connection**
  - The IP address **returns to the IP pool** of the DHCP server
  - It is available for another client to use
- A lease is **renewed** when **50%** of the lease time has elapsed
  - Request is sent to the DHCP server
  - If the initial DHCP is not available then the request is broadcasted to all other DHCP servers available

### Advantages

- Prevents the network administrator from doing a lot of manual configuration work
  - Especially in large networks with 100+ clients
- Able to move a device from one network to another and gain instant connectivity
- More **efficient utilisation** of available IP addresses, since inactive clients do not receive an IP address

### Disadvantages

- DHCP packets are **UDP packets**
  - Can lead to **unreliable and insecure operations**
- Potential for **unauthorised clients**
  - Apply **MAC address filtering** to mitigate
- Potential for **malicious DHCP clients and servers**
  - Supplying incorrect configuration parameters
  - Exhaustion of IP address pool

## DNS

- DNS (Domain Name System) is used to translate names to IP addresses on the internet
- A **globally distributed**, **scalable**, and **reliable** database
- Consists of three components:
  - A **name space**
  - **Servers**: make that **name space** available
  - **Resolvers (Clients)**: Query the **Servers** about the **name space**

### DNS as a Lookup Mechanism

- Users generally prefer names to numbers
- But computers prefer numbers to names
- DNS provides the mapping between the two

### Global Distribution

- Data is **maintained locally**, but **retrievable globally**
  - No single computer has all the DNS data
- DNS lookups can be performed on any device
- Remote DNS data is usually cached locally to improve performance

### Loose Coherency

- The database is always **internally consistent**
  - Each version of a subset of the database (known as a **zone**) has a **serial number**
    - This serial number is incremented on each database change
- Changes to the master copy of the database are **replicated** according to a **timing** set by the **zone administrator**
- Cached data expires according to a **timeout** set by the **zone administrator**

### Scalability

- There is **no limit** to the **size** of the database
  - It could store many millions of domain names, but is not particularly a good idea
- **No limit** to the **number of queries**
  - Tens of thousands of queries are easily handled every second
- Queries are **distributed** among the network of primary and secondary DNS servers and caches

### Reliability

- Data is **replicated**
  - Each **secondary server** replicates the data from the **primary server**
- Clients can query:
  - The primary server
  - Any of the secondary servers
- Clients will usually query local caches first
- DNS uses either UDP or TCP (on port 53)
  - TCP is for communication between servers (e.g. for replication)
  - UDP is for communication between clients and servers (e.g. for name lookups)

### Dynamicity

- The database can be updated dynamically
  - Only the **primary server** can be dynamically updated
  - Add/modify/delete of any record
- Modification of the primary database triggers a replication to the secondary servers

### Domain Names

- A domain name is the sequence of labels from a node to the root, separated by periods (`.`), read left to right
  - `uninotes.ryanbester.com`
  - The name space has a **maximum depth of 127 levels**
  - Domain names are limited to **255 characters in length**
- A node's domain name identities it's position in the name space

#### Domain Name Structure

```plaintext
                              ┌───┐
                              │ . │
                              └─┬─┘
             ┌──────────────────┴─┬────────────────┐
          ┌──┴──┐              ┌──┴──┐           ┌─┴──┐
          │ com │              │ net │           │ uk │
          └──┬──┘              └──┬──┘           └─┬──┘
      ┌──────┴──────┐       ┌─────┴─────┐     ┌────┴─────┐
┌─────┴──────┐  ┌───┴────┐  │ minecraft │   ┌─┴──┐     ┌─┴──┐
│ ryanbester │  │ google │  └───────────┘   │ ac │     │ co │
└─────┬──────┘  └────────┘                  └─┬──┘     └─┬──┘
 ┌────┴─────┐                              ┌──┴───┐  ┌───┴────┐
 │ uninotes │                              │ port │  │ google │
 └──────────┘                              └──────┘  └────────┘
```

#### Subdomains

- A domain is a subdomain of another if its domain name ends in the other's domain name.

```plaintext
 https  ://  uninotes . ryanbester . com
 =====       ========   ==========   ===
Protocol     Subdomain  Domain name  TLD
```

### (Domain) Name Servers

- Name servers store information about the name space in units called **zones**
  - The name servers that serve a **complete zone** are known to be **authoritative** for that zone
- More than one name server can be authoritative for the same zone
  - Ensures redundancy and spreads the load
- A single name server can be authoritative for many zones

### Types of Name Servers

- There are two main types of servers:
  - **Authoritative**: Maintains the data
    - **Primary**: Where the data is modified
    - **Secondary**: Where the data is replicated to
  - **Non-authoritative** or caching: Stores the data obtained from an authoritative server
- No special hardware is needed for a name server

### Name Resolution

- **Name Resolution** is the process in which local resolvers and name servers work together to find data in the name space
- Upon receiving a query from a resolver (client), a name server:
  1. Looks for the answer in its cache and authoritative data
  2. If Step 1 fails, the query must be passed to other servers

### The Resolution Process

#### Iterative Resolution

1. The workstation `alice` asks its configured name server, `dave` for `www.ryanbester.com`'s address
2. The name server `dave` asks a root name server `m.root-servers.net`, for `www.ryanbester.com`'s address
3. The root server `m.root-servers.net` refers `dave` to the `com` name servers
   - This type of response is called a **referral**
4. The name server `dave` asks a `com` name server `f.gtld-servers.net` for `www.ryanbester.com`'s address
5. The `com` name server refers `dave` to the `ryanbester.com` name servers
6. The name server `dave` asks a `ryanbester.com` name server, `ns1.ryanbester.com` for `www.ryanbester.com`'s address
7. The name server `ns1.ryanbester.com` responds with `www.ryanbester.com`'s address
8. The name server `dave` responds to `alice` with `www.ryanbester.com`'s address

#### Caching

- After the previous query, the name server `dave` now knows the following information:
  - The **names** and **IP addresses** of the `com` name servers
  - The **names** and **IP addresses** of the `ryanbester.com` name servers
  - The **IP address** of `www.ryanbester.com`
- This data is stored in a cache on `dave`
- The process now, with the cache, is as follows:

1. The workstation `alice` asks its configured name server, `dave` for `uninotes.ryanbester.com`'s address
2. `dave` has cached an NS record indicating `ns1.ryanbester.com` is a `ryanbester.com` name server, so it asks it for `uninotes.ryanbester.com`'s address
3. The name server `ns1.ryanbester.com` responds with `uninotes.ryanbester.com`'s address
4. The name server `dave` responds to `alice` with `uninotes.ryanbester.com`'s address

### The Root Nameservers

- The root zone file lists the names and IP addresses of the authoritative DNS servers for all the TLDs
  - <https://www.iana.org/domains/root/db>
  - <https://data.iana.org/TLD/tlds-alpha-by-domain.txt>
- The root zone file is published on 13 servers, `A` to `M`, around the Internet
  - <https://www.iana.org/domains/root/servers>
- Root name server operations are currently provided by volunteers by a very diverse set of organisations

### Load Concerns

- DNS is capable of handling the load
  - The DNS root servers get approximately 3000 queries per second
    - DDoS attacks have proved root name servers can handle 50,000 queries per second
    - The limitation is the network bandwidth, not the DNS protocol
  - The `in-addr.arpa` zone, which translates numbers to names, gets about 2000 queries per second

### Performance Concerns

- DNS is a very lightweight protocol
  - Simple query and response
- Any performance limitations are the result of **network limitations**
  - Speed of light
  - Network congestion
  - Switching/forwarding latencies

### Security Concerns

- Base DNS protocol (RFC 1034, RFC 1035) is **insecure**
  - **DNS spoofing** (or cache poisoning) attacks are possible
- **DNS Security Enhancements** (DNSSEC, RFC 2565) fixes this flaw
  - But creates new ones, such as DoS attacks and [amplification attacks](https://nirlog.com/2006/03/28/dns-amplification-attack/)
- DNSSEC strongly discourages large flat zones
  - Hierarchy (delegation) is good
