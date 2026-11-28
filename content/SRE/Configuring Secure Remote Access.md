---
aliases:
  - SSH
  - Telnet
draft: false
tags:
  - networking
---
## Secure Remote Access
Secure remote access is about allowing us safe access to an stuff from a ==remote location==.
## Telnet Operation
- TCP port 23
- **older**, outdated protocol
- uses ==unsecure plaintext transmission== of login authentication (password & username) and the data transmitted between the communicating devices, which threat actors monitoring packets can capture
## SSH Operation
- *secure shell* operation
- TCP port 22
- secure, ==encrypted== management connection to a remote device
### Verify the Switch Supports SSH
On the `show version` command, an IOS filename that has ==“k9”== supports cryptographic (encrypted) features and capabilities, so it can enable SSH. 

Alternatively, `show ip ssh` will be unrecognised if a switch doesn't support SSH.

![[Verify the Switch Supports SSH.png|600]]
### Configure SSH
Before configuring SSH, the switch must be minimally configured with a *unique hostname*, the correct *network connectivity settings*, and SSH support must be verified.

1. **Configure the IP domain**
   Configure the IP domain name of the network using `ip domain-name domain-name` global configuration mode command. 
2. **Generate RSA Key Pairs**
   Generating a key pair automatically enables SSH. Use global config mode command `crypto key generate rsa` to enable the SSH server on the switch and generate an RSA key pair.
3. **Configure User Authentication**
   SSH server can authenticate users *locally* or using an authentication server.
   For local, create a username & password pair using `username username secret password`.
4. **Configure the vty lines**
   Enable SSH on the vty lines using the `transport input ssh` line config mode command. Use the `line vty` global configuration mode command and then the `login local` line configuration mode command to ==require local authentication== for SSH connections from the local username database.
5. **Enable SSH version 2**
   By default, SSH supports both versions, as shown in `show ip ssh` output as supporting version 2. Enable SSH version using `ip ssh version 2`.

> [!Warning] Deleting the RSA Key Pair
To delete the RSA key pair, use the `crypto key zeroize rsa` global configuration mode command. After the RSA key pair is deleted, the SSH server is **automatically disabled**.
### Verify SSH is Operational
On a PC, an **SSH client** such as *PuTTY*, is used to connect to an SSH server. 
For example, assume the following is configured:
- SSH is enabled on switch S1
- Interface VLAN 99 (SVI) with IPv4 address 172.17.99.11 on switch S1
- PC1 with IPv4 address 172.17.99.21

Using a **terminal emulator**, initiate an SSH connection to the SVI VLAN IPv4 address of S1 from PC1.

When connected, the user is prompted for a username and password. After entering the correct combination, the user is connected via SSH to the command line interface (CLI) on the Catalyst 2960 switch.

![[Verify SSH is Operational.png|300]]

To display the **version and configuration data** for SSH on the device that you configured as an SSH server, use the `show ip ssh` command. In the example, SSH version 2 is enabled.

![[show ip ssh.png|600]]