---
title: "1. The Virtual Network"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1. The Virtual Network

[🔒 Lab Sheet and Recordings](https://github.com/ryanbester/uni-resources/tree/main/sai/y1/tb2/1-virtual-network)

## What is a Computer Network?

A **computer network** is a collection of devices that are all interconnected.

Components of a network include:

- **Hosts** (computers, printers, etc)
- **Links** (coaxial cable, twisted pair, optical fibre, radio, satellite)
- **Switches/routers** (intermediate systems)

The goal of a computer network is to provide ubiquitous access to resources, and allow remote users to communicate.

## Network Operating System

A Network Operating System, or **NOS**, expands the role of a normal OS, in that it offers:

- A remote file system
- Running of shared applications
- Input and output to shared network devices
- CPU scheduling of networked processes

## Types of Networks

Networks can be classified in different ways:

- **Based on management method**: Peer-to-peer, client/server
- **Based on network size**: LAN, WAN, and MAN
- **Based on topology**: Bus, Star, Ring, etc
- **Based on transmission media**: Wired (UTP, coaxial, fibreoptic), and Wireless

### Peer-to-peer Networks

A peer-to-peer network contains no fixed clients or servers.

Resources are hosted on other clients on the network.

### Client/Server Based Networks

The client/server model involves requests and replies.

Requests are sent to the central server from a client and the server responds to the client with the requested resource.

## Microsoft Networking Models

- **Workgroups**:
    - Peer-to-peer
    - A logical grouping of several computers whose work or users are connected and share their resources
- **Domains**:
    - Client/server
    - A type of workgroup that includes a server
    - Management made easy with Server Management application
    - Discretionary access control
    - A domain contains a **domain controller**, **member servers** (optional), and **workstations or clients**

## Communications Model

![Communications Model](/img/sai/y1/communications-model.png)

## Multiplexing

**Multiplexing** allows multiple channels or users to share link capacity.

Multiplexing devices or mechanisms:

- **Multiplexor**:
    - Accepts data from multiple sources
    - Sends data across a shared channel
- **Demultiplexor**:
    - Extracts data from a shared channel
    - Sends to the correct destination

Types of multiplexing:

- Frequency Division multiplexing
- Time Divison multiplexing
- Statistical multiplexing

### Frequency Division Multiplexing (FDM)

- Circuit mode (constant bandwidth) multiplexing technique
- Multiple items are transmitted simultaneously
- Each channel is allocated a particular portion of the bandwidth (known as bands)
- All modulated signals are carried simultaneously (as a composite analog signal)
- Example: TV, radio

![Frequency Division Multiplexing](/img/sai/y1/fdm.png)

### Synchronous Time Division Multiplexing

- Circuit mode (constant bandwidth) multiplexing technique
- Divides time into equal-sized quanta
- Assigns each quanta to flows on the physical link in a round-robin fashion.

![Time Division Multiplexing](/img/sai/y1/tdm.png)

### Statistical Multiplexing

With **statistical multiplexing**, each flow is broken into packets and sent to a switch, which can deal with the arriving packets according to a policy, such as, FIFO, round-robin, etc.

Unlike circuit mode multiplexing, statistical multiplexing allows for variable bandwidth.

## Circuit Switching

- Source first establishes a connection (circuit) to the destination
    - Each router or switch along the way may reserve some bandwidth for the data flow
- Source sends the data over the circuit
    - No need to include the destination address with the data since the routers know the path
- The connection is torn down

An example of circuit switching is the telephone network (analog).

- **Advantages**:
    - Fast and simple data transfer, once the circuit has been established
    - Predictable performance since the circuit provides isolation from other users, e.g. guaranteed bandwidth
- **Disadvantages**:
    - In bursty traffic, circuit will be idle for significant periods of time
    - Users with different bandwidth needs may need to use multiple circuits

## Packet Switching

- A form of **statistical time-division multiplexing**
- Source sends information as self-contained packets that have an address
    - Source may have to break up single message into multiple packets
- Each packet travels independently to the destination host
    - Packets are passed from node to node between source and destination
    - Routers and switches use the address in the packet to determine how to forward the packets

- **Advantages**:
    - Packets from different sources are interleaved
    - Efficient use of resources (since they are used on demand)
    - Can accommodate bursty traffic
    - Allows for flexibility and robustness. Packets can travel through alternative paths (adaptive routing)
- **Disadvantages**:
    - Undesired situations such as congestion; long delays may occur

## Packet Details

- Depends on the underlying network:
    - Minimum/maximum size
    - Format
- A hardware packet is called a **frame**

## Internetworking

A **gateway** or **router** is needed to interconnect one or more networks.

Host-to-host connectivity is only possible if there's a **uniform addressing** scheme and a **routing mechanism**.

Messages can be sent to a single destination (**unicase**), to multiple destinations (**multicast**), or to all possible destinations (**broadcast**).

**Routers** determine the next network point on a data unit's path. They are essentially the *sorting offices* for the Internet Protocol.

## LAN/MAN/WAN Networks

Computer networks can also be classified according to their geographical coverage:

- **Local Area Network (LAN)**: Covers a small geographic area, such as a building
- **Metropolitan Area Network (MAN)**: Covers a larger geographic area, such as a town or city
- **Wide Area Network (WAN)**: Covers a very large geographic area, such as the Earth.
