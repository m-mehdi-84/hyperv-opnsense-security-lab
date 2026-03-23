# Lab Documentation – Hyper-V OPNsense Security Lab

## Overview

This document provides the **technical implementation details** of the Hyper-V OPNsense Security Lab.

The README presents a high-level overview, while this document focuses on:

- configuration steps  
- troubleshooting  
- technical validation  
- implementation details  

---

## Lab Objective

The objective of this lab was to build a functional virtual network simulating a small enterprise environment.

Key goals:

- deploy an internal network using virtualization  
- configure OPNsense as firewall and gateway  
- verify connectivity between systems  
- implement network segmentation (LAN2)  
- troubleshoot DHCP issues  
- introduce IPv6 alongside IPv4  
- validate NAT and internet access  

---

## Environment Setup

### Virtualization Platform

- Microsoft Hyper-V used for all virtual machines  
- virtual switches created for WAN, LAN and LAN2  

### Firewall Configuration

OPNsense configured as:

- router  
- firewall  
- default gateway  

### Networks

- LAN → 192.168.10.0/24  
- LAN2 → 192.168.20.0/24  

---

## Phase 1 – Initial Deployment

The lab started with a single internal network (LAN).

### Implementation Steps

- created virtual machines (Windows, Linux-based systems)  
- connected systems to LAN virtual switch  
- configured IPv4 addressing via DHCP  
- set OPNsense as default gateway  

### Result

- internal communication successfully established  
- all traffic routed through OPNsense  
- basic network functionality validated  

---

## Connectivity Verification

Connectivity testing was performed using ICMP.

### Commands

```
ping <target-ip>
```

### Validation

- system-to-system communication confirmed  
- gateway reachability verified  
- expected ICMP replies received  

---

## Phase 2 – Network Segmentation (LAN2)

A second subnet was introduced to simulate network segmentation.

### Subnet

192.168.20.0/24  

### Implementation

- added LAN2 interface in OPNsense  
- assigned interface IP: 192.168.20.1  
- connected Windows 11 client to LAN2 network  

---

## Issue – DHCP Failure (LAN2)

The LAN2 client received an APIPA address:

```
169.254.x.x
```

### Analysis

This indicates failure to obtain an IP address from DHCP.

### Root Cause

- DHCP service was not enabled on the LAN2 interface  

---

## Troubleshooting Process (LAN2 DHCP)

Steps performed:

- verified LAN2 interface assignment in OPNsense  
- checked DHCP configuration settings  
- confirmed correct virtual switch mapping in Hyper-V  
- renewed client IP configuration  

### Resolution

- enabled DHCP service on LAN2  
- verified subnet configuration (192.168.20.0/24)  

### Commands (Windows)

```
ipconfig /release
ipconfig /renew
```

### Result

- client received valid IP (192.168.20.x)  
- connectivity restored  
- segmentation functioning correctly  

---

## Phase 3 – IPv6 Implementation

IPv6 was introduced without modifying the existing IPv4 configuration.

### Configuration

OPNsense LAN interface:

```
2001:db8:1::1/64
```

Clients:

- Windows → 2001:db8:1::10  
- Ubuntu → 2001:db8:1::20  

Default gateway:

```
2001:db8:1::1
```

---

## IPv6 Testing

### Commands

```
ping 2001:db8:1::1
ping6 2001:db8:1::1
```

### Result

- successful communication with firewall  
- IPv6 routing verified within LAN  
- dual-stack functionality confirmed  

---

## NAT Configuration (IPv4)

Outbound NAT configured in OPNsense using Hybrid mode.

### Rule

```
Source: 192.168.10.0/24 → WAN
```

---

## Internet Connectivity Validation

### Test

```
ping 8.8.8.8
```

### Result

- NAT functioning correctly  
- outbound internet access confirmed  

---

## Additional Troubleshooting & Issues Encountered

### 1. Windows Firewall Blocking ICMP

#### Issue

- ping from Ubuntu Server to Windows failed  

#### Cause

- Windows Firewall blocks ICMP by default  

#### Resolution (PowerShell)

```
Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"
```

#### Result

- ICMP allowed  
- bidirectional communication restored  

---

### 2. Ubuntu IPv6 – "Network is unreachable"

#### Issue

```
ping6: connect: network is unreachable
```

#### Cause

- missing or incorrect IPv6 configuration / routing  

#### Resolution

- verified IPv6 address assignment  
- verified default gateway configuration  
- ensured correct subnet (2001:db8:1::/64)  

#### Result

- IPv6 communication successfully established  

---

### 3. Windows Ping Error – "General failure"

#### Issue

```
Transmit failed. General failure.
```

#### Cause

- network misconfiguration or interface issue  

#### Resolution

- renewed DHCP lease  
- verified network adapter settings  
- ensured correct virtual switch connection  

#### Commands

```
ipconfig /release
ipconfig /renew
```

#### Result

- network stack restored  
- connectivity working again  

---

### 4. Hyper-V Network Misconfiguration

#### Issue

- VM connected to incorrect virtual switch  

#### Cause

- mismatch between Hyper-V switch and intended network (LAN/LAN2)  

#### Resolution

- reassigned VM to correct virtual switch  

#### Result

- correct network segmentation restored  
- DHCP and connectivity functioning properly  

---

## Technical Observations

- network segmentation requires DHCP per interface  
- APIPA (169.254.x.x) indicates DHCP failure  
- IPv6 can be implemented alongside IPv4 without disruption  
- NAT is required for IPv4 internet access  
- Hyper-V switch configuration must match firewall interfaces  
- firewall rules can impact connectivity (ICMP blocking)  
- structured troubleshooting improves efficiency  
- validating each layer (IP, gateway, routing) is critical  

---

## Conclusion

The lab successfully demonstrates how to design, configure and troubleshoot a segmented virtual network using OPNsense and Hyper-V.

It provides a strong foundation in:

- network architecture  
- firewall configuration  
- segmentation  
- troubleshooting methodology  
- dual-stack networking  

This environment serves as a base for more advanced networking and cybersecurity labs in separate repositories.

---
