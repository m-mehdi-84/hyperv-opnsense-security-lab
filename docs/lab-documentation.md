# Troubleshooting

During the setup of the Hyper-V OPNsense Security Lab several issues were encountered.  
The environment was built step by step and required troubleshooting at multiple stages.  
Below is a chronological overview of the main problems and the solutions used to resolve them.

---

## 1. OPNsense WAN and LAN Assigned to the Same Network

[... ALL DIN GAMLA TEXT ORÖRD ...]

---

## 7. Network Connectivity Verification

After all virtual machines were configured, network connectivity was verified between systems.

Examples:

```
ping 192.168.10.1
ping 192.168.10.132
ping 192.168.10.138
```

Successful responses confirmed that:

- the LAN network was functioning correctly
- the OPNsense firewall was routing traffic properly
- all virtual machines could communicate within the network

---

## 8. LAN2 DHCP Issue (Network Segmentation)

When introducing a second network (LAN2), a new subnet was configured in OPNsense:

```
192.168.20.0/24
```

A dedicated Windows 11 client (Win11-LAN2) was connected to this network and configured to obtain an IP address via DHCP.

### Problem

The client received an APIPA address:

```
169.254.x.x
```

Observed issues:

- No default gateway
- No connectivity to `192.168.20.1`
- Network unreachable

### Troubleshooting

The following checks were performed:

- Verified Hyper-V switch configuration for LAN2
- Checked VM network adapter connection
- Confirmed OPNsense interface (OPT1 / LAN2)
- Verified subnet configuration (/24)
- Reviewed DHCP settings

All configurations appeared correct, but the issue persisted.

### Root Cause

The DHCP service was not configured to listen on the LAN2 interface.

This resulted in DHCP requests being sent without receiving any response.

### Solution

- Added LAN2 (OPT1) to the DHCP service interface list
- Renewed the IP configuration on the client

### Result

The client successfully received:

```
192.168.20.x
Gateway: 192.168.20.1
```

Connectivity was restored and network communication worked as expected.

---
