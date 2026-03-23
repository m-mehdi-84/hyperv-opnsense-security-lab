# Hyper-V OPNsense Security Lab

A hands-on **cybersecurity home lab** built using **Microsoft Hyper-V** and **OPNsense firewall** to simulate a realistic small enterprise network.

This project demonstrates practical skills in **network design, segmentation, firewall configuration, troubleshooting and dual-stack (IPv4/IPv6) networking**.

The lab is developed as a **portfolio project** to showcase real-world networking and cybersecurity capabilities.

---

## Lab Overview

This lab simulates a **segmented internal network environment** using virtualization.

Key components:

- Hyper-V virtualization platform
- OPNsense firewall acting as router and gateway
- Multiple virtual machines (Windows & Linux-based systems)
- Network segmentation using multiple subnets (LAN & LAN2)

---

## Network Topology

```
                         INTERNET
                             |
                            WAN
                             |
                    +------------------+
                    |     OPNsense     |
                    |  Firewall/Router |
                    +--------+---------+
                             |
               -----------------------------
               |                           |
      +------------------+       +------------------+
      |       LAN        |       |       LAN2       |
      | 192.168.10.0/24 |       | 192.168.20.0/24 |
      +--------+---------+       +--------+---------+
               |                           |
     --------------------                -------
     |    |     |     |                     |
   Win11 Server Ubuntu Kali          Win11 (Isolated)
```

---

## Virtual Machines

| Machine        | OS                | Network | Role                     |
|----------------|------------------|---------|--------------------------|
| OPNsense       | Firewall         | WAN/LAN/LAN2 | Router & Gateway      |
| Windows 11     | Client           | LAN     | End-user workstation     |
| Windows Server | Server           | LAN     | Internal services        |
| Ubuntu         | Linux-based      | LAN     | System testing           |
| Kali Linux     | Linux-based      | LAN     | Security testing         |
| Windows 11     | Client           | LAN2    | Segmented / isolated host|

---

## Network Configuration

| Network | Subnet            | Gateway        | Description              |
|--------|------------------|---------------|--------------------------|
| LAN    | 192.168.10.0/24  | 192.168.10.1  | Primary internal network |
| LAN2   | 192.168.20.0/24  | 192.168.20.1  | Segmented network        |

---

## Implemented Phases

### Phase 1 – Initial Deployment

- Deployed OPNsense firewall in Hyper-V
- Created and configured virtual switches (WAN & LAN)
- Connected multiple virtual machines to the internal network
- Configured DHCP for automatic IP assignment

---

### Phase 2 – Network Verification & Troubleshooting

- Verified connectivity between all virtual machines
- Tested communication with default gateway
- Validated internet access (NAT)
- Identified DHCP issue on LAN2 (APIPA address)
- Diagnosed and resolved DHCP configuration problem
- Performed network testing using ICMP (ping)

---

### Phase 3 – Network Segmentation & IPv6

- Implemented a second internal network (LAN2)
- Configured network segmentation
- Introduced IPv6 alongside IPv4 (dual-stack)
- Verified IPv6 connectivity between hosts
- Tested internet access through NAT

---

## Screenshots

### Hyper-V Virtual Switches
![Hyper-V Switches](images/hyperv-switches.png)

### Virtual Machines Overview
![VM List](images/vm-list.png)

### OPNsense Dashboard
![OPNsense Dashboard](images/opnsense-dashboard.png)

### OPNsense Interfaces
![OPNsense Interfaces](images/opnsense-interfaces.png)

### Network Connectivity Test (Ping)
![Ping Test](images/ping-test.png)

### IP Configuration (Client)
![IP Config](images/ip-config.png)

### LAN2 Issue – APIPA Address
![LAN2 APIPA](images/lan2-apipa.png)

### OPNsense LAN2 Interface Configuration
![LAN2 Interface](images/lan2-interface.png)

### DHCP Fixed on LAN2
![LAN2 DHCP Fixed](images/lan2-dhcp-fixed.png)

### LAN2 Connectivity Restored
![LAN2 Connectivity](images/lan2-connectivity.png)

### IPv6 Configuration in OPNsense
![IPv6 OPNsense](images/ipv6-opnsense.png)

### IPv6 Test (Windows)
![IPv6 Windows](images/ipv6-windows-test.png)

### IPv6 Test (Ubuntu)
![IPv6 Ubuntu](images/ipv6-ubuntu-test.png)

---

## Connectivity Validation

Commands used during testing:

### Windows
```
ipconfig
ping 192.168.10.1
ping 8.8.8.8
```

### Ubuntu Server
```
ip a
ping 192.168.10.1
ping 8.8.8.8
ping6 2001:db8:1::1
```

---

## Key Learning Outcomes

- Designing and deploying virtual networks using Hyper-V
- Configuring OPNsense as firewall and gateway
- Implementing network segmentation (LAN & LAN2)
- Troubleshooting DHCP and connectivity issues
- Working with IPv4 and IPv6 (dual-stack networking)
- Validating NAT and external connectivity
- Performing structured network testing and verification

---

## Project Structure

```
hyperv-opnsense-security-lab/
│
├── README.md
├── docs/
│   └── lab-documentation.md
└── images/
```

📄 Detailed technical documentation:  
👉 docs/lab-documentation.md

---

## Conclusion

This project represents a **completed foundational networking lab** demonstrating practical skills in virtualization, network configuration and troubleshooting.

It serves as a strong base for more advanced labs such as Active Directory, security monitoring and attack simulations, which will be developed in separate repositories to maintain clarity and focus.

---

## Author

**Muhammad Mehdi**  
IT Security Developer Student  

---
