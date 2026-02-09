# UNIVERSITY CAMPUS NETWORK PROJECT

## 📌 Overview
This project is a network design and implementation for **Albion University**, which has two campuses located 20 miles apart.  
The network is designed using **VLANs, Routing (RIPv2), DHCP, and Inter-VLAN Routing** to provide full end-to-end connectivity between departments, faculties, internal servers, and an external cloud email server.

---

## 🗺️ Network Topology
<p align="center">
  <img src="https://github.com/user-attachments/assets/3e8b7fe5-67cf-435e-b892-e11ff47f1bca" width="900">
</p>

---

## 📚 Coursework Brief

Albion University consists of two campuses:
- **Main Campus**
- **Smaller Campus**

The university has four faculties:
- Health and Sciences
- Business
- Engineering and Computing
- Art and Design

Each staff member has a PC, and students access PCs via laboratories.

---

## 🏢 Campus Structure

### Main Campus
- **Building A**
  - Administrative departments: Management, HR, Finance
  - Faculty of Business
  - VLAN-based segmentation is required
- **Building B**
  - Faculty of Engineering & Computing
  - Faculty of Art & Design
- **Building C**
  - Student Labs
  - IT Department
  - Hosts internal Web Server and other servers

An **external Email Server** is hosted in the cloud.

### Smaller Campus
- Faculty of Health & Sciences
- Staff and student labs are located on different floors

---

## 🧾 Requirements
- Each department/faculty must be on a **separate IP network**
- Switches must be configured with **VLANs and security**
- **RIPv2** is used for internal routing
- **Static routing** is used for external server access
- Devices in Building A must obtain IP addresses via **Router-based DHCP**

---

## 🧰 Devices Used
- Router 2911 (3 Units)
- Multilayer Switch L3 (1 Unit)
- Switch L2 (10 Units)
- End Devices (PCs)
- Server (3 Units)

---

## 🔌 Cable Types
- Serial DCE
- Copper Straight-Through
- Copper Cross-Over

---

## 🔧 VLAN Allocation

| VLAN ID | Name       | Department / Area |
|-------:|------------|-------------------|
| 10 | ADMIN     | Administration |
| 20 | HR        | Human Resources |
| 30 | FINANCE   | Finance |
| 40 | BUSINESS  | Business Faculty |
| 50 | E&C       | Engineering & Computing |
| 60 | A&D       | Art & Design |
| 70 | STUDLAB   | Student Labs |
| 80 | ITLAB     | IT Department |
| 90 | STAFF     | Health & Science Staff |
| 100 | STUDENT  | Health & Science Students |

---

## 🔧 Switch L2 Configuration

### SWITCH ADMIN
```bash
enable
configure terminal
vlan 10
 name ADMIN
interface range fa0/1-24
 switch mode access
 switch access vlan 10
exit


SWITCH HR
enable
configure terminal
vlan 20
 name HR
interface range fa0/1-24
 switch mode access
 switch access vlan 20
exit


SWITCH FINANCE
enable
configure terminal
vlan 30
 name FINANCE
interface range fa0/1-24
 switch mode access
 switch access vlan 30
exit


SWITCH BUSINESS
enable
configure terminal
vlan 40
 name BUSINESS
interface range fa0/1-24
 switch mode access
 switch access vlan 40
exit


SWITCH E&C
enable
configure terminal
vlan 50
 name E&C
interface range fa0/1-24
 switch mode access
 switch access vlan 50
exit


SWITCH A&D
enable
configure terminal
vlan 60
 name A&D
interface range fa0/1-24
 switch mode access
 switch access vlan 60
exit


SWITCH STUDENT LAB
enable
configure terminal
vlan 70
 name STUDLAB
interface range fa0/1-24
 switch mode access
 switch access vlan 70
exit


SWITCH IT LAB
enable
configure terminal
vlan 80
 name ITLAB
interface range fa0/1-24
 switch mode access
 switch access vlan 80
exit


🔀 Multilayer Switch (L3) Configuration
enable
configure terminal
interface gigabitEthernet1/0/1
 switch mode trunk
exit

interface gigabitEthernet1/0/2
 switch mode access
 switch access vlan 10
exit

interface gigabitEthernet1/0/3
 switch mode access
 switch access vlan 20
exit

interface gigabitEthernet1/0/4
 switch mode access
 switch access vlan 30
exit

interface gigabitEthernet1/0/5
 switch mode access
 switch access vlan 40
exit

interface gigabitEthernet1/0/6
 switch mode access
 switch access vlan 50
exit

interface gigabitEthernet1/0/7
 switch mode access
 switch access vlan 60
exit

interface gigabitEthernet1/0/8
 switch mode access
 switch access vlan 70
exit

interface gigabitEthernet1/0/9
 switch mode access
 switch access vlan 80
exit


Router Main Configuration (Router-on-a-Stick)
interface gig0/0
 no shutdown
exit

interface gig0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
exit

interface gig0/0.20
 encapsulation dot1Q 20
 ip address 192.168.2.1 255.255.255.0
exit

interface gig0/0.30
 encapsulation dot1Q 30
 ip address 192.168.3.1 255.255.255.0
exit

interface gig0/0.40
 encapsulation dot1Q 40
 ip address 192.168.4.1 255.255.255.0
exit

interface gig0/0.50
 encapsulation dot1Q 50
 ip address 192.168.5.1 255.255.255.0
exit

interface gig0/0.60
 encapsulation dot1Q 60
 ip address 192.168.6.1 255.255.255.0
exit

interface gig0/0.70
 encapsulation dot1Q 70
 ip address 192.168.7.1 255.255.255.0
exit

interface gig0/0.80
 encapsulation dot1Q 80
 ip address 192.168.8.1 255.255.255.0
exit


📡 DHCP Configuration (Router-Based)
service dhcp

ip dhcp pool ADMIN
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 192.168.1.1
exit

ip dhcp pool HR
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
 dns-server 192.168.2.1
exit

ip dhcp pool FINANCE
 network 192.168.3.0 255.255.255.0
 default-router 192.168.3.1
 dns-server 192.168.3.1
exit


🔁 Routing Configuration (RIPv2)
MAIN ROUTER
router rip
 version 2
 network 192.168.1.0
 network 192.168.2.0
 network 192.168.3.0
 network 192.168.4.0
 network 192.168.5.0
 network 192.168.6.0
 network 192.168.7.0
 network 192.168.8.0
exit


