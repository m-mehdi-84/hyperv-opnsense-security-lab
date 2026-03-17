# Troubleshooting

During the setup of the Hyper-V OPNsense Security Lab several issues were encountered.  
The environment was built step by step and required troubleshooting at multiple stages.  
Below is a chronological overview of the main problems and the solutions used to resolve them.

---

## 1. OPNsense WAN and LAN Assigned to the Same Network

During the initial configuration of OPNsense, the WAN and LAN interfaces ended up in the same network range.  
This created a network conflict because the firewall could not properly separate internal and external traffic.

When both interfaces belong to the same subnet, routing and firewall behavior become incorrect.

### Solution

The issue was resolved by separating the interfaces using different virtual switches in Hyper-V.

Steps taken:

1. Verify that WAN and LAN were connected to the correct virtual switches.
2. Assign the WAN interface to the external network switch.
3. Assign the LAN interface to the internal lab network switch.

The LAN interface was configured with the following address:

```
192.168.10.1/24
```

After separating the interfaces into different networks, OPNsense was able to properly route traffic between WAN and LAN.

---

## 2. Accessing the OPNsense Web Interface

After configuring OPNsense, it was initially unclear which IP address should be used to access the web management interface.

### Solution

The LAN interface address was identified as:

```
192.168.10.1
```

The web interface could then be accessed via a browser:

```
https://192.168.10.1
```

This allowed the firewall configuration to be completed.

---

## 3. Windows 11 Installation Blocked by Hardware Requirements

When installing Windows 11 in a Hyper-V virtual machine, the installation stopped with a message indicating that the system did not meet the minimum hardware requirements (TPM and Secure Boot).

### Solution

The hardware requirement checks were bypassed using the Windows Registry during installation.

1. When the error appeared, open the command prompt:

```
Shift + F10
```

2. Launch the Registry Editor:

```
regedit
```

3. Navigate to:

```
HKEY_LOCAL_MACHINE\SYSTEM\Setup
```

4. Create a new key named:

```
LabConfig
```

5. Inside `LabConfig`, create the following DWORD values:

```
BypassTPMCheck
BypassSecureBootCheck
BypassRAMCheck
```

6. Set each value to:

```
1
```

After applying these changes, the Windows 11 installation continued successfully.

---

## 4. Kali Linux Issue with Hyper-V Generation 1

Kali Linux was initially installed using a **Generation 1 virtual machine** in Hyper-V.

The installation completed successfully and the system booted, but only **terminal mode (CLI)** was available.  
The graphical desktop environment (GUI) could not be accessed.

Despite this limitation, basic network tests from the terminal worked correctly.

Examples:

```
ip a
ping 192.168.10.1
ping 192.168.10.131
```

These tests confirmed that the network configuration and connectivity were functioning correctly.

However, since the graphical desktop environment could not be accessed, the virtual machine was recreated using **Generation 2**.

### Solution

The issue was resolved by creating a new Kali Linux virtual machine using **Generation 2** in Hyper-V.

Steps:

1. Create a new virtual machine in Hyper-V.
2. Select:

```
Generation 2
```

3. Attach the Kali Linux ISO image.
4. Start the installation.

After installing Kali Linux using Generation 2, the graphical desktop environment (GUI) worked correctly.

---

## 5. Ubuntu Keyboard Configuration Problem

When attempting to change the keyboard layout in Ubuntu, the following command produced an error because the required package was not installed:

```
sudo dpkg-reconfigure keyboard-configuration
```

### Solution

The missing package needed to be installed first.

1. Update the package list:

```
sudo apt update
```

2. Install the keyboard configuration package:

```
sudo apt install keyboard-configuration
```

3. Run the configuration command again:

```
sudo dpkg-reconfigure keyboard-configuration
```

4. Select the following options:

```
Generic 105-key PC
Swedish
```

The keyboard layout was successfully updated.

---

## 6. Ping Blocked by Windows Firewall

During connectivity testing, ICMP ping between Windows machines (Windows 11 and Windows Server) was blocked by the Windows Firewall.

### Solution

ICMP echo requests were enabled using PowerShell with administrator privileges.

Run the following command:

```
Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"
```

After enabling the rule, ping requests between machines worked correctly.

Example test:

```
ping 192.168.10.131
```

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
