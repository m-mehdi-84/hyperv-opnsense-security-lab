# Hyper-V OPNsense Security Lab

A personal **cybersecurity home lab** built using **Hyper-V** and **OPNsense firewall** to simulate a realistic internal network environment.

This lab environment includes multiple virtual machines representing a small enterprise infrastructure used for **network administration, security testing, and cybersecurity learning**.

The project is part of my **IT Security Developer studies** and will continue to evolve with additional labs such as Active Directory, network segmentation, attack simulation, and monitoring.

---

## Lab Overview

This lab simulates a **small internal corporate network** using virtualization.

The environment includes:

- Hyper-V virtualization  
- OPNsense firewall  
- Windows and Linux servers  
- Kali Linux attacker machine  
- internal LAN network  

The goal is to practice:

- network architecture  
- firewall configuration  
- virtualization  
- system administration  
- cybersecurity testing  

---

## Network Topology

```
                 Internet
                    │
                    ▼
                WAN Network
                    │
                    ▼
            OPNsense Firewall
                    │
                    ▼
        LAN Network (192.168.10.0/24)
                    │
      ┌─────────────┼─────────────┐
      │             │             │
      ▼             ▼             ▼
 Windows 11   Windows Server   Ubuntu Server
  (Client)        (Server)        (Linux)

                    │
                    ▼
                Kali Linux
            (Security Testing)
```

---

## Virtual Machines

```
OPNsense (Firewall / Router)
│
├── Windows 11       → Client workstation
├── Windows Server   → Server environment
├── Ubuntu Server    → Linux server
└── Kali Linux       → Security testing machine
```

| Machine | Role | Operating System | IP Address |
|--------|------|------------------|-----------|
| OPNsense | Firewall / Router | OPNsense | 192.168.10.1 |
| Windows 11 | Client workstation | Windows 11 | 192.168.10.144 |
| Windows Server | Server environment | Windows Server 2025 | 192.168.10.131 |
| Ubuntu Server | Linux server | Ubuntu Server | 192.168.10.132 |
| Kali Linux | Security testing | Kali Linux | 192.168.10.138 |

---

## Network Configuration

```
Internet
   │
   ▼
WAN Interface
   │
   ▼
OPNsense Firewall
   │
   ▼
LAN Network (192.168.10.0/24)
   │
   ├── Windows 11
   ├── Windows Server
   ├── Ubuntu Server
   └── Kali Linux
```

| Component | Description |
|-----------|-------------|
| WAN | External network connected to internet |
| LAN | Internal network managed by OPNsense |
| Firewall | OPNsense controlling traffic |
| Virtual Switch | Hyper-V virtual networking |

---

## Connectivity Verification

Connectivity between virtual machines was verified using **ICMP ping tests**.

Example connectivity tests:

```
Windows 11 → OPNsense
Windows 11 → Ubuntu Server
Ubuntu Server → Windows Server
Kali Linux → All machines
```

Successful responses confirmed:

- correct network configuration  
- functioning gateway  
- internal connectivity  
- proper firewall routing  

---

## Screenshots

### Network Topology
![Topology](images/topology.png)

### OPNsense Dashboard
![OPNsense](images/opnsense-dashboard.png)

### Firewall Rules
![Firewall](images/firewall-rules.png)

### Hyper-V Virtual Machines
![Hyper-V](images/hyperv-vms.png)

### Network Interfaces
![Interfaces](images/network-interfaces.png)

### Connectivity Test
![Ping Test](images/ping-test.png)

---

## Project Structure

```
hyperv-opnsense-security-lab
│
├── README.md
├── docs
│   └── lab-notes.md
└── images
    ├── topology.png
    ├── opnsense-dashboard.png
    ├── firewall-rules.png
    ├── hyperv-vms.png
    ├── network-interfaces.png
    └── ping-test.png
```

---

## Documentation

Additional notes and step-by-step lab documentation can be found in the **docs** directory.

This includes:

- installation notes  
- configuration steps  
- troubleshooting steps  
- lab observations  

The documentation will expand as the lab evolves with new cybersecurity experiments.

---

## Results

The lab environment was successfully deployed using **Hyper-V** with **OPNsense** acting as the firewall and gateway.

All virtual machines were able to communicate within the LAN network and access the internet through the firewall.

Connectivity verification using ICMP ping confirmed proper routing and network configuration across the environment.

---

## Key Skills Demonstrated

| Area | Skills |
|------|--------|
| Virtualization | Hyper-V lab deployment, VM management |
| Networking | IP addressing, LAN/WAN design |
| Security | OPNsense firewall configuration |
| Systems Administration | Windows 11, Windows Server, Ubuntu Server, Kali Linux |
| Troubleshooting | Network testing and connectivity verification |

---

## Future Lab Extensions

This lab will continue expanding with additional cybersecurity experiments.

Planned future labs include:

- Active Directory domain environment  
- Network segmentation using VLANs  
- Attack simulation using Kali Linux  
- IDS / IPS testing in OPNsense  
- Log monitoring and analysis  
- Security incident investigation scenarios  

---

## Conclusion

This project demonstrates the creation of a functional **cybersecurity lab environment** using virtualization and open-source security tools.

The lab provides a safe environment for practicing networking, system administration, and security testing.

The environment will continue to evolve as new technologies and security scenarios are introduced throughout the **IT Security Developer program**.

---

## Author

**Mehdi**

IT Security Developer Student  
Building hands-on cybersecurity labs focused on networking, infrastructure, and security testing.
