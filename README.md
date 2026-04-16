# 🖥️ Active Directory + DHCP Home Lab

## Overview

This home lab demonstrates the deployment of a Windows Server Active Directory environment with DHCP, connected to a Windows client machine — all virtualized in VirtualBox. The goal was to simulate a real-world corporate network where a Domain Controller manages authentication and IP address assignment for domain-joined clients.

---

## 🧰 Technologies Used

| Tool | Purpose |
|---|---|
| VirtualBox | Hypervisor / virtualization platform |
| Windows Server 2019 | Domain Controller + DHCP Server |
| Windows Client | Domain-joined workstation |
| Active Directory Domain Services (AD DS) | User/machine management |
| DHCP Server Role | Automated IP address assignment |
| DNS | Name resolution within the domain |

---

## 🌐 Network Topology

```
+------------------------------+       +-----------------------------+
|   Windows Server 2019        |       |   Windows Client Machine    |
|   Role: DC + DHCP Server     | <---> |   Role: Domain Member       |
|                              |       |                             |
|   IP: 172.16.0.1 (static)   |       |   IP: 172.16.0.100-200      |
|   Domain: mydomain.com       |       |   (DHCP assigned)           |
+------------------------------+       +-----------------------------+
           |
    VirtualBox Internal Network
```

---

## ⚙️ Lab Configuration

### Domain Controller / DHCP Server

- **OS:** Windows Server 2019
- **Roles Installed:** Active Directory Domain Services, DHCP Server, DNS Server
- **Domain Name:** `mydomain.com`
- **Static IP:** `172.16.0.1`
- **DHCP Scope:** `172.16.0.100 – 172.16.0.200`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `172.16.0.1`
- **DNS:** Points to itself (DC handles name resolution)

### Client Machine

- **OS:** Windows (Client)
- **IP Assignment:** Dynamic (via DHCP from DC)
- **Domain Joined:** ✅ `mydomain.com`
- **DNS:** `172.16.0.1` (resolves domain names through the DC)

---

## 🔧 Steps Performed

1. **Installed VirtualBox** and created two VMs on an Internal Network adapter
2. **Configured Windows Server 2019**
   - Assigned a static IP address
   - Installed the AD DS role and promoted the server to Domain Controller
   - Created the domain `mydomain.com`
3. **Configured DHCP Server Role**
   - Created a DHCP scope: `172.16.0.100 – 172.16.0.200`
   - Set DNS and gateway options within the scope
   - Authorized the DHCP server in Active Directory
4. **Configured the Client Machine**
   - Set DNS to point to the DC's IP
   - Joined the client to `mydomain.com`
   - Verified DHCP lease was received from the server
5. **Verified Connectivity**
   - Ran `ipconfig /all` on client to confirm DHCP server field
   - Confirmed hostname resolution between machines
   - Verified client appeared in AD Users and Computers

---

## ✅ Skills Demonstrated

- Active Directory Domain Services deployment
- DHCP scope creation and lease management
- DNS configuration for internal name resolution
- Domain join process (client to server)
- Virtual networking with VirtualBox internal adapters
- Windows Server role management

---

## 📌 Notes

- All VMs were connected via VirtualBox **Internal Network** to isolate lab traffic
- DHCP authorization in AD is required for the server to hand out leases — a common real-world gotcha
- This lab mirrors a foundational enterprise IT setup seen in Tier 1/2 helpdesk environments

---

*Built as part of an ongoing IT home lab portfolio. See other projects for pfSense/VLAN segmentation, osTicket ticketing system, and Group Policy management.*
