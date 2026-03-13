# Hyper-V OPNsense Security Lab

This project demonstrates a virtual network security lab built using **Microsoft Hyper-V** and **OPNsense**.
The lab simulates a small network environment with multiple operating systems connected through a firewall.

The purpose of this lab is to practice **virtualization, networking, and basic security infrastructure**.

---

# Lab Architecture

Internet
│
WAN-Switch
│
OPNsense Firewall
│
LAN-Switch
│
├── Windows 11 Client
├── Windows Server 2025
├── Ubuntu Server
└── Kali Linux

---

# Technologies Used

* Microsoft Hyper-V
* OPNsense Firewall
* Windows 11
* Windows Server 2025
* Ubuntu Server
* Kali Linux
* Virtual Networking
* DHCP
* Routing
* Network troubleshooting

---

# Virtual Machines

### OPNsense

Role: Firewall / Router
LAN IP: `192.168.10.1`
DHCP Range: `192.168.10.100 – 192.168.10.200`

### Windows 11

Role: Client machine
Network: DHCP

### Windows Server 2025

Role: Server environment
Network: DHCP

### Ubuntu Server

Role: Linux server
SSH enabled

### Kali Linux

Role: Security testing machine

---

# Lab Network Configuration

Network: `192.168.10.0/24`

| Machine             | Role              | IP Address     |
| ------------------- | ----------------- | -------------- |
| OPNsense            | Firewall / Router | 192.168.10.1   |
| Windows 11          | Client            | 192.168.10.144 |
| Windows Server 2025 | Server            | 192.168.10.131 |
| Ubuntu Server       | Linux Server      | 192.168.10.132 |
| Kali Linux          | Security Testing  | 192.168.10.138 |

Gateway: `192.168.10.1`
DHCP Server: `OPNsense`

---

# Network Verification

Connectivity between all machines was verified using:

```
ipconfig
ip addr
ping
```

Example tests:

```
ping 192.168.10.1
ping 192.168.10.132
ping 8.8.8.8
```

Results:

* All virtual machines received IP addresses from the OPNsense DHCP server.
* All machines could communicate with each other.
* Internet connectivity worked through OPNsense.

---

# Project Goals

* Build a virtual enterprise-like network
* Practice firewall configuration
* Work with Windows and Linux systems
* Test internal network communication
* Verify connectivity between multiple operating systems

---

# Repository Structure

```
hyperv-opnsense-security-lab
│
├── README.md
├── docs
│   └── lab-documentation.md
│
├── diagrams
│   └── network-topology.png
│
└── screenshots
    ├── hyperv-switches.png
    ├── opnsense-dashboard.png
    ├── vm-list.png
    └── ping-test.png
```

---


## Screenshots

### Hyper-V Virtual Switches
![Hyper-V Switches](hyperv-switches.png)

### Virtual Machines
![VM List](vm-list.png)

### OPNsense Dashboard
![OPNsense Dashboard](opnsense-dashboard.png)

### OPNsense Interfaces
![OPNsense Interfaces](opnsense-interfaces.png)

### Network Connectivity Test
![Ping Test](ping-test.png)

### IP Configuration
![IP Config](ip-config.png)

---
Examples of screenshots to include:

* Hyper-V virtual switches
* OPNsense dashboard
* Virtual machines list
* Ping connectivity tests

---

# Author

Muhammad Mehdi
IT Security Developer Student
