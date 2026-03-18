# Hyper-V OPNsense Security Lab

A personal **cybersecurity home lab** built using **Microsoft Hyper-V** and **OPNsense firewall** to simulate a realistic internal network environment.

This project demonstrates how to design and deploy a small virtual enterprise network including firewall routing, multiple operating systems, segmentation, and connectivity verification.

The lab serves as a **hands-on learning platform** for networking, system administration, and cybersecurity experimentation.

---

## Lab Overview

This lab simulates a **small enterprise-style network** using virtualization.

### Components

- Hyper-V virtualization
- OPNsense firewall/router
- Windows and Linux systems
- Kali Linux attacker machine
- Segmented networks (LAN & LAN2)

### What this lab demonstrates

- network topology design  
- firewall configuration  
- network segmentation  
- system administration  
- troubleshooting real-world issues  
- basic security testing  

---

## Network Topology

```
                         Internet
                            │
                            ▼
                        WAN Network
                            │
                            ▼
                   ┌─────────────────┐
                   │   OPNsense FW   │
                   │ (Router/Gateway)│
                   └───────┬─────────┘
                           │
        ┌──────────────────┴──────────────────┐
        │                                     │
        ▼                                     ▼
   LAN (192.168.10.0/24)              LAN2 (192.168.20.0/24)
        │                                     │
 ┌──────┼──────────┬──────────┬───────┐        │
 │      │          │          │       │        ▼
 ▼      ▼          ▼          ▼       ▼   Win11-LAN2
Win11  WinServer  Ubuntu     Kali   (Attacker)
Client   Server   Server     Linux
```

---

## Virtual Machines

| Machine        | Role                | OS              | Network | IP Address |
|----------------|---------------------|------------------|--------|------------|
| OPNsense       | Firewall / Router   | OPNsense         | WAN/LAN/LAN2 | 192.168.10.1 |
| Windows 11     | Client workstation  | Windows 11       | LAN    | 192.168.10.144 |
| Windows Server | Server environment  | Windows Server   | LAN    | 192.168.10.131 |
| Ubuntu Server  | Linux server        | Ubuntu Server    | LAN    | 192.168.10.132 |
| Kali Linux     | Security testing    | Kali Linux       | LAN    | 192.168.10.138 |
| Win11-LAN2     | Segmented client    | Windows 11       | LAN2   | DHCP (192.168.20.x) |

---

## Network Configuration

| Component        | Description |
|-----------------|------------|
| WAN             | External internet connection |
| LAN             | Primary internal network |
| LAN2            | Segmented internal network |
| Firewall        | OPNsense controls traffic |
| Virtual Switch  | Hyper-V networking |

---

## Connectivity Verification

Connectivity between machines verified using **ICMP (ping)**.

### Example tests

```
Windows11 → OPNsense
Windows11 → Ubuntu
Ubuntu → Windows Server
Kali → All machines
```

### Verified results

- routing works correctly  
- internal communication works  
- firewall allows expected traffic  
- all systems reachable  

---

## Screenshots

### Hyper-V Virtual Switches
![Hyper-V Switches](images/hyperv-switches.png)

### Virtual Machines
![VM List](images/vm-list.png)

### OPNsense Dashboard
![OPNsense Dashboard](images/opnsense-dashboard.png)

### OPNsense Interfaces
![OPNsense Interfaces](images/opnsense-interfaces.png)

### Ping Test
![Ping Test](images/ping-test.png)

### IP Configuration
![IP Config](images/ip-config.png)

---

### LAN2 – DHCP Issue

### APIPA Problem
![APIPA](images/lan2-apipa.png)

### OPNsense LAN2 Interface
![LAN2 Interface](images/lan2-interface.png)

### DHCP Fix
![DHCP Fix](images/lan2-dhcp-fixed.png)

### Connectivity Restored
![LAN2 Result](images/lan2-connectivity.png)

---

### IPv6 Configuration

### OPNsense IPv6
![IPv6 OPNsense](images/ipv6-opnsense.png)

### Ubuntu IPv6
![IPv6 Ubuntu](images/ipv6-ubuntu-test.png)

### Windows IPv6
![IPv6 Windows](images/ipv6-windows-test.png)

---

## Project Structure

```
hyperv-opnsense-security-lab
│
├── README.md
├── lab-documentation.md
│
└── images
    ├── hyperv-switches.png
    ├── vm-list.png
    ├── opnsense-dashboard.png
    ├── opnsense-interfaces.png
    ├── ping-test.png
    ├── ip-config.png
    ├── lan2-apipa.png
    ├── lan2-interface.png
    ├── lan2-dhcp-fixed.png
    ├── lan2-connectivity.png
    ├── ipv6-opnsense.png
    ├── ipv6-ubuntu-test.png
    └── ipv6-windows-test.png
```

---

## Documentation

Full technical documentation is available in:

```
lab-documentation.md
```

Includes:

- installation steps  
- configuration  
- troubleshooting  
- lab notes  

---

## Results

- full LAN connectivity achieved  
- LAN2 segmentation working  
- DHCP issue resolved  
- NAT working correctly  
- IPv6 successfully implemented  

---

## Key Skills Demonstrated

| Area              | Skills |
|------------------|--------|
| Virtualization   | Hyper-V, VM setup |
| Networking       | IP addressing, subnetting |
| Security         | Firewall (OPNsense) |
| Systems          | Windows, Linux, Kali |
| Troubleshooting  | DHCP, connectivity |
| Advanced         | IPv6, NAT, segmentation |

---

## Future Lab Extensions

- Active Directory  
- VLAN segmentation  
- IDS/IPS (Snort / Suricata)  
- monitoring & logging  
- attack simulations  

---

## Phase 2 – Network Segmentation (LAN2)

New subnet:

```
192.168.20.0/24
```

### Issue

Client received APIPA (169.254.x.x)

### Cause

DHCP not enabled on LAN2

### Fix

- enabled DHCP  
- verified interface  
- renewed IP  

### Result

- correct IP assigned  
- connectivity restored  

---

## Phase 3 – IPv6 + NAT

### IPv6 Setup

```
2001:db8:1::1/64
```

Clients:

- Windows → 2001:db8:1::10  
- Ubuntu → 2001:db8:1::20  

Gateway:

```
2001:db8:1::1
```

---

### IPv6 Test

```
ping 2001:db8:1::1
ping6 2001:db8:1::1
```

---

### NAT (IPv4)

```
192.168.10.0/24 → WAN
```

---

### Internet Test

```
ping 8.8.8.8
```

---

### Before vs After

| Stage  | IPv4 | IPv6 | NAT | Internet |
|--------|------|------|-----|----------|
| Before | ✔ | ❌ | ✔ | ✔ |
| After  | ✔ | ✔ | ✔ | ✔ |

---

## Conclusion

A fully functional cybersecurity lab built using virtualization and OPNsense.

Supports:

- network design  
- segmentation  
- troubleshooting  
- security testing  

---

## Author

**Muhammad Mehdi**  
IT Security Developer Student
