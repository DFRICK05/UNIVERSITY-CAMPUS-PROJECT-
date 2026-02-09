# UNIVERSITY-CAMPUS-PROJECT-

TOPOLOGI
<img width="3198" height="982" alt="Image" src="https://github.com/user-attachments/assets/3e8b7fe5-67cf-435e-b892-e11ff47f1bca" />


QUESTION
# ENGLISH VERSION

Coursework Brief
Albion University is a large university which has two campuses situated 20 miles apart. The university's students and staff are distributed in 4 faculties; these include the faculties of Health and Sciences; Business; Engineering/Computing and Art/Design. Each member of staff has a PC and students have access to PCs in the labs.

Requirements:
a. Create a network topology with the main components to support the following:
Main campus:
- Building A: Administrative staff in the departments of management, HR and finance. The admin staff PCs are distributed in the building offices and it is expected that they will share some networking equipment (Hint: use of VLANs is expected here). The Faculty of Business is also situated in this building.
- Building B: Faculty of Engineering and Computing and Faculty of Art and Design.
- Building C: Students' labs and IT department. The IT department hosts the University Web server and other servers.
There is also an email server hosted externally on the cloud.
- Smaller campus:
Faculty of Health and Sciences (staff and students' labs are situated on separate floors).

b. You will be expected to configure the core devices and few end devices to provide end-to-end connectivity and access to the internal servers and the external server.
- Each department/faculty is expected to be on its own separate IP network.
- The switches should be configured with appropriate VLANs and security settings.
- RIPv2 will be used to provide routing for the routers in the internal network and static routing for the external server.
- The devices in building A will be expected to acquire dynamic IP addresses from a router-based DHCP server.



# Versi Bahasa Indonesia
Ringkasan Tugas Kuliah
Universitas Albion adalah universitas besar yang memiliki dua kampus dengan jarak 20 mil. Mahasiswa dan staf universitas tersebar di 4 fakultas; mencakup fakultas Kesehatan dan Sains; Bisnis; Teknik/Komputasi dan Seni/Desain. Setiap anggota staf memiliki PC dan mahasiswa memiliki akses ke PC di laboratorium.

Persyaratan:
a. Buatlah topologi jaringan dengan komponen utama untuk mendukung hal-hal berikut:
Kampus Utama:
- Gedung A: Staf administrasi di departemen manajemen, HRD, dan keuangan. PC staf admin tersebar di kantor-kantor gedung dan diharapkan mereka akan berbagi beberapa perangkat jaringan (Petunjuk: penggunaan VLAN diharapkan di sini). Fakultas Bisnis juga terletak di gedung ini.
- Gedung B: Fakultas Teknik dan Komputasi serta Fakultas Seni dan Desain.
- Gedung C: Laboratorium mahasiswa dan departemen IT. Departemen IT meng-host server Web Universitas dan server lainnya.
Terdapat juga server email yang di-host secara eksternal di cloud.
- Kampus Kecil:
Fakultas Kesehatan dan Sains (staf dan lab mahasiswa terletak di lantai yang berbeda).

b. Anda diharapkan untuk mengonfigurasi perangkat inti dan beberapa perangkat akhir untuk menyediakan konektivitas ujung-ke-ujung (end-to-end) serta akses ke server internal dan server eksternal.
- Setiap departemen/fakultas diharapkan berada pada jaringan IP terpisah masing-masing.
- Switch harus dikonfigurasi dengan VLAN dan pengaturan keamanan yang sesuai.
- RIPv2 akan digunakan untuk menyediakan perutean (routing) bagi router di jaringan internal dan routing statis untuk server eksternal.
- Perangkat di gedung A diharapkan mendapatkan alamat IP dinamis dari server DHCP berbasis router.

DEVICE 
1. ROUTER 2911 3 units
2. SWITCH L3 (Multilayer Switch) 1 unit
3. Switch L2 10 units
4. END DEVICE
5. SERVER 3 units

CABLE
SERIAL DCE
CROSS OVER
COPPER STRAIGHT


# CONFIGURE DEVICE 
SWITCH ADMIN
enable
configure terminal
vlan 10
name ADMIN
interface range fa0/1-24
switch mode access
switch access vlan 10

SWITCH HR
enable
configure terminal
vlan 20
name HR
interface range fa0/1-24
switch mode access
switch access vlan 20

SWITCH FINANCE
enable
configure terminal
vlan 30
name FINANCE
interface range fa0/1-24
switch mode access
switch access vlan 30

SWITCH BUSINESS
enable
configure terminal
vlan 40
name BUSINNES
interface range fa0/1-24
switch mode access
switch access vlan 40

SWITCH E&C
enable
configure terminal
vlan 50
name E&C
interface range fa0/1-24
switch mode access
switch access vlan 50

SWITCH A&D
enable
configure terminal
vlan 60
name A&D
interface range fa0/1-24
switch mode access
switch access vlan 60

SWITCH STUD_LAB
enable
configure terminal
vlan 70
name STUDLAB
interface range fa0/1-24
switch mode access
switch access vlan 70

SWITCH IT_LAB
enable
configure terminal
vlan 80
name ITLAB
interface range fa0/1-24
switch mode access
switch access vlan 80

# CONFIGURE 
MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/2
switch mode access 
sw access vlan 10
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/3
switch mode access 
sw access vlan 20
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/4
switch mode access 
sw access vlan 30
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/5
switch mode access 
sw access vlan 40
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/6
switch mode access 
sw access vlan 50
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/7
switch mode access 
sw access vlan 60
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/8
switch mode access 
sw access vlan 70
exit

MULTILAYER SWITCH L3
enable
configure terminal
interface gigabitEthernet1/0/9
switch mode access 
sw access vlan 80
exit

interface gigabitEthernet10/1
swithc mode trunk
exit
do write


# CONFIGURE ROUTER 2911

ROUTER MAIN
enable
configure terminal
interface gig0/0
no sh
exit

interface serial0/1/0
no sh
clock rate 64000
ex

interface serial0/1/1
no sh
clock rate 64000
ex

Router(config)#int gig0/0.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip address 192.168.1.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 192.168.2.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.30
Router(config-subif)#encapsulation dot1Q 30
Router(config-subif)#ip address 192.168.3.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.40
Router(config-subif)#encapsulation dot1Q 40
Router(config-subif)#ip address 192.168.4.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.50
Router(config-subif)#encapsulation dot1Q 50
Router(config-subif)#ip address 192.168.5.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.60
Router(config-subif)#encapsulation dot1Q 60
Router(config-subif)#ip address 192.168.6.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.70
Router(config-subif)#encapsulation dot1Q 70
Router(config-subif)#ip address 192.168.7.1 255.255.255.0
Router(config-subif)#ex

Router(config)#int gig0/0.80
Router(config-subif)#encapsulation dot1Q 80
Router(config-subif)#ip address 192.168.8.1 255.255.255.0
Router(config-subif)#ex


# DHCP POOL ROUTER MAIN
Router(config)#service dhcp

Router(config)#ip dhcp pool ADMIN
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.1.1 
Router(dhcp-config)#dns-server 192.168.1.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool HR
Router(dhcp-config)#network 192.168.2.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.2.1 
Router(dhcp-config)#dns-server 192.168.2.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool FINANCE
Router(dhcp-config)#network 192.168.3.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.3.1
Router(dhcp-config)#dns-server 192.168.3.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool BUSINESS
Router(dhcp-config)#network 192.168.4.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.4.1
Router(dhcp-config)#dns-server 192.168.4.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool E&C
Router(dhcp-config)#network 192.168.5.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.5.1
Router(dhcp-config)#dns-server 192.168.5.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool A&D
Router(dhcp-config)#network 192.168.6.0 255.255.255.0
Router(dhcp-config)#dns-server 192.168.6.1
Router(dhcp-config)#default-router 192.168.6.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool STUDLAB
Router(dhcp-config)#network 192.168.7.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.7.1 
Router(dhcp-config)#dns-server 192.168.7.1
Router(dhcp-config)#ex

Router(config)#ip dhcp pool ITLAB
Router(dhcp-config)#network 192.168.8.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.8.1
Router(dhcp-config)#dns-server 192.168.8.1

Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 10.10.10.0
Router(config-router)#network 10.10.10.4
Router(config-router)#network 192.168.1.0
Router(config-router)#network 192.168.2.0
Router(config-router)#network 192.168.3.0
Router(config-router)#network 192.168.4.0
Router(config-router)#network 192.168.5.0
Router(config-router)#network 192.168.6.0
Router(config-router)#network 192.168.7.0
Router(config-router)#network 192.168.8.0
Router(config-router)#ex
Router(config)#do wr


# ROUTER CLOUD
enable
configure terminal 
interface serial0/1/0
no sh

Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 20.0.0.0
Router(config-router)#network 10.10.10.4
Router(config-router)#ex
Router(config)#do wr

# ROUTER BRANCH CAMPUS 
enable
configure terminal
int serial0/1/0
no sh
ex

int gig0/0.90
encapsulation dot1q 90
ip address 192.168.9.1 255.255.255.0
ex

int gig0/0.100
encapsulation dot1q 100
ip address 192.168.10.1 255.255.255.0
ex

service dhcp
ip dhcp pool Staff
netowrk 192.168.9.0 255.255.255.0
default-router 192.168.9.1
dns-server 192.168.9.1

ip dhcp pool STUDLB
netowrk 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.10.1
ex
do write

Router(config)#router rip 
Router(config-router)#version 2
Router(config-router)#network 192.168.9.0
Router(config-router)#network 192.168.10.0
Router(config-router)#network 10.10.10.0
Router(config-router)#ex
Router(config)#
Router(config)#do wr


# CONFIGURE MULTILAYER SWITCH L3
int gigabitEthernet1/0/1
switch mode trunk
ex

int gigabitEthernet1/0/2
switch mode access
sw access vlan 90
ex

int gigabitEthernet1/0/3
switch mode access
sw access vlan 100
ex
do wr

# CONFIGURE SWITCH L2
enable 
configure terminal
int range fa0/1-24
sw mode access 
sw access vlan 90
ex


int range fa0/1-24
sw mode access
sw access vlan 100
ex

do wr






then you do it on all PCs to the desktop, select IP configuration then switch to DHCP

<img width="930" height="362" alt="Image" src="https://github.com/user-attachments/assets/c3cd87a4-9574-42b6-b374-90b5eaeeaf1b" />

<img width="739" height="625" alt="Image" src="https://github.com/user-attachments/assets/c4ac070c-48a0-4aa0-b620-f6b9d1098468" />

