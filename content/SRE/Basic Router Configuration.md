---
aliases:
- 
draft: false
tags:
- networking
---
The following initial configuration tasks should always be performed, *regardless* if it you're working with a router or a switch: 
1. Name the device (to distinguish it from other routers).
2. Configure passwords.
3. Configure a banner to provide legal notification of unauthorized access.
4. Save the changes on a router.

![[Router Configure Name and Password.png|500]]
![[Router Configure Legal Banner.png|600]]
### Configure Rotuer Interfaces
A feature that *differs* between routers and switches is the **interface type** supported. 

For example, Layer 2 switches support **LANs**; therefore they have mutiple *FastEthernet* or *Gigabit Ethernet* ports. 

Routers support **LANs and WANs** and thus can interconnect different types of networks and support *many* types of interfaces. 

For example, **G2 ISRs** have one or two integrated *Gigabit Ethernet* interfaces and *High-Speed WAN Interface Card (HWIC)* slots to accommodate other types of network interfaces, including *serial*, *DSL*, and *cable* interfaces.

**Dual Stack Topology**, where a device supports both IPv4 and IPv6, is shown in the router below.
![[Dual Stack Topology.png|500]]
### Interface Availability Conditions
To be available, an interface must be:
- configured with at least one **IP address**
  use `ip-address {ip-address} {subnet-mask}` and `ipv6-address {ip-address} {subnet-mask}`
- **Activated**
  By default, interfaces are inactive (*shutdown*). Enable with the `no shutdown` command. 
  The interface must also be connected to another device (a hub, switch or another router) for the **physical layer** to be active.
- **Description**
  Optionally, the interface could also be configured with a *short description* of up to 240 characters. It is good practice to configure a description on each interface. 
  
  Helpful in **troubleshooting** and in identifying a **third-party** connection & contact information.

![[Configure Router Interface.png|500]]
### IPv4 Loopback Interfaces
- logical interface *internal* to the router
- unassigned to a physical port
- unable to connect to other devices
- software interface that's automatically "up" as long as the router is ==functional==
- useful for **testing & managing** as it ensures at least one interface is always available
  *ex: testing internal routing process, emulating networks behind the router*
- commonly used in lab environments to create **additional interfaces**
  *ex: to simulate more networks for configuration practice & testing*
- IPv4 address for each loopback must be **unique** and unused by any other interface

**TLDR: Loopbacks are fake interfaces used for testing.**

Enable and assign a Loopback using:
``` 
Router(config)# interface loopback {number}
Router(config-if)# ip address {ip-address} {subnet-mask}
```
## Verify Directly Connected Networks
### Interface Verification Commands
Several `show` commands:

| Command                                                         | Description                                                                              |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `show ip interface brief`<br>and<br>`show ipv6 interface brief` | Display a **summary** for all interfaces including IP address and operational status     |
| `show running-config interface {interface-id}`                  | Displays the **commands** applied to the specified interface.                            |
| `show ip route`<br>and <br>`show ipv6 route`                    | Display the contents of the IPv4/IPv6 **routing table** stored in RAM. [^1]              |
| `show interfaces`                                               | Displays interface information and **packet flow count** for all interfaces on a router. |
#### Verify IPv6 Link Local and Multicast Address
![[Interface Verification show ip interface brief.png|700]]

The [[Interface Verification show ip interface brief.png|output]] above shows **two** configured IPv6 addresses per command. 

One is the IPv6 **global unicast address** that was manually entered.
The other, beginning with `FE80`, is the **link-local unicast address** for the interface, which is *automatically* added whenever a global unicast address is assigned.

An IPv6 address is ==required== to have a link-local unicast address, but not required to have a global unicast address.

The command `show ipv6 interface gigabitethernet0/0/0` displays ==all== ipv6 addresses and interface status belonging to that interface. 

So it not only displays the global & link-local unicast addresses, but includes the ==multicast address== assigned to the interface, beginning with the prefix `FF02`.

![[show ipv6 interface gigabitethernet.png]]
#### Verify Routes
![[Pasted image 20261123232226.png]]

The output of the `show ip route` and `show ipv6 route` commands reveal the three directly connected **network entries** and the three local host route interface entries, as shown in the example. 

The **local** host route is for routes on the router that ==owns the IP address==, used to allow the router to process packets destined to that IP. The local host route has an:
- administratative distance of 0
- /32 mask for IPv4
- /128 mask for IPv6

A ‘**C**’ next to a route within the routing table indicates that this is a **directly connected** network. When the router interface is configured with a global unicast address and is in the “up/up” state, the IPv6 prefix and prefix length are added to the IPv6 routing table as a connected route.

The IPv6 **global unicast address** applied to the interface is also installed in the routing table as a *local* route. The local route has a **/128** prefix. Local routes are used by the routing table to efficiently process packets with the ==interface address of the router== as the destination.

[^1]: In Cisco IOS 15, active interfaces should appear in the routing table with two related entries identified by the code ‘**C**’ (Connected) or ‘**L**’ (Local). In previous IOS versions, only a single entry with the code ‘C’ will appear.