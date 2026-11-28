---
tags:
  - Networking
---
Essentially a small revision of Intro to Networking.
## Part 1: Create Network Topology
Drag and drop the devices:
- a 1941 router
- two 2960 switches
- two PCs

 Rename them to RTA, SW1 (connected to PC-1), SW2 (connected to PC-2). Lastly, connect with **Copper Straight-Through** cables, following the table:
 

| Device | Port | To Device | Port          |
| ------ | ---- | --------- | ------------- |
|        | G0/0 | SW1       | G0/1          |
| RTA    | G0/1 | SW2       | G0/1          |
| SW1    | F0/1 | PC-1      | Fastethernet0 |
| SW2    | F0/1 | PC-2      | Fastethernet0 |
## Part 2: Connect Devices
Click on the devices to enter the CLI, and input the respective commands:
### RTA (Router)
``` 
en
config t
hostname RTA

interface gig0/0
ip address 10.10.10.1 255.255.255.0
description Connection SW1
no shutdown

interface gig0/1
ip address 10.10.20.1 255.255.255.0
description Connection SW2
no shutdown
```
### SW1
``` 
en
config t
hostname SW1

interface VLAN1
ip address 10.10.10.2 255.255.255.0
no shutdown

exit
ip default-gateway 10.10.10.1
```
### SW2
```
en 
config t
hostname SW2

int VLAN1
ip address 10.10.10.2 255.255.255.0
no shutdown

exit
ip default-gateway 10.10.20.1
```
### PC1
Click on PC-1, then click on IP Configuration.
- IPv4 Address `10.10.10.3`
- Subnet Mask `255.255.255.0`
- Default Gateway `10.10.10.1`
### PC2
- IPv4 Address `10.10.20.3`
- Subnet Mask `255.255.255.0`
- Default Gateway `10.10.20.1`
### Glossary of Commands
In case you've forgotten, I'm including the meanings of the commands:
- `interface {interface}` 
  Starts configuring the specified interface.
- `ip address {ip address} {subnet mask}` 
  Sets an IPv4 address and subnet mask for the interface.
- `description`
  Acts like a **comment** in coding, displays when you enter the interface in the future
- `no shutdown`
  Turns the interface on, so it shows "up".
## Part 3: Configure Devices
Now we're setting the passwords.
### Router
```
en 
conf t
enable secret Ciscoenpa55

line console 0
password Ciscolinepa55
login
exit

line vty 0 15
password Ciscolinepa55
login
exit

banner motd "Do not enter, we are watching you"
exit

copy run start
(just press enter here when they ask for filename)
```
### SW1
``` 
en
conf t
enable secret Ciscoenpa55

line console 0
password Ciscolinepa55
login
exit

line vty 0 15
password Ciscolinepa55
login
exit
exit

copy run start
```
### SW2
```
en
conf t
enable secret Ciscoenpa55

line console 0
password Ciscolinepa55
login
exit

line vty 0 15
password Ciscolinepa55
login
exit
exit

copy run start
```

At this point, you should see the completion is 100%. If it's not, you fucked up.
### Glossary of Commands
- `enable secret {password}`
  Sets a password for Privileged Mode, aka when you type `enable`.
- `line vty {line number} {ending line number}`
  These are for configuring **Virtual Terminal Lines**, which we use when connecting remote through telnet or SSH.
- `line console 0`
  Configures the line for the **console port**, which is the *local* terminal.