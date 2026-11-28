---
aliases:
- Switch Virtual Interface (SVI)
- Auto-MDIX
draft: false
tags:
- networking
---

## Configure a Switch with Initial Settings
### Switch Boot Sequence
The operating system for Cisco devices is the **Cisco IOS (Internetworking Operating System)**. 

Once powered on, a Cisco switch goes through a 5-step boot sequence:
1. **POST** (Power-On Self Test) checks the CPU subsystem, testing the *CPU*, *DRAM* and the *flash file system* part of the flash device.
2. **Boot Loader Software**, a small program also stored in ROM, runs immediately after POST successfully completes.
3. The CPU performs **Low-level CPU Initialisation**. 
   It initialises the CPU *registers*, which control where the physical memory is mapped, the quantity of memory and its speed.
4. The bootloader initialises the **flash file system** on the system board.
5. Boot loader locates and loads a **default IOS operating system software image** into memory and hands over control of the switch to it.

THe boot sequence for a router is ==basically the same== as well.

>[!Info] Stored in ROM
>POST and Boot Loader Software both are programs stored in the ROM (read-only memory).
### Switch Management Access
For **remote management access** (accessing the switch from a different physical location), the switch must be configured with:
- an ip address
- a subnet mask
- a default gateway

![[Switch Management Access.png|300]]

In the figure, the **switch virtual interface (SVI)** should be assigned an IP address. Note that SVI is a *virtual* interface rather than a physical one. A console cable （aka rollover cable)  is attached to a PC so the switch can be initially configured.
### Configure Switch Virtual Interface (SVI)
> [!Warning] Don't Use Default VLAN1
> By *default*, the switch is configured to have its management controlled through **VLAN 1**. All ports are assigned to VLAN 1 by default. For security purposes, it is considered a best practice to use a ==VLAN other than VLAN 1== for the **management VLAN**. There's no real upper limit on the VLAN number.
#### Step 1: Configure the Management Interface
From the VLAN interface configuration mode, apply an **IPv4 address** and **subnet mask** to the management SVI, using the commands below.

> [!Info]
>  The SVI for VLAN 99 won't appear as *up/up* until VLAN 99 is created and there is a **device connected** to a switch port associated with VLAN 99.

>[!Warning] IPv6 Configuration
>To configure ipv6, first run `sdm prefer dual-ipv4-and-ipv6 default` and `reload`. Otherwise, ipv6 addresses are invalid commands.



| Task                                          | Commands                                               |
| --------------------------------------------- | ------------------------------------------------------ |
| Enter global config mode                      | `S1# configure terminal`                               |
| Enter interface config mode for the SVI       | `S1(config)# interface vlan 99`                        |
| Configure management interface IPv4 address   | `S1(config-if)# ip address 172.17.99.11 255.255.255.0` |
| Configure management interface IPv6 address   | `S1(config-if)# ipv6 address 2001:db8:acad:99::1/64`   |
| Enable the management interface               | `S1(config-if)# no shutdown`                           |
| Return to the privileged EXEC mode            | `S1(config-if)# end`                                   |
| Save the running config to the startup config | `S1(config-if)# copy running-config startup-config`    |
#### Step 2: Configure the Default Gateway
The switch should be configured with a **default gateway** if it will be managed *remotely* from networks that aren't directly connected.

Since it receive its default gateway information from a *router advertisement (RA) message*, the switch does not require an **IPv6** default gateway.

| Task                                          | Commands                                     |
| --------------------------------------------- | -------------------------------------------- |
| Enter global config mode                      | `S1# configure terminal`                     |
| Configure the default gateway for the switch  | `S1(config)# ip default-gateway 172.17.99.1` |
| Return to privileged EXEC mode                | `S1(config-if)# end`                         |
| Save the running config to the startup config | `S1# copy running-config startup-config`     |
#### Step 3: Verify Switch Port Configuration
Here, commands `show ip interface brief` and `show ipv6 interface brief` help determine the status of both physical and virtual interfaces.

> [!Info]
> The IP address for the SVI is *only* for remote management access; it cannot route Layer 3 packets.

![[Verify SVI Management Interface show ip interface brief.png|600]]
## Configure Switch Ports
### Duplex Connection
**Full-duplex**, aka bidrectional communication, is when the connection is able to transmit & receive data *simultaneously*, increasing bandwidth efficiency. It requires microsegmentation.

A **microsegmented LAN** is created when a switch port has *only* one device connected and is operating in full-duplex mode. There is no collision domain associated with a switch port operating in full-duplex mode.

**Half-duplex**, like walkie-talkies, can only transmit data in one direction at a time, often resulting in collisions.

**Gigabit Ethernet** and **10 Gb NICs** require full-duplex connections to operate. In full-duplex mode, the **collision detection circuit** on the NIC is *disabled*. Full-duplex offers 100% efficiency in both directions (transmitting and receiving). 

>[!Info] Speed Mismatch
>When there's a mismatch in speed between two switches, like one operating in 100Mbps while the other's 1000Mbps, The overall speed will follow the ==lower one==, so 100Mbps in this case.
>
>Think of it as trying to talk to your friend in the next car over while driving; you can only do so comfortably if both of you are side-by-side at similar speeds.
### Configure Switch Ports at the Physical Layer
Switch ports can be manually configured with specific **duplex** and **speed** settings.

- default settings for switch ports on Cisco Catalyst 2960 and 3560 is **auto**
- 10/100/1000 ports operate *only* in full-duplex at 1000 Mbps
  (operates in half or full when set to 10 or 100 Mbps)
- Best practice when connecting to known devices is to manually set these settings; **Autonegotiation** is useful when the speed and duplex settings of the device connecting to the port are *unknown* or may change.

>[!Warning]
>Mismatched Settings for the duplex mode and speed of the switch ports can cause connectivity issues. Autonegotiation failure creates mismatched settings.

>[!Info]
>All fiber optic ports, like the 1000BASE-SX ports, operate only at **one preset speed** and are **always full-duplex**.

| Task                                      | Commands                                 |
| ----------------------------------------- | ---------------------------------------- |
| Enter global config mode                  | `S1# configure terminal`                 |
| Enter interface config mode for the SVI   | `S1(config)# interface FastEthernet 0/1` |
| Configure the interface duplex            | `S1(config-if)# duplex-full`             |
| Configure the interface speed             | `S1(config-if)# speed 100`               |
| Return to privileged EXEC mode            | `S1(config-if)# end`                     |
| Save the running config to startup config | `S1# copy running-config startup-config` |
### Automatic Medium-Dependent Interface Crossover (Auto-MDIX)
Interface *automatically* detects the required **cable connection type** (straight-through or crossover) and configures the connection appropriately, so it ==doesn't matter which type you use==.

Auto-mdix `mdix auto` command (though it's enabled by default). When using auto-MDIX on an interface, the interface speed and duplex must be set to *auto* so that the feature operates correctly. 

>[!info]
>Auto-mdix is unavailable on older devices, like *Catalyst 2950* and *Catalyst 3550* switches.
#### Cable Connection Type
When connecting to switches without the auto-MDIX feature:
- **Straight-through** cables must be used to connect to devices such as *servers*, *workstations*, or *routers*. 
- **Crossover** cables must be used to connect to other *switches* or *repeaters*.
### Switch Verification Commands

| Task                                             | Commands                                                                                 |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| Display interface status and configuration.      | `S1# show interfaces [interface-id]`                                                     |
| Display current startup configuration.           | `S1# show startup-config`                                                                |
| Display current running configuration.           | `S1# show running-config`                                                                |
| Display information about the flash file system. | `S1# show flash`                                                                         |
| Display system hardware & software status.       | `S1# show version`                                                                       |
| Display history of commands entered.             | `S1# show history`                                                                       |
| Display IP information about an interface.       | `S1# show ip interface [interface-id]`<br>OR<br>`S1# show ipv6 interface [interface-id]` |
| Display the MAC address table.                   | `S1# show mac-address-table`<br>OR<br>`S1# show mac address-table`                       |
> [!Example] show running-config
>![[show running-config Switch Port Verification.png|400]]
>- Fast Ethernet 0/18 interface configured with the management VLAN 99
>- VLAN 99 configured with an IPv4 address of 172.17.99.11 255.255.255.0
>  Default gateway set to 172.17.99.1

> [!Example] show interfaces
> ![[show interfaces Switch Port Verification.png]]
> 
> The first line shows that FastEthernet0/18 interface is up, meaning it's **operational**.
> The duplex is full and the speed is 100 Mbps. Further down, counters and statistics are shown.