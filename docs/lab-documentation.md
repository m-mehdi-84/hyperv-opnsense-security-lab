# Lab Documentation

## Overview

This document provides additional technical notes for the **Hyper-V OPNsense Security Lab**.

The purpose of this lab is to simulate a small internal network protected by a firewall and practice virtualization, networking, and security fundamentals.

---

## Environment

Virtualization Platform
Microsoft Hyper-V

Firewall
OPNsense

Internal Network
192.168.10.0/24

---

## Virtual Machines

**Windows 11**
Client machine used for testing connectivity.

**Windows Server 2025**
Used to simulate a server environment.

**Ubuntu Server**
Linux server with SSH enabled.

**Kali Linux**
Used for security testing and security tools.

---

## Network Verification

The following tests were performed to verify the network:

* IP configuration checks
* Connectivity tests between machines
* Internet access verification through OPNsense firewall

---

## Commands Used

### Windows

```
ipconfig
ping 192.168.10.1
```

### Linux

```
ip addr
ping 8.8.8.8
```

---

## Results

* All virtual machines received IP addresses from the OPNsense DHCP server.
* All machines were able to communicate with each other.
* Internet connectivity worked correctly through the firewall.

---

## Conclusion

This lab demonstrates how a virtual network environment can be built using Hyper-V and secured with OPNsense.

The setup provides a foundation for practicing networking, firewall configuration, and security testing using both Windows and Linux systems.
