---
title: "3. DNS"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 3. DNS

[🔒 Lab Sheet and Recordings](https://github.com/ryanbester/uni-resources/tree/main/sai/y1/tb2/3-dns)

## Hostnames

IP addresses are good for computers but difficult for humans to remember.

**Domain Name System (DNS)** is an automated system used to translate names (known as hostnames) to IP addresses.

## Domain Name System

- Used to map host names to IP addresses on th eInternet
    - Also called *name resolution* or *address resolution*
    - A configuration file has to be manually edited whenever a host is added
- Name resolution is an essential Internet function implemented as an application-layer protocol
- Domain name information is maintained through a **distributed database** of hostname/IP address pairs

## Distributed, Hierarchial Database

The Internet Domain Name System is probably the largest distributed database.

There are 13 root name servers worldwide.

![DNS Servers](/img/sai/y1/dns-servers.png)

## DNS Functionality

- Returns the computer's IP address given the name of a computer
- Uses distributed lookup
- Some domain names map to multiple IP addresses, e.g. multiple servers, load balancing
- Some IP addresses map to multiple domain names, e.g. aliasing of a web server
- Some domain names are virtual; maps to an IP address but the host is shared

## DNS Components

There are two main DNS components:

- **Name Server (DNS Server)**:
    - Supports name-to-address and address-to-name resolution
    - Exists at all levels of hierarchy
- **Name Resolver (DNS Client)**:
    - Is linked into each application via a DLL
    - Can contact DNS server to lookup names
    - Used by browsers, email clients, and client utilities such as `ping` and `tracert`

### Name Server

- **Root name servers**:
    - Contacts **authoritative name server** if the name mapping is not known
    - Gets mapping
    - Returns mapping to local name server
- **Top-level domain (TLD) servers**:
    - Responsible for com, org, net, edu, etc
    - Also for all top-level country domains, such as, uk, fr, ca, jp
- **Authoritative DNS servers**:
    - An organisation's DNS servers, providing authoritative hostname to IP mappings for an organisation's servers
    - Can be maintained by the organisation or service provider
- **Local DNS servers**:
    - Does not strictly belong to a hierarchy
    - When a host makes a DNS query, the query is sent to its local DNS server
        - Acts as a proxy, forwards query into hierarchy
        - Configured with well-known root servers

### Name Resolver

- The resolver becomes a client by contacting a DNS server
- Each resolver is configured with the address of one or more local domain name servers
- The resolver forms a DNS request message
    - The message is sent to the local DNS server
    - Waits for the server to send a DNS reply message

## Domain Names Syntax

Domain names are alphanumeric segments separated by dots.

For example: www.ryanbester.com.

There can be up to 127 levels in the tree.

- Usually no more than 5 or 6 are used.
- Each level is identified by a character string of up to 63 bytes, but a FQDN can only be 255 or less

Domain names are *not* case sensitive.

## Domain Namespaces

- The root level domain is `.`
- Top level domains include com, org, net
- Second-level domains are often owned by companies and individuals
- A subdomain is a further division of a second-level domain

Every domain name actually ends with `.` (the root level domain), but this is usually omitted.

### Top Level Domains

- There are a limited number of TLDs
    - edu, gov, com, net, org, mil, ...
- Countries each have a top level domain (2 letter domain name)
- TLDs are either **generic** or **restricted**
    - **Generic** TLDs are generally available
    - **Restricted** TLDs can only be used by specific groups or government agencies
- DNS allows organisations to use a geographic registration

### Second-level Domains

- Second-level domains, such as `ryanbester.com` have control over naming within their domain
    - They can create hosts such as `www`, and `ftp`
- A name suich as `www.ryanbester.com` is a Fully Qualified Domain Name (FQDN)

## Host Names

- The first portion of a URL is typically a host name
- This is usually different from the computer name
- Many hosts can be associated with the same server
- Many organisations assign domain names that reflect the service a computer provides

![DNS Host Names](/img/sai/y1/dns-hostname.png)

## How DNS Works

During a standard DNS lookup:

- Application sends a request to the local DNS server
- The local server:
    - If the answer is known, returns the response
    - If the answer is unknown:
        - Starts at root-level server
        - Follows links
        - Returns response

DNS uses the well-known port 53.

DNS supports two paradigms of queries:

- **Iterative**:
    - Each name server responds directly to the client with either the final answer or the IP address of another name server that should know the answer
    - It is up to the client to query the next name server
- **Recursive**:
    - The local name server determines the answer by iteratively or recursively querying other name servers

Most requests are answered via a combination of both recursion and iteration. The results may be cached.

![DNS Queries](/img/sai/y1/dns-queries.png)

## Categories of DNS servers

- **Primary Server**:
    - Defines the hosts for the domain
        - Maintains a database for the domain
        - Each represents a small part of the distributed database
    - It has **authority** for the domain
        - Root name servers are authoritative for all TLDs
- **Secondary Server**:
    - Gets data from primary server
    - Provides fault tolerance and load distribution
- **Caching Server**:
    - Resolves host names
    - Caches the result until the data expires
    - Automatically installed when the DNS is installed
    - No configuration necessary
- **Forwarding Server**:
    - Caching server that has access to the Internet and forwards traffic from other caching servers

## DNS Caching

- Improves efficiency
    - Quick response for repeated translations
    - Other queries may reuse some parts of lookup
- Eliminates unnecessary searches

Cached data periodically times out, defined by the TTL (Time to Live) controlled by the data owner.

## Zones

A zone is a part of the domain namespace.

- For a domain as small as `ryanbester.com`, the domain name represents a single zone
- For large organisations, subdomainds can be divided into separately maintained zones
    - Each zone typically has a separate DNS
- Host name assignments are maintained through zone files on the primary DNS server
    - The secondary server retrieves this from the primary server
- Forward lookup zones map the hostname to the IP address, whereas reverse lookup zones do the opposite

## DNS Records

Common DNS records:

| DNS Record | Function |
|:-----------|:---------|
| Address (A) | Associates a host name to an IP address |
| Canonical name (CNAME) | Creates an alias for a specified host |
| Internet (IN) | Identifies Internet records; precedes most DNS record entries |
| Mail Exchanger (MX) | Identifies a server used for processing and delivering email for the domain |
| Name Server (NS) | Identifies DNS servers for the DNS domain |
| Pointer (PTR) | Performs reverse DNS lookups. Resolves an IP address to a host name |
| Start of Authority (SOA) | Identifies the DNS server with the most current information for the DNS domain |

### The A Record

- Maps a domain name to an IP address
- DNS classifies bindings as **type A**
- Contains an IP address

### The CNAME Record

- Similar to a symbolic link in a file system, it contains an alias for another DNS entry
- Allows an organisation to change the computer used for a particular service without changing the names or addresses
- Also allows an organisation to associate multiple aliases with a single computer

## Reverse Lookup and IN-ADDR.ARPA

The in-addr.arpa domain is used for reverse DNS lookups.

If `host.company.com` maps to the IP address `A.B.C.D`, then `D.C.B.A.in-addr.arpa` maps to `host.company.com`

## DNS Tools

`ping` displays name resolution even if the computer cannot be contacted.

`nslookup` displays information from the DNS server.

`dig` available on Linux.
