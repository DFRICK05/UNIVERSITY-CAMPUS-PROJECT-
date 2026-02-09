# UNIVERSITY-CAMPUS-PROJECT

## TOPOLOGY
<p align="center">
  <img src="https://github.com/user-attachments/assets/3e8b7fe5-67cf-435e-b892-e11ff47f1bca" width="900">
</p>

---

## QUESTION

### ENGLISH VERSION

**Coursework Brief**

Albion University is a large university which has two campuses situated 20 miles apart.  
The university's students and staff are distributed in 4 faculties:
- Health and Sciences  
- Business  
- Engineering and Computing  
- Art and Design  

Each member of staff has a PC and students have access to PCs in the labs.

#### Requirements
**a. Network Design**
- Main Campus:
  - **Building A**  
    Administrative staff (Management, HR, Finance)  
    Faculty of Business  
    VLANs are required
  - **Building B**  
    Engineering & Computing  
    Art & Design
  - **Building C**  
    Student Labs  
    IT Department  
    Internal Web Server and other servers
  - External Email Server hosted on the Cloud

- Smaller Campus:
  - Faculty of Health & Sciences  
  - Staff and Student Labs on separate floors

**b. Configuration**
- Separate IP network for each department/faculty
- VLAN and security configuration on switches
- RIPv2 for internal routing
- Static routing for external server
- DHCP provided by router for Building A

---

### VERSI BAHASA INDONESIA

Universitas Albion memiliki dua kampus dengan jarak 20 mil.  
Mahasiswa dan staf tersebar di empat fakultas:
- Kesehatan dan Sains  
- Bisnis  
- Teknik dan Komputasi  
- Seni dan Desain  

Setiap staf memiliki PC dan mahasiswa menggunakan PC di laboratorium.

---

## DEVICE
- Router 2911 (3 Units)
- Multilayer Switch L3 (1 Unit)
- Switch L2 (10 Units)
- End Devices (PC)
- Server (3 Units)

---

## CABLE
- Serial DCE
- Copper Straight-Through
- Copper Cross-Over

---

## CONFIGURE DEVICE

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


SWITCH STUD_LAB
enable
configure terminal
vlan 70
 name STUDLAB
interface range fa0/1-24
 switch mode access
 switch access vlan 70
exit


SWITCH IT_LAB
enable
configure terminal
vlan 80
 name ITLAB
interface range fa0/1-24
 switch mode access
 switch access vlan 80
exit


CONFIGURE MULTILAYER SWITCH L3
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

do write


CONFIGURE ROUTER 2911 (MAIN)
enable
configure terminal

interface gig0/0
 no shutdown
exit

interface serial0/1/0
 no shutdown
 clock rate 64000
exit

interface serial0/1/1
 no shutdown
 clock rate 64000
exit


ROUTER-ON-A-STICK
ROUTER MAIN
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


DHCP POOL (ROUTER MAIN)
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

ip dhcp pool BUSINESS
 network 192.168.4.0 255.255.255.0
 default-router 192.168.4.1
 dns-server 192.168.4.1
exit

ip dhcp pool E&C
 network 192.168.5.0 255.255.255.0
 default-router 192.168.5.1
 dns-server 192.168.5.1
exit

ip dhcp pool A&D
 network 192.168.6.0 255.255.255.0
 default-router 192.168.6.1
 dns-server 192.168.6.1
exit

ip dhcp pool STUDLAB
 network 192.168.7.0 255.255.255.0
 default-router 192.168.7.1
 dns-server 192.168.7.1
exit

ip dhcp pool ITLAB
 network 192.168.8.0 255.255.255.0
 default-router 192.168.8.1
 dns-server 192.168.8.1
exit


ROUTING (RIPv2)
ROUTER MAIN
router rip
 version 2
 network 10.10.10.0
 network 10.10.10.4
 network 192.168.1.0
 network 192.168.2.0
 network 192.168.3.0
 network 192.168.4.0
 network 192.168.5.0
 network 192.168.6.0
 network 192.168.7.0
 network 192.168.8.0
exit

do write


```

<img width="930" height="362" alt="Image" src="https://github.com/user-attachments/assets/c3cd87a4-9574-42b6-b374-90b5eaeeaf1b" />





<img width="739" height="625" alt="Image" src="https://github.com/user-attachments/assets/c4ac070c-48a0-4aa0-b620-f6b9d1098468" />
