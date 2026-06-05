# Cisco Packet Tracer: OSPF & Extended Access Control List (ACL) Configuration

## 📌 Overview
This repository contains a Cisco Packet Tracer simulation demonstrating the implementation of **Single-Area OSPF (Open Shortest Path First)** routing alongside an **Extended Access Control List (ACL)**. The objective of this lab is to establish dynamic routing across multiple subnets while strictly controlling HTTP traffic flows for security.

## 🏗️ Network Topology
The network architecture comprises the following infrastructure:
* **End Devices:** `PC0`, `Server0`, `Server1`
* **Switching:** 2x Cisco 2960-24TT Switches (`Switch0`, `Switch1`)
* **Routing:** 2x Cisco ISR4331 Routers (`Router0`, `Router1`)

**Traffic Flow:** `PC0` -> `Switch0` -> `Router0` -> `Router1` -> `Switch1` -> `Servers`

[Network Topology](screenshots/router1-acl-config.png) 

## 🖧 IP Addressing Scheme

| Device | Interface | IP Address | Subnet Mask | Network / Zone |
| :--- | :--- | :--- | :--- | :--- |
| **Router0** | `GigE 0/0/1` | 192.168.1.1 | 255.255.255.0 | Local LAN (Client) |
| **Router0** | `GigE 0/0/0` | 10.0.0.1 | 255.255.255.0 | P2P Transit Link |
| **Router1** | `GigE 0/0/0` | 10.0.0.2 | 255.255.255.0 | P2P Transit Link |
| **Router1** | `GigE 0/0/1` | 172.16.0.1 | 255.255.255.0 | Server LAN |

## ⚙️ Configuration Highlights

### 1. Dynamic Routing (Single-Area OSPF)
OSPF Process ID `1` in Area `0` is configured on both routers to dynamically exchange routes between the `192.168.1.0/24` and `172.16.0.0/24` networks.

**Router0 OSPF Block:**
```text
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.255 area 0