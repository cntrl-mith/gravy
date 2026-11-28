---
aliases:
- 
draft: false
tags:
- computer-architecture
- SNA
---
## Kernel Definition
- core of the Operating System
- software residing in **memory** telling the CPU what to do
- manages resources *ex: memory, processes, I/O devices*
- interface between computer's hardware and its processes
- accepts user inputs through the [[Shell|shell]]
## KErnel Types
### Monolithic Kernel
In computing, **monolithic** refers to something that is built as a single, unified structure. A monolithic kernels means the entire operating system core (kernel) is built as ==one large program==, handling most functions, like:
- all essential services like memory management, process scheduling, file system management, and device drivers
- runs in a **single address space (kernel mode)** for faster performance
- allows **dynamically-loaded modules**, meaning features can be added or removed (like drivers) without restarting the system
### Microkernels
- only the most *essential* functions (CPU, memory management) run in the kernel
- other services (drivers, file systems) run in the user space instead, making it more stable but slower
- examples are the *Minix* and *QNX*
### Hybrid Kernels
- a mix of both [[#Mono|monolithic]] and [[#Microkernels|micro]]
- some parts run in the kernel, while others (like drivers) run in the user space for **flexibility**
- Windows and MacOS are **hybrid kernels**, and is **closed-source** (not publicly available for modification)