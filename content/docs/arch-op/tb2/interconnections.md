---
title: "4. Interconnections"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 4. Interconnections

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/arch-op/y1/tb2/4-interconnections)

- A computer is a network of basic modules
- There needs to be parts for connecting the modules
- The structure of these depends on the exchanges

**Memory**:

- N words equal length
- Unique numerical address
- Read/write data word
- Operating is indicatred by read and write control signals
- The location for the operation is specified by an address

![Interconnection Structure: Memory](/img/arch-op/y1/interconnections-memory.png)

**I/O Module**:

- Similar to Memory (internal point of view): read/write
- Control more than one external device (port - unique address)
- External data path (input/output) with an external device
- Interrupt signals

![Interconnection Structure: I/O Module](/img/arch-op/y1/interconnections-io-module.png)

**Processor**:

- Reading instruction and data
- Write out data after processing
- Use control signals to control the overall operations
- Receive interrupt signals

![Interconnection Structure: Processor](/img/arch-op/y1/interconnections-processor.png)

## Types of Transfers

- **Memory to Procesor**: The processor reads an instruction or a unit of data from memory
- **Processor to Memory**: The processor writes a unit of data to memory
- **I/O to Processor**: The processor reads data from an I/O device via an I/O module
- **Processor to I/O**: The processor sends data to the I/O device
- **I/O to or from Memory**: I/O module is allowed to exchange data directly with memory, without going through the processor, using direct memory access

## Types of Interconnections

### Bus

- Communication pathway connecting two or more devices
- Key characteristics: shared transmission medium
- Multiple devices connect to the bus, and a signal transmitted by any one device can be received by all other devices attached to the bus
- Signal overlap and become garble - only one device at a time can successfully transmit
- A bus consists of multiple communication pathways, lines - each transmit signals representing binary 0 or 1 (e.g. 8-bit unit transmits over 8 bus lines)
- Example: System Bus

#### Bus Functional Groups

![Bus Functional Groups](/img/arch-op/y1/bus-lines.png)

- **Data Lines**:
    - Moving data
    - Data bus
    - Bus Width - Number of lines
    - Data bus width - Key factor in determining overall system performance
- **Address Lines**:
    - Source/destination of the data on data bus - Address Bus
    - Bus width - Determines the maximum possible memory capacity
    - Address I/O ports
    - Higher order bits - select module
    - Lower order bits - memory location or I/O port
- **Control Lines**:
    - Controls the access and the use of the data and the address bus
    - **Control signals**:
        - **Command signals**: Specifies the operation to be performed
        - **Timing signals**: Validity of data and address information

#### Bus Operation

If one module wants to send data to another module, it must:

- Obtain the use of the bus
- Transfer the data via the bus

If one module wants to request data from another module, it must:

- Obtain the use of the bus
- Transfer a request to the other module over the appropriate control and address lines

### Point-to-Point Interconnection

- Contemporary systems increasingly rely on Point-to-Point interconnection
- Bus system problem
- Lower latency, higher data rate, better scalability
- QuickPath Interconnect (QPI - 2008):
    - Multiple Direct Connections
    - Layered Protocol Architecture
    - Packetised Data Transfer

![Point-to-Point Interconnection](/img/arch-op/y1/point-to-point-interconnection.png)
