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
- virtual switches created for WAN, LAN, and LAN2

### Firewall Configuration

- OPNsense configured as:
  - router
  - firewall
  - default gateway

### Networks

- LAN → 192.168.10.0/24
- LAN2 → 192.168.20.0/24

---

## Initial Deployment

The lab started with a single internal network (LAN).

### Steps

- created virtual machines
- connected systems to LAN
- configured IPv4 addressing
- set OPNsense as default gateway

### Result

- internal communication established
- routing verified through OPNsense

---

## Connectivity Verification

Connectivity testing was performed using ICMP.

### Command

```bash
ping <target-ip>
```

### Validation

- system-to-system communication confirmed
- routing path verified
- expected responses received

---

## Phase 2 – Network Segmentation (LAN2)

A second subnet was introduced to simulate segmentation.

### Subnet

```text
192.168.20.0/24
```

### Implementation

- added LAN2 interface in OPNsense
- connected Win11-LAN2 to LAN2 network

---

## Issue – DHCP Failure

The LAN2 client received an APIPA address:

```text
169.254.x.x
```

### Analysis

This indicated failure to obtain an IP address from DHCP.

### Root Cause

- DHCP service not active on LAN2 interface

---

## Troubleshooting

Steps performed:

- verified LAN2 interface assignment
- checked DHCP configuration in OPNsense
- confirmed correct network attachment in Hyper-V
- renewed client IP configuration

### Resolution

- enabled DHCP on LAN2
- validated subnet settings
- renewed DHCP lease

### Result

- valid IP assigned (192.168.20.x)
- connectivity restored

---

## Purpose of Network Segmentation

The LAN2 network was created to simulate internal network segmentation. This allows separation of systems into different subnets, which improves security and control over network traffic.

Segmentation is commonly used in real environments to isolate sensitive systems and reduce the impact of potential attacks.

---

## Issues Encountered

### IPv6 connectivity issue on Ubuntu

Error:
ping6: connect: Network is unreachable

### Solution

- Verified network configuration
- Checked routing settings
- Adjusted configuration
- Retested connectivity successfully

---

## Lessons Learned

- Importance of correct routing configuration
- Differences between IPv4 and IPv6 behavior
- How segmentation affects communication between networks
- Practical troubleshooting in a virtual lab environment

---

## Phase 3 – IPv6 Implementation

IPv6 was introduced without modifying the existing IPv4 setup.

### Configuration

OPNsense LAN interface:

```text
2001:db8:1::1/64
```

Clients:

- Windows → 2001:db8:1::10
- Ubuntu → 2001:db8:1::20

Gateway:

```text
2001:db8:1::1
```

---

## IPv6 Testing

### Commands

```bash
ping 2001:db8:1::1
ping6 2001:db8:1::1
```

### Result

- successful communication with firewall
- IPv6 routing verified within LAN

---

## NAT Configuration (IPv4)

Outbound NAT configured in OPNsense (Hybrid mode).

### Rule

```text
192.168.10.0/24 → WAN
```

---

## Internet Connectivity

### Test

```bash
ping 8.8.8.8
```

### Result

- NAT functioning correctly
- internet access confirmed

---

## Technical Observations

- segmentation requires correct DHCP configuration per interface  
- APIPA indicates DHCP failure  
- IPv6 can be introduced without disrupting IPv4  
- NAT is essential for IPv4 internet access  
- Hyper-V networking must align with firewall interfaces  

---
