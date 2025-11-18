# Company Network Infrastructure

## What This Project Does
This project connects two company branches using a secure, scalable, and well-segmented network design.  
The focus is on reliability, security, and easy expansion.

---

## The Setup
Both branches connect through a cloud WAN link protected by FortiGate firewalls.  
Each branch uses VLAN segmentation to separate departments and improve security.

---

## Main Components

### **OSPF Routing**
Dynamic routing using OSPF lets routers automatically calculate the best paths.  
If a link fails, OSPF reroutes traffic instantly.

### **VLAN Segmentation**
Each department has its own VLAN to separate traffic and apply different security policies.

### **Inter-VLAN Routing**
Layer 3 routing allows VLANs to communicate only when needed and only through controlled rules.

### **Security Policies**
FortiGate firewalls at both sites inspect and filter traffic between:
- VLANs  
- Branches  
- The cloud link  

Nothing passes without security checks.

---

## Equipment Used
- Cisco routers (WAN + routing)
- FortiGate firewalls
- Layer 3 switches for VLAN routing
- User PCs & endpoints

---

## IP Addressing
Using private IP addressing:

- **192.168.x.x/24** — Internal VLANs  
- **/30 subnets** — Point-to-point router links  
- **14.0.0.0/30** — Cloud link  

---

## IP Addressing Plan

| Network / Subnet      | Description               | IP Range                   |
|-----------------------|----------------------------|----------------------------|
| 192.168.10.0/24       | Internal VLAN 10          | 192.168.10.1 - 192.168.10.254 |
| 192.168.20.0/24       | Internal VLAN 20          | 192.168.20.1 - 192.168.20.254 |
| 192.168.30.0/24       | Internal VLAN 30          | 192.168.30.1 - 192.168.30.254 |
| 192.168.40.0/24       | Internal VLAN 40          | 192.168.40.1 - 192.168.40.254 |
| 192.168.50.0/24       | Internal VLAN 50          | 192.168.50.1 - 192.168.50.254 |
| 192.168.60.0/24       | Internal VLAN 60          | 192.168.60.1 - 192.168.60.254 |
| 192.168.100.0/24      | Internal VLAN 100         | 192.168.100.1 - 192.168.100.254 |
| 192.168.200.0/24      | Internal VLAN 200         | 192.168.200.1 - 192.168.200.254 |
| 13.0.0.0/30           | Router Link 1             | 13.0.0.1 - 13.0.0.2 |
| 12.0.0.0/30           | Router Link 2             | 12.0.0.1 - 12.0.0.2 |
| 14.0.0.0/30           | Cloud Connectivity Link   | 14.0.0.1 - 14.0.0.2 |

---

## How It Works
- Branch traffic stays local unless it needs another VLAN or the other branch.
- OSPF automatically handles routing & failures.
- Firewalls enforce strict traffic control.

---

## Testing Performed
- Branch-to-branch connectivity tests  
- Link failure tests (OSPF rerouting)  
- VLAN isolation verification  
- Firewall rule validation  

---

# Network Device Configurations

---

## R1 CONFIG
```
hostname R1
no ip domain lookup
ip cef

interface FastEthernet0/0
 ip address 13.0.0.1 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet1/0
 ip address 14.0.0.1 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet2/0
 no ip address
 shutdown
 duplex half

router ospf 1
 network 13.0.0.0 0.0.0.3 area 0
 network 14.0.0.0 0.0.0.3 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
 transport input all
```

---

## R2 CONFIG
```
hostname R2
no ip domain lookup
ip cef

interface FastEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 duplex auto
 speed auto
 no shutdown

interface FastEthernet0/1
 ip address 192.168.20.1 255.255.255.0
 duplex auto
 speed auto
 no shutdown

interface FastEthernet1/0
 no switchport
 ip address 192.168.100.1 255.255.255.0
 no shutdown

interface FastEthernet1/1
 no switchport
 ip address 192.168.50.1 255.255.255.0
 no shutdown

router ospf 1
 log-adjacency-changes
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.50.0 0.0.0.255 area 0
 network 192.168.100.0 0.0.0.255 area 0

ip route 0.0.0.0 0.0.0.0 192.168.100.2

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
```

---

## R3 CONFIG
```
hostname R3
no ip domain lookup
ip cef

interface FastEthernet0/0
 ip address 12.0.0.1 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet1/0
 ip address 11.0.0.1 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet2/0
 no ip address
 shutdown
 duplex half

router ospf 1
 network 11.0.0.0 0.0.0.3 area 0
 network 12.0.0.0 0.0.0.3 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
 transport input all
```

---

## R4 CONFIG
```
hostname R4
no ip domain lookup
ip cef

interface FastEthernet0/0
 ip address 192.168.30.1 255.255.255.0
 duplex auto
 speed auto
 no shutdown

interface FastEthernet0/1
 ip address 192.168.40.1 255.255.255.0
 duplex auto
 speed auto
 no shutdown

interface FastEthernet1/0
 no switchport
 ip address 192.168.200.1 255.255.255.0
 no shutdown

interface FastEthernet1/1
 no switchport
 ip address 192.168.60.1 255.255.255.0
 no shutdown

router ospf 1
 log-adjacency-changes
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0
 network 192.168.60.0 0.0.0.255 area 0
 network 192.168.200.0 0.0.0.255 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
```

---

## R5 CONFIG
```
hostname R5
no ip domain lookup
ip cef

interface FastEthernet0/0
 no ip address
 shutdown
 duplex half

interface FastEthernet1/0
 ip address 13.0.0.2 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet2/0
 ip address 12.0.0.2 255.255.255.252
 duplex half
 no shutdown

interface FastEthernet3/0
 no ip address
 shutdown
 duplex half

router ospf 1
 network 12.0.0.0 0.0.0.3 area 0
 network 13.0.0.0 0.0.0.3 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
 transport input all
```
# Snort IDS – Key Installation & Configuration Summary

## ✅ Essential Steps

### 1. Prerequisites & Dependencies
- Update the system
- Install build tools
- Install required networking libraries:
  - libpcap
  - OpenSSL
  - zlib
  - lzma
  - and others...

---

## ✅ Core Components Installed

### 1. PCRE
- Pattern-matching library.
- Snort needs it to detect attacks using regex rules.

### 2. Hyperscan
- Intel high-speed pattern-matching engine.
- Makes Snort much faster when scanning payloads.

### 3. DAQ (Data Acquisition Library)
- Snort’s packet-capturing layer.
- Responsible for reading packets from the network interface.

### 4. Boost C++ Libraries
- Required for compiling Snort 3.

### 5. Snort 3
- The main IDS application after all dependencies are prepared.

---

## ✅ Critical Configuration

### Disable GRO/LRO
- Must disable:
  - GRO = Generic Receive Offload
  - LRO = Large Receive Offload
- Because they merge packets, breaking Snort’s ability to inspect traffic correctly.

---

## ✅ Testing Snort

### 1. Custom Rule
- Created a custom ICMP detection rule.

### 2. Running Snort in alert mode
- Ran Snort on a specific network interface to monitor live traffic.

---

## ✅ What You Can Skip
- The long Arabic explanation of each library.
  - Useful for learning, but not necessary for installation workflow.

- What matters is the core workflow:
  1. Install dependencies  
  2. Build from source  
  3. Configure  
  4. Add rules  
  5. Test  

- **Order is important**  
  Each component depends on the previous one — you cannot skip or install out of order.

---

## 📌 Final Added Note (as requested)
The document contains many detailed explanations about what each library does and why it's needed. These are useful for understanding how Snort works internally, but they are not required to successfully complete the installation. The essential part is following the correct installation sequence, because every component depends on the previous one. The workflow remains: install dependencies → build → configure → test with rules.

