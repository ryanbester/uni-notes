---
title: "1.7. Port Scanning 2 & Packet Capturing"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.7. Port Scanning 2 & Packet Capturing

## OSI Model and Internet Model

The **OSI model** shows the order of encapsulation of network packets.

<table>
    <thead>
        <tr>
            <th>ISO/OSI Model</th>
            <th>Internet Model</th>
            <th>Example Protocols</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Application</td>
            <td rowspan="3">Application</td>
            <td>HTTP, FTP, SSH</td>
        </tr>
        <tr>
            <td>Presentation</td>
            <td>ASCII, MIME, ASN.1</td>
        </tr>
        <tr>
            <td>Session</td>
            <td>SOCKS, NetBIOS</td>
        </tr>
        <tr>
            <td>Transport</td>
            <td>Transport</td>
            <td>TDP, UDP</td>
        </tr>
        <tr>
            <td>Network</td>
            <td>Internet</td>
            <td>IP, ICMP, IPsec</td>
        </tr>
        <tr>
            <td>Data Link</td>
            <td rowspan="2">Network</td>
            <td>Ethernet, IEEE 802.11, ATM</td>
        </tr>
        <tr>
            <td>Physical</td>
            <td>Ethernet, Bluetooth, USB, RS-232</td>
        </tr>
    </tbody>
</table>

## TCP Handshake Flags

| Flag | Description |
|:----:|:------------|
| SYN | Only the first packet sent from each side should have this flag. Used to tell the other side what sequence number to expect. |
| ACK | Used to acknowledge packets which are successfully received. All packets after first SYN should have this set. |
| FIN | Requests connection termination |
| RST | Terminates the connection | 
| URG | Notifies the receiver to process the urgent packets before other packets |
| PSH | Tells the receiver to process packets as they are received instead of buffering them |

## TCP Scanning Methods

### Stealth/SYN Scan

Attempts to hide the scans from the firewall and logs by not fully completing the TCP 3-way handshake.

Example: `nmap -sS [host]`, sends a SYN to each port.

| Response from host | State |
|:------------------:|:------|
| TCP SYN/ACK | Open |
| TCP RST | Closed |
| No response | Filtered |
| ICMP unreachable error | Filtered |

### Full TCP Scan

Tries to negotiate a full 3-way handshake. If the connection is established, the service is alive and the port is open.

Example: `nmap -sT [host]`.

### FIN, NULL, Xmas Scan

FIN Scan: `nmap -sF [host]`
NULL Scan: `nmap -sN [host]`
Xmas scan: `nmap -sX [host]`

| Response from host | State |
|:------------------:|:------|
| No response | Open/Filtered |
| TCP RST | Closed |
| ICMP unreachable error | Filtered |

## UDP Scanning

UDP has no concept of handshaking, so scanning is more difficult.

Example: `nmap -sU [host]` tries sending some data to each UDP port.

| Response from host | State |
|:------------------:|:------|
| Any UDP response | Open |
| No response received | Open/Filtered |
| ICMP port unreachable error | Closed |
| Other ICMP unreachable error | Filtered |

## Packet Capturing

**Packet capturing** or **sniffing** is where traffic is intercepted and logged.

A **packet sniffer** is a piece of software or hardware used to intercept and log traffic that passes through a network.

This can be used to:

- Detect network intrustion attempts
- Identify suspect content in network traffic
- Spy on users and collect sensitive information

### Wireshark

Wireshark is a free and open-source network packet analysis program.

Wireshark shows packets that it captures in real-time.

#### Analysing Data Packets

- The top pane shows the list of packets that have been captured
- The bottom-left pane shows the readable information about the packet
- The bottom-right pane shows the hex data of the packet

#### Capture Filters

Wireshark supports filters to limit the packets that are captured.

- `host [IP address]`: Limits the packets to traffic to and from the IP address
- `net 192.168.0.0/24`: Captures all traffic on the subnet
- `dst host [IP address]`: Captures only packets sent to the IP address
- `port 80`: Captures packets on port 80 only
- `port not 53 and not arp`: Captures all packets except DNS and ARP traffic

#### Display Filters

Wireshark also supports filters to limit the captured packets that are shown.

- `ip.src==[IP address 1] or ip.dst==[IP address 2]`: Shows packets from one computer to another
- `tcp.port eq 22`: Shows all traffic on port 22
- `icmp`: Shows only ICMP packets
- `ip.addr!=[IP address]`: Shows all traffic except from the specified IP address
