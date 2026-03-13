# Hyper-V OPNsense Security Lab

This project demonstrates a virtual network security lab built using **Microsoft Hyper-V** and **OPNsense Firewall**.

The lab simulates a small internal network environment where multiple operating systems communicate through a firewall. The goal is to practice virtualization, networking, and basic security infrastructure.

---

# Lab Architecture

Internet  
│  
WAN Switch  
│  
OPNsense Firewall  
│  
LAN Switch  
├── Windows 11 Client  
├── Windows Server 2025  
├── Ubuntu Server  
└── Kali Linux  

---

# Network Topology

```
Internet
   |
WAN Switch
   |
OPNsense Firewall
   |
LAN Switch
   |--- Windows 11 Client
   |--- Windows Server 2025
   |--- Ubuntu Server
   |--- Kali Linux
```

---

# Project Goals

- Practice virtualization using Hyper-V
- Configure and manage a firewall using OPNsense
- Implement DHCP for internal network
- Test connectivity between multiple operating systems
- Practice network troubleshooting and verification

---

# Technologies Used

- Microsoft Hyper-V
- OPNsense Firewall
- Windows 11
- Windows Server 2025
- Ubuntu Server
- Kali Linux
- Virtual Networking
- DHCP
- Routing
- Network troubleshooting

---

# Virtual Machines

| Machine | Role |
|------|------|
| OPNsense | Firewall / Router |
| Windows Server 2025 | Internal server |
| Windows 11 | Client machine |
| Ubuntu Server | Linux server |
| Kali Linux | Security testing |

---

# Network Configuration

| Machine | IP Address |
|------|------|
| OPNsense LAN | 192.168.10.1 |
| Windows Server | 192.168.10.131 |
| Ubuntu Server | 192.168.10.132 |
| Kali Linux | 192.168.10.138 |
| Windows 11 | 192.168.10.144 |

All virtual machines received their IP addresses from the **OPNsense DHCP server**.

---

# Verification

Connectivity between machines was verified using:

- IP configuration checks
- Ping tests between machines
- Internet access verification through the OPNsense firewall

---

# Commands Used

### Windows

```
ipconfig
ping 192.168.10.1
```

### Linux (Ubuntu / Kali)

```
ip addr
ping 192.168.10.1
ping 8.8.8.8
```

---

# Screenshots

### Hyper-V Virtual Switches
![Hyper-V Switches](hyperv-switches.png)

### Virtual Machines (Hyper-V Manager)
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

# Documentation

Additional technical notes can be found in:

docs/lab-documentation.md

---

# Results

- All virtual machines received IP addresses from the OPNsense DHCP server
- All machines were able to communicate with each other
- Internet connectivity worked correctly through the firewall

---

# Conclusion

This lab demonstrates how a virtual network environment can be built using Hyper-V and secured with OPNsense.

The setup provides a foundation for practicing networking, firewall configuration, and security testing using both Windows and Linux systems.

---

# Author

Muhammad Mehdi  
IT Security Developer Student  
EC Utbildning
