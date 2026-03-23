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
- routing (static & dynamic)  
- routing metrics and path selection  

---

## Network Topology

Internet → WAN → OPNsense → LAN (192.168.10.0/24) + LAN2 (192.168.20.0/24)

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

Connectivity between machines verified using ICMP (ping).

### Example tests

Windows → OPNsense  
Windows → Ubuntu  
Ubuntu → Windows Server  
Kali → All machines  
Ubuntu → LAN2  

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

### Windows IPv6
![IPv6 Windows](images/ipv6-ubuntu-test.png)

### Ubuntu IPv6
![IPv6 Ubuntu](images/ipv6-windows-test.png)

---

## Project Structure

hyperv-opnsense-security-lab  
├── README.md  
├── lab-documentation.md  
└── images  

---

## Documentation

Full technical documentation is available in:

lab-documentation.md

Includes:

- installation steps  
- configuration  
- troubleshooting  
- lab notes  

---

## Phase 2 – Network Segmentation (LAN2)

Subnet: 192.168.20.0/24  

Issue: APIPA (169.254.x.x)  
Cause: DHCP not enabled  

Fix:
- enabled DHCP  
- verified interface  
- renewed IP  

Result:
- correct IP  
- connectivity restored  

---

## Phase 3 – IPv6 + NAT

IPv6 network: 2001:db8:1::/64  

Tests:
- ping IPv6 gateway  
- verify dual-stack  

NAT:
- 192.168.10.0/24 → WAN  

Result:
- IPv4 + IPv6 working  
- internet access verified  

---

## Phase 4 – Routing (Static, Metric & OSPF)

### Static Routing

Configured route to LAN2 network.

Result:
- LAN ↔ LAN2 communication works  

Important:
- not required in this topology (directly connected networks)  
- used for learning purposes  

---

### Routing Metric

Configured two routes:

- metric 0 (primary)  
- metric 10 (backup)  

Test:
- removed primary  
- traffic used backup  

Result:
- router selects lowest metric  
- fallback confirmed  

---

### Dynamic Routing (OSPF)

FRR installed and configured via Routing menu.

Observation:
- configuration successful  
- no routing exchange  

Explanation:
- only one router  
- OSPF requires multiple routers  

---

### Issues & Troubleshooting

Firewall:
- LAN2 blocked traffic → fixed with allow rule  

Windows:
- blocked ICMP → fixed with firewall rule  

FRR:
- not visible under Services → found under Routing  

Routing loop:
- TTL exceeded error  
- caused by mixed config  

Fix:
- removed routes and gateway  
- disabled OSPF  
- rebooted OPNsense  

---

## Results

- full LAN connectivity achieved  
- LAN2 segmentation working  
- DHCP issue resolved  
- routing verified  
- routing metric tested  
- OSPF configured and analyzed  
- routing loop resolved  
- NAT working  
- IPv6 implemented  

---

## What I Learned

- Hyper-V networking  
- OPNsense firewall configuration  
- segmentation (LAN vs LAN2)  
- static vs dynamic routing  
- routing metrics  
- OSPF limitations  
- firewall troubleshooting  
- routing loops (TTL exceeded)  
- real-world debugging  

---

## Future Improvements

- multi-router OSPF lab  
- VLAN segmentation  
- IDS/IPS  
- monitoring  

---

## Conclusion

A functional cybersecurity lab demonstrating networking, segmentation, routing and troubleshooting in a realistic environment.

---

## Author

Muhammad Mehdi  
IT Security Developer Student
