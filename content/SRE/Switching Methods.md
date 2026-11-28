---
tags:
  - networking
draft: false
aliases:
  - egress
  - ingress
  - Store and Forward
  - Cut-Through
  - MAC Address Table
  - Learn and Forward
---
# Frame Forwarding
## Switching in Networking
Two terms are associated with frames entering or leaving an interface:
- **Ingress**: entering the interface
- **Egress**: exiting the interface

A switch *forwards* based on the ingress interface and the destination MAC address.
A switch uses its [[#MAC Address Table]] to make forwarding decisions. 

> [!Info]
> A switch will never allow traffic to be forwarded out the **same** interface it received the traffic.
### MAC Address Table
A switch will use the *destination* MAC address to determine the *egress* interface, that is, which interface to exit out of. But before making this decision, it must learn what **interface** the destination is located. 

Thus, a switch builds a MAC address table, also known as a **Content Addressable Memory (CAM)** table, by recording the:
- *source* MAC address
- the ==port== it was received
### Switch Learn and Forward Method
1. **Learn**
	- examines *source* address
	- if in table, resets the timeout settings back to 5 minutes
	- if not in table, add the source MAC
2. **Forward**
	- examines *destination* address
	- if in table, forwarded out the specified port
	- if not in table, flooded out all interfaces *expect* the one it was received
## Switch Forwarding Methods
Switches use software on **application-specific-integrated circuits (ASICS)** to make very quick decisions.

A switch uses one of two methods to make forwarding decisions after it receives a frame:
- [[#Store-and-Forward Switching]]
- [[#Cut-through Switching]]
### Store-and-Forward Switching
- Receives the entire frame and ensures the frame is valid.
- Cisco’s *preferred* switching method
- **Error Checking**
  Checks the **Frame Check Sequence (FCS)** for CRC errors. Bad frames will be discarded.
- **Buffering**
  The ingress interface buffers the frame while it checks the FCS. 
  This also allows the switch to ==adjust== to a potential difference in speeds between the ingress and egress ports.

![[Store-and-Forward Switching.png|600]]
### Cut-through Switching
- Forwards the frame *immediately* after determining the destination MAC address of an incoming frame and the egress port.
- **Fragment (Frag) Free method**
  Checks the destination and ensures the frame is at least *64* Bytes. This will eliminate runts.
- appropriate for switches that need ==<10 microseconds latency==
- doesn't check FCS, can propagate errors, which may lead to bandwidth issues if too many errors
- can't support ports with **differing speeds** going from ingress to egress

![[Cut-through Switching.png|600]]
