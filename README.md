# 🚀 Company Network Infrastructure & Security Architecture
### **Full Multi-Site Design | OSPF | FortiGate | VLANs | IPsec VPN | AD | DHCP | DNS | Snort IDS**

This project delivers a fully designed, fully configured, and fully tested enterprise-grade network infrastructure connecting two remote company branches.  
The network is built with scalability, segmentation, high availability, and multilayer security as top priorities.

It simulates a real corporate environment with routing, switching, firewalls, identity services, VPN encryption, and intrusion detection.

---

## 📌 1. Project Overview

The goal was to design and implement a secure and resilient enterprise network linking:

- **Branch 1**
- **Headquarters (HQ)**
- Through an **ISP backbone**
- Protected by **FortiGate firewalls**
- Connected using **Cisco routers and L3 switches**
- Managed through **Active Directory**
- Monitored by **Snort IDS**

---

## 🧩 2. High-Level Network Features

- ✔ VLAN Segmentation for all departments  
- ✔ Inter-VLAN Routing on Layer 3 switches  
- ✔ EtherChannel (LACP) for redundancy & better throughput  
- ✔ OSPF Dynamic Routing + Static routes on FortiGate  
- ✔ Site-to-Site IPsec VPN (AES-256 / SHA-256 / PFS)  
- ✔ FortiGate Firewall Policies (LAN, VPN, NAT)  
- ✔ Certificate Deployment (Self-Signed SSL)  
- ✔ LDAP Integration with FortiGate for centralized auth  
- ✔ **Windows Server services:**
  - Primary Domain Controller (PDC)
  - Additional Domain Controller (ADC)
  - DNS Server
  - DHCP Server
  - Group Policy Objects (GPO)
- ✔ Snort IDS Connected via SPAN for real-time threat detection  
- ✔ Kali Linux Attack Simulation  
- ✔ Full monitoring, logging, and traffic analysis  

---

## 🏛 3. Network Architecture

### 🔹 **Branch 1**
**VLANs:**
- VLAN 10 — Users  
- VLAN 20 — Management  
- VLAN 50 — Admin  
- VLAN 184 — Servers  

**Routing & Switching:**
- L3 Switch with SVIs  
- Static default route to FortiGate  
- OSPF to core router  

**Firewall:**
- FortiGate B1  
- Static + OSPF routing  
- Policies: LAN → VPN, LAN → Internet, Implicit Deny  

---

### 🔹 **HQ Branch**
**VLANs:**
- VLAN 30 — Sales  
- VLAN 40 — HR  
- VLAN 60 — Administration  
- VLAN 184 — Servers  

**Routing:**
- L3 switch running Inter-VLAN routing  
- Static routes to FortiGate  
- OSPF to upstream routers  

**Firewall:**
- FortiGate HQ  
- VPN termination  
- NAT  
- Internal security rules  
- LDAP/AD authentication  

---

### 🔹 **ISP Backbone**
- Runs **OSPF Area 0**
- Exchanges routes between Branch and HQ

---

## 🌐 4. IP Addressing

- ✔ VLANs → `192.168.x.0/24`  
- ✔ Router-to-router links → `/30`  
- ✔ Firewall uplinks → `/30`  
- ✔ Core/Distribution links → `192.168.100.0` & `192.168.200.0`  

### **Addressing Table**
| Subnet           | Use                     |
| ---------------- | ------------------------ |
| 192.168.10.0/24  | Branch 1 Users           |
| 192.168.20.0/24  | Branch 1 Management      |
| 192.168.50.0/24  | Branch 1 Admin           |
| 192.168.30.0/24  | HQ Sales                 |
| 192.168.40.0/24  | HQ HR                    |
| 192.168.60.0/24  | HQ Admin                 |
| 192.168.184.0/24 | Servers                  |
| 13.0.0.0/30      | Router Link B1 → ISP     |
| 12.0.0.0/30      | Router Link HQ → ISP     |
| 14.0.0.0/30      | FortiGate → Router Link  |

---

## 🔶 5. Routing Design (OSPF + Static)

### ✔ **Layer 3 Switches**
- Inter-VLAN routing  
- Static default route → FortiGate  

### ✔ **Routers (R1–R5)**
- Handle OSPF between branches  
- Advertise internal networks through the ISP backbone  

### ✔ **FortiGate**
- Static routes for branch VLANs  
- OSPF enabled only for core links  
- Selective redistribution  

---

## 🔐 6. FortiGate Firewall Security

### ✔ **Policies**
- Branch → HQ VPN  
- HQ → Branch VPN  
- VLAN-to-VLAN controlled access  
- Internet NAT  
- Implicit deny for all other traffic  
- No-inspection profiles for internal trusted paths  

### ✔ **VPN Configuration**
- AES-256 Encryption  
- SHA-256 Hashing  
- Diffie-Hellman Group 14  
- PFS enabled  
- Tunnel-based selectors  

---

## 🖥 7. Active Directory Infrastructure

### ✔ **Domain Controllers**
- PDC + ADC for redundancy  

### ✔ **Core Services**
- DNS  
- DHCP  
- LDAP  
- GPO  

### ✔ **DHCP Scopes**
- VLAN user networks  
- Server networks  
- Reserved IP ranges for infrastructure  

---

## 🛡 8. IDS Deployment (Snort)

Snort installed on Ubuntu and connected via **SPAN/Monitor Port**.

### ✔ Required Libraries Installed
- PCRE  
- Hyperscan  
- gperftools  
- DAQ  
- Boost  
- Ragel  
- Flatbuffers  

### ✔ Snort 3 Installed from Source

### ✔ Configuration Steps
- Disabled GRO/LRO  
- Added custom rules  
- Enabled ICMP detection  
- Ran Snort in **alert mode** and **IDS mode**  

### ✔ Security Validation
- Kali Linux used for attack simulation:  
  - Scanning  
  - Enumeration  
  - Exploit-like traffic  
- Snort successfully logged and alerted  

---

## 🔬 9. Testing Performed

- ✔ VLAN isolation  
- ✔ Inter-VLAN routing verification  
- ✔ OSPF adjacency tests  
- ✔ Failover route testing  
- ✔ Branch-to-branch communication  
- ✔ Firewall rule validation  
- ✔ VPN encryption tests  
- ✔ LDAP authentication checks  
- ✔ Snort IDS alert generation  

---

## 🎯 Final Summary

This project represents a complete multi-site enterprise network including:

- Routing  
- Switching  
- Security  
- VPN encryption  
- Active Directory  
- Firewalls  
- IDS monitoring  
- Attack simulation  
- Certificates  
- Identity integration  

It fully simulates how modern companies design and secure their infrastructure.

---
