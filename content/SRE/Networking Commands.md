---
draft: false
tags:
  - networking
---
## General STuff

| Commands                             | Description                                                                                                                                                                                                      |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `copy running-config startup-config` | Essentially saves all the configurations you made. Without this, all your changes are gone the moment you close.                                                                                                 |
| `enable`                             | Enters privileged-EXEC mode, which starts with the `#` instead of `>`.                                                                                                                                           |
| `enable secret {password}`           | Sets an encrypted, password for privileged mode.                                                                                                                                                                 |
| `login`                              | Asks for password when someone connects. Without it, even if a password is set they won't be asked to sign in.                                                                                                   |
| `config terminal`                    | Enters the global-configuration mode, used to change the device's overall settings or enter specific submodes (interface, routing configuration).<br><br>The CLI will show `S1(config)#` to reflect the changes. |
| `show history`                       | Lists all the previous commands entered in the current session.                                                                                                                                                  |
| `banner motd {message}`              | Sets a message to display on login.                                                                                                                                                                              |
| `hostname {name}`                    | Sets the name for the device.                                                                                                                                                                                    |
## Interfaces and IP Addressing

| Command                                                           | Description                                                                                                           |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `ping {hostname/ system-address}`                                 | Used to diagnose basic network connectivity by sending an echo request packet to an address then waiting for a reply. |
| `interface {interface}`                                           | Only works in global-config, enters interface-configuration mode.                                                     |
| `no shutdown`<br>OR<br>`shutdown`                                 | Turns the interface on or off.                                                                                        |
| `description {text}`                                              | Essentially adds a comment to display for the interface.                                                              |
| `ip address {ipv4 addr}<br>`<br>OR <br>`ipv6 address {ipv6 addr}` | Assigns an ipv4 or ipv6 address.                                                                                      |
| `show ip interface brief`                                         | One-line status and IP of every interface.                                                                            |


