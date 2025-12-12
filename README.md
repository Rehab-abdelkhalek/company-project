🚀 Company Network Infrastructure & Security Architecture
Full Multi-Site Design | OSPF | FortiGate | VLANs | IPsec VPN | AD | DHCP | DNS | Snort IDS

This project delivers a fully designed, fully configured, and fully tested enterprise-grade network infrastructure connecting two remote company branches.
The network is built with scalability, segmentation, high availability, and multilayer security as top priorities.

It simulates a real corporate environment with routing, switching, firewalls, identity services, VPN encryption, and intrusion detection.
📌 1. Project Overview

The goal was to design and implement a secure and resilient enterprise network linking:

Branch 1

Headquarters (HQ)

Through an ISP backbone

Protected by FortiGate firewalls,

Connected using Cisco routers and L3 switches,

Managed through Active Directory,

And monitored by Snort IDS.

🧩 2. High-Level Network Features
✔ VLAN Segmentation for all departments
✔ Inter-VLAN Routing on Layer 3 switches
✔ EtherChannel (LACP) for redundancy & better throughput
✔ OSPF Dynamic Routing + Static routes on FortiGate
✔ Site-to-Site IPsec VPN (AES-256/SHA-256/PFS)
✔ FortiGate Firewall Policies (LAN, VPN, NAT)
✔ Certificate Deployment (Self-Signed SSL)
✔ LDAP Integration with FortiGate for centralized auth
✔ Windows Server:

Primary Domain Controller (PDC)

Additional Domain Controller (ADC)

DNS Server

DHCP Server

GPO Policies

✔ Snort IDS Connected via SPAN for real-time threat detection
✔ Kali Linux Attack Simulation for testing
✔ Full monitoring, logging, and traffic analysis

🏛 3. Network Architecture
🔹 Branch 1

Includes:

VLAN 10 (Users)

VLAN 20 (Management)

VLAN 50 (Admin)

VLAN 184 (Servers)

Routing & Switching:

L3 Switch with SVIs

Static default route to FortiGate

OSPF to core router

Firewall:

FortiGate B1 → Static + OSPF routing

Policies: LAN → VPN, LAN → Internet, Implicit Deny

🔹 HQ Branch

Includes:

VLAN 30 (Sales)

VLAN 40 (HR)

VLAN 60 (Administration)

VLAN 184 (Servers)

Routing:

L3 Switch with Inter-VLAN routing

Static route to FortiGate

OSPF upstream

Firewall:

FortiGate HQ → VPN termination, NAT, internal security rules

LDAP/Auth with AD
🔹 ISP Backbone

Runs OSPF Area 0, exchanging routes between R-B1 & R-HQ.

🌐 4. IP Addressing
✔ VLANs → 192.168.x.0/24
✔ Router-to-router → /30
✔ Firewall uplinks → /30
✔ Core/Distribution links → 192.168.100.0 & 192.168.200.0
| Subnet           | Use                     |
| ---------------- | ----------------------- |
| 192.168.10.0/24  | Branch 1 Users          |
| 192.168.20.0/24  | Branch 1 Management     |
| 192.168.50.0/24  | Branch 1 Admin          |
| 192.168.30.0/24  | HQ Sales                |
| 192.168.40.0/24  | HQ HR                   |
| 192.168.60.0/24  | HQ Admin                |
| 192.168.184.0/24 | Servers                 |
| 13.0.0.0/30      | Router Link B1 → ISP    |
| 12.0.0.0/30      | Router Link HQ → ISP    |
| 14.0.0.0/30      | FortiGate → Router Link |

🔶 5. Routing Design (OSPF + Static)
✔ Layer 3 switches:

Inter-VLAN routing

Static default routes → FortiGate

✔ Routers (R1–R5):

Handle OSPF between branches

Share all internal subnets with ISP router

✔ FortiGate:

Static routes for all VLANs

OSPF only for core links

Selected routes redistributed

🔐 6. FortiGate Firewall Security
✔ Policies include:

Branch-to-HQ VPN traffic

HQ-to-Branch VPN traffic

VLAN-to-VLAN controlled access

Internet NAT

Implicit Deny for unmatched traffic

No-inspection profiles for trusted internal paths

NAT + PAT for internet access

✔ VPN Configuration:

AES-256 Encryption

SHA-256 Hashing

DH Group 14

PFS enabled

Tunnel-based selectors
7. Active Directory Infrastructure
✔ PDC + ADC deployed for:

Redundancy

Load balancing

✔ Services installed:

DNS

DHCP

LDAP

Group Policy Objects

✔ DHCP scopes created for:

Department VLANs

Server segments

Reserved ranges for firewalls/switches
🛡 8. IDS Deployment (Snort)

Snort was installed on Ubuntu and connected to the network using a SPAN/monitor port from the L3 switch.

✔ Installed Libraries:

PCRE

Hyperscan

gperftools

DAQ

Boost

Ragel

Flatbuffers

✔ Snort 3 Installed from Source
✔ Configuration:

Disabled GRO/LRO

Custom rules created

ICMP detection testing

Snort running in alert mode & IDS mode

✔ Security Validation:

Kali Linux used to:

Scan

Enumerate

Generate malicious signatures

Snort successfully generated alerts → verifying IDS accuracy.

🔬 9. Testing Performed
✔ VLAN isolation
✔ Inter-VLAN routing
✔ OSPF adjacency checks
✔ Failover route testing
✔ Branch-to-branch communication
✔ Firewall filtering behavior
✔ VPN encryption tests
✔ ADS (LDAP) authentication
✔ Snort IDS attack detection

🎯 Final Summary

This project represents a complete enterprise network, covering:

Routing

Switching

VLANs

Security

VPN

Active Directory

Firewalls

IDS monitoring

Attack simulation

Certificates

Identity integration

It provides a realistic simulation of how modern companies build and protect their networks.

