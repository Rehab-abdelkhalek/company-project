Company Network Project
📌 Overview

This project simulates a company network infrastructure using VLANs, Inter-VLAN Routing, and FortiGate Firewall integration. The goal is to segment the network into different departments, improve security, and implement controlled communication between them.

🏢 Departments & VLANs

The network is divided into multiple VLANs, each representing a company department:
| Department   | VLAN ID | Description                       |
| ------------ | ------- | --------------------------------- |
| HR           | 10      | Human Resources department VLAN   |
| PR           | 20      | Public Relations department VLAN  |
| Marketing    | 30      | Marketing department VLAN         |
| Wireless LAN | 40      | Wi-Fi access for employees/guests |

🎯 Objectives

Configure VLANs on Cisco switches for department segmentation.

Implement Inter-VLAN Routing to enable communication between VLANs.

Integrate FortiGate Firewall to apply security policies and control access.

Add Wireless Network Support for mobile users.

Test advanced VLAN features like trunking and firewall-based filtering.

Document all configurations and prepare a final presentation.

📅 Project Plan
Week 1: VLAN Configuration Basics

Create VLANs for HR, PR, Marketing, and Wireless.

Assign VLAN IDs and configure switch ports.

Implement basic Inter-VLAN Routing.

Deliverables: VLAN configuration document + network topology diagram.

Week 2: FortiGate Integration

Configure VLAN interfaces on FortiGate.

Set up Inter-VLAN Routing on FortiGate.

Define firewall policies (e.g., HR ↔ Marketing allowed, PR restricted).

Deliverables: FortiGate configuration + firewall policy documentation.

Week 3: VLAN Trunks + Testing

Implement VLAN trunking between switches and FortiGate.

Test communication across VLANs.

Validate firewall rules with connectivity tests (ping, access control).

Deliverables: Testing report + trunk configuration details.

🔐 Firewall Policy Matrix
| From → To     | HR | PR | Marketing | Wireless |
| ------------- | -- | -- | --------- | -------- |
| **HR**        | ✅  | ❌  | ✅         | ❌        |
| **PR**        | ❌  | ✅  | ❌         | ❌        |
| **Marketing** | ✅  | ❌  | ✅         | ❌        |
| **Wireless**  | ❌  | ❌  | ❌         | ✅        |

✅ = Allowed | ❌ = Blocked

⚙️ Tools & Technologies

Cisco Packet Tracer – Network simulation.

FortiGate Firewall – Security policies and inter-VLAN routing.

Markdown (GitHub) – Project documentation.

✅ Expected Outcomes

By completing this project, we will achieve:

Proper VLAN segmentation for departments.

Secure communication using FortiGate policies.

Controlled wireless network access.

Clear documentation and presentation of results.
