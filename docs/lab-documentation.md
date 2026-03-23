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
- configure and analyze routing behavior

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

ping <target-ip>

### Validation

- system-to-system communication confirmed
- routing path verified
- expected responses received

---

## Phase 2 – Network Segmentation (LAN2)

A second subnet was introduced to simulate segmentation.

### Subnet

192.168.20.0/24

### Implementation

- added LAN2 interface in OPNsense
- connected Win11-LAN2 to LAN2 network

---

## Issue – DHCP Failure

The LAN2 client received an APIPA address:

169.254.x.x

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

## Phase 3 – IPv6 Implementation

IPv6 was introduced without modifying the existing IPv4 setup.

### Configuration

OPNsense LAN interface:

2001:db8:1::1/64

Clients:

- Windows → 2001:db8:1::10
- Ubuntu → 2001:db8:1::20

Gateway:

2001:db8:1::1

---

## IPv6 Testing

### Commands

ping 2001:db8:1::1  
ping6 2001:db8:1::1  

### Result

- successful communication with firewall
- IPv6 routing verified within LAN

---

## NAT Configuration (IPv4)

Outbound NAT configured in OPNsense (Hybrid mode).

### Rule

192.168.10.0/24 → WAN

---

## Internet Connectivity

### Test

ping 8.8.8.8

### Result

- NAT functioning correctly
- internet access confirmed

---

## Phase 4 – Routing (Static, Metric & OSPF)

This phase focused on understanding how routing works between segmented networks and how routing decisions are made.

### Network Context

- LAN → 192.168.10.0/24
- LAN2 → 192.168.20.0/24

Ubuntu Server placed on LAN and Windows client on LAN2.

---

### Static Routing

A static route was configured in OPNsense.

Configuration:

- Destination network: 192.168.20.0/24
- Gateway: 192.168.20.1

### Result

- successful communication between LAN and LAN2
- traffic correctly routed through OPNsense

### Observation

Since both networks are directly connected to OPNsense, static routing is not strictly required. This step was performed for learning purposes.

---

### Routing Metric

Two routes were configured to simulate path selection.

Configuration:

- primary route → metric 0
- secondary route → metric 10

### Testing

- primary route removed
- connectivity tested again

### Result

- traffic automatically used secondary route
- confirmed that lower metric is preferred

---

### Dynamic Routing (OSPF)

FRR plugin installed and OSPF configured.

Configuration steps:

- enabled FRR under Routing menu
- enabled OSPF
- added LAN interface
- added LAN2 interface
- defined OSPF networks

### Observation

- OSPF configured successfully
- no routing exchange occurred

### Explanation

- only one router exists in the lab
- OSPF requires multiple routers to exchange routes
- therefore, no dynamic routing behavior was observed

---

### Troubleshooting (Routing Phase)

#### Firewall Issue

- LAN2 had no default allow rule
- traffic between LAN and LAN2 blocked

Fix:
- added allow rule on LAN2 interface

---

#### Windows ICMP Blocking

Issue:
- ping failed from Ubuntu to Windows

Cause:
- Windows firewall blocked ICMP

Fix:
- enabled ICMP rule in Windows firewall

Result:
- bidirectional communication restored

---

#### FRR Visibility Issue

Issue:
- FRR plugin not visible under Services

Cause:
- newer OPNsense versions use Routing menu

Fix:
- accessed FRR via Routing → General / OSPF

---

#### Routing Loop (TTL Exceeded)

Issue:
- ping returned TTL exceeded

Cause:
- conflict between static routes, custom gateway, and OSPF

Fix:

- removed static routes
- removed custom gateway
- disabled OSPF
- rebooted OPNsense

Result:

- routing table reset
- normal connectivity restored

---

## Technical Observations

- segmentation requires correct DHCP configuration per interface  
- APIPA indicates DHCP failure  
- IPv6 can be introduced without disrupting IPv4  
- NAT is essential for IPv4 internet access  
- Hyper-V networking must align with firewall interfaces  
- static routing is unnecessary for directly connected networks  
- routing metrics determine path preference  
- dynamic routing protocols require multiple routers  
- incorrect routing configuration can cause loops  
- system reboot may be required to clear routing state  
