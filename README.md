# deep-in-net

## Purpose of This Document

This README explains **all networking concepts**, **answers every theoretical question**, and documents the **exact steps used to solve each exercise** in Cisco Packet Tracer. It is written to be used during audit preparation.

---

## Core Networking Concepts

### What Is a Network?

A network is a collection of devices connected together to exchange data. Communication happens using rules called **protocols**.

### What Is a Networking Device?

Networking devices control how data moves between endpoints.

* **PC / End Device**: Generates and receives data
* **Hub**: Broadcasts data to all ports
* **Switch**: Sends data only to the correct destination using MAC addresses
* **Router**: Connects different networks using IP addresses
* **Server**: Provides services (DNS, DHCP, HTTP, FTP, etc.)

---

## OSI Model (Essential for Audit)

| Layer | Name         | Role                                  |
| ----- | ------------ | ------------------------------------- |
| 7     | Application  | User-facing services (HTTP, FTP, DNS) |
| 6     | Presentation | Encryption, formatting                |
| 5     | Session      | Session control                       |
| 4     | Transport    | TCP / UDP, ports                      |
| 3     | Network      | IP addressing, routing                |
| 2     | Data Link    | MAC addresses, switching              |
| 1     | Physical     | Cables, bits                          |

---

## Cables and Physical Layer

### What Is an RJ-45 Cable?

An RJ-45 cable is an Ethernet cable used to connect networking devices.

### Straight-Through vs Crossover

* **Straight-through**: PC ↔ Switch, Router ↔ Switch
* **Crossover**: PC ↔ PC, Switch ↔ Switch

(Packet Tracer often auto-selects, but understanding is mandatory.)

---

## Exercise 1 – Basic Connectivity

### Goal

* PC0 communicates with PC1
* PC2 communicates with PC3
* PC4 communicates with PC5

### Steps

1. Place PCs in pairs
2. Connect each pair using the correct cable
3. Assign IP addresses in the same subnet
4. Use `ping` to verify connectivity

### Explanation

Devices in the **same subnet** can communicate without a router.

---

## Exercise 2 – Hub vs Switch

### Hub

* Operates at **OSI Layer 1**
* Broadcasts frames to all ports
* No MAC address learning

### Switch

* Operates at **OSI Layer 2**
* Uses MAC address table
* Sends frames only to the destination port

### Steps

1. Connect PCs to hub → test communication
2. Connect PCs to switch → test communication

---

## Exercise 3 – Servers and Services

### What Is a Server?

A server is a device that provides a specific service to clients.

### DHCP

* Automatically assigns IP addresses
* Operates using UDP
* OSI Layer 7 (Application)

### DNS

* Resolves names to IP addresses
* Example:

  * deep-in-net.local → 192.168.1.99
  * deep-in-net.com → deep-in-net.local

### HTTP vs HTTPS

* **HTTP**: Unencrypted
* **HTTPS**: Encrypted using TLS

### FTP

* File transfer protocol
* Requires user authentication

### Steps

1. Assign static IPs to servers
2. Enable DHCP service
3. Disable HTTP, enable HTTPS
4. Create FTP user `deepinnet`
5. Configure DNS records
6. Test access via browser and FTP

---

## TCP vs UDP

| TCP                 | UDP               |
| ------------------- | ----------------- |
| Reliable            | Unreliable        |
| Connection-based    | Connectionless    |
| Uses acknowledgment | No acknowledgment |

Both operate at **OSI Layer 4**.

---

## Ports

A port identifies a specific service on a device.

| Service | Port    |
| ------- | ------- |
| HTTP    | 80      |
| HTTPS   | 443     |
| FTP     | 21      |
| DNS     | 53      |
| DHCP    | 67 / 68 |

---

## Exercise 4 – Router Basics

### What Is a Router?

A router connects **different networks**.

* Operates at **OSI Layer 3**
* Uses IP addresses

### Default Gateway

The default gateway is the router interface used to reach other networks.

### Steps

1. Place router between two networks
2. Assign IPs to router interfaces
3. Configure PCs with default gateway
4. Test with `ping`

---

## Exercise 5 – Inter-Subnet Communication

### Concept

Devices in different subnets require a **router** to communicate.

### Steps

1. Create two subnets
2. Assign correct IPs and masks
3. Configure router interfaces
4. Verify bidirectional communication

---

## Exercise 6 – Routing Table

### What Is a Routing Table?

A routing table tells the router **where to send packets**.

Each entry contains:

* Destination network
* Next hop
* Interface

### Steps

1. Configure static routes
2. Verify routing table
3. Test communication

---

## Exercise 7 – Multi-Subnet Routing

Same logic as Exercise 5, expanded topology.

Key focus:

* Correct IP addressing
* Correct gateway configuration

---

## Exercise 8 – Full Connectivity

### Goal

All subnets communicate with each other.

### Steps

1. Assign unique subnet ranges
2. Configure router interfaces
3. Ensure correct gateways
4. Test all communication paths

---
## Commands Used

### Basic
- `enable` — enter privileged EXEC mode
- `configure terminal` — enter global configuration mode
- `interface <type><number>` — select interface to configure (e.g., `g0/0`)
- `ip address <ip> <mask>` — assign IP to interface
- `no shutdown` — activate the interface
> Tip: Always check interface status with `show ip interface brief`

### Static Routing
- `ip route <destination-network> <mask> <next-hop-ip>` — define static route
> Tip: Verify with `show ip route`

### Saving Configuration (RAM → NVRAM)
- `copy running-config startup-config`
- `copy run start`
- `write memory`
- `wr`
> Any of the above commands is valid and saves the running configuration to persistent memory.
> Tip: If you forget this, all changes are lost after `reload`.

### Quick Reference
- `show running-config` — view current configuration in RAM
- `show startup-config` — view saved configuration in NVRAM
- `show ip interface brief` — check IP and interface status
- `reload` — reboot device (unsaved changes are lost)

## Dynamic Routing protocols


RIP OSPT EIGRP ... 

## Final Notes

Networking is fundamental for Cloud and DevOps engineering. This project builds the mindset required to design, debug, and reason about real networks.
