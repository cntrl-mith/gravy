---
tags:
  - networking
draft: false
aliases:
  - Broadcast Domain
  - Collision Domain
---
## Switching Domains
### Collision Domains
- part of a network where **packet collisions** can occur
- **collision:** two devices send a packet at the same time, corrupting the packet
- collisions are often in a ==hub== environment, because each port on a hub is on the *same* collision domain.
- By contrast, each port on a bridge, switch or router is in a *separate* collision domain.

![[Collision Domains.png|400]]

#### Switches and Collisions Domains
Switches help eliminate collision domains and reduce congestion. **Full duplex** on a link *eliminates* the collision domains.

One or more devices in **half-duplex** leads to contention for the bandwidth, making collisions possible, *creating* a collision domain.

Most devices, including Cisco and Microsoft use **auto-negotiation** as the default setting for duplex and speed

![[Switches and Collision Domains.png|400]]
### Broadcast Domains
- domain in which a broadcast is forwarded
- contains all devices that can reach each other at the **data link layer** using broadcast
- All ports on a hub or switch are, by *default*, in the **same** broadcast domain.
- All ports on a ==router== are in **different** broadcast domains, and routers don't forward broadcasts from one domain to another.

![[Broadcast Domain.png|600]]
#### Switches and Broadcast Domains
A broadcast domain extends across all **Layer 1 or Layer 2** devices on a LAN.
Only a **layer 3** device (router) will *break* the broadcast domain.

When the layer 2 switch receives the broadcast, it will flood it out *all* interfaces except for the ingress interface. 

Too many broadcasts may cause congestion and poor network performance. Increasing devices at Layer 1 or layer 2 will expand the broadcast domain.
### Alleviated Network Congestion
Switches use the [[Switching Methods#MAC Address Table|MAC Address Table]] and full-duplex to eliminate collisions and avoid congestion.
Features of the switch include:

| Protocol                | Function                                                                                                                |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Fast Port Speeds           | Depending on the model, switches may have up to 100Gbps port speed                                                      |
| Fast Internal Switching | This uses fast internal bus or shared memory to improve performanc                                                      |
| Large Frame Buffers     | Allows for temporary storage while processing large quantities of the fr                                                |
| High Port Density          | Provides many ports for devices to connect to LAN with less cost. Also provides for more traffic with less congestion. with  |
