---
aliases:
- Upstream
- Downstream
draft: false
tags:
- SNA
- Linux
---
## Linux Overview
An **operating system** with the following features:

| Feature           | Description                                                       |
| ----------------- | ----------------------------------------------------------------- |
| Open Source       | Anyone can view, change or improve the source code.               |
| Free              | No cost to download and usage for most distributions.             |
| Secure            | Less prone to viruses; strong permission and user control system. |
| Customisable      | Can be tailored for desktops, servers or embedded devices.        |
| Stable            | Often runs for months and years before needing a reboot.          |
| Community Support | Supported by a global community of developers.                    |
| Modularity        | Designed to easily replace or remove components.                  |
### History of Linux
A complete Linux system is developed by **multiple independent development communities** that work cooperatively on individual components. 

In 1991, graduate student **Linus Torvalds** developed a *UNIX-like kernel* that he named Linux, and licensed it as open source software under the GPL. The kernel is the core of the operating system and manages hardware, memory, and the scheduling of running programs. 

The Linux kernel is supplemented with **other open source software** including utilities and programs from the **GNU Project**, a graphical interface from MIT's X Window System. The Linux kernel also includes other open source components, such as the Sendmail mail server and the Apache HTTP web server, to become a complete open source UNIX-like operating system.

A major challenge for Linux users was assembling all these software pieces from many sources. Early Linux developers provided a distribution of ==prebuilt and tested tools== that users could download and install to quickly implement Linux systems.
### Advantages of Linux
Linux (along with Windows) is the predominant OS in **modern data centers**, with uses in *application development*, *cloud computing*, as well as *mobile devices & IoT devices*. 

So Linux skills are generally in high demand.
## Linux Distributions (Distros)
A linux distribution, *distro* for short, is an installable operating system constructed from a **Linux kernel** and that supports user programs and libraries.

Many different distros exist, with differing goals and criterias. They generally share these characteristics:
- a linux kernel and support user-space programs
- small and single-purpose, or include thousands of open source programs
- provide a means to install and update the software and its components
- distribution provider supports the software and participates in the dev community
### Popular Linux Distributions (Distros)

| Distro                          | Use-Case                                              |
| ------------------------------- | ----------------------------------------------------- |
| Ubuntu                          | beginner-friendly, desktop and server use             |
| Debian                          | very stable, used as the base for many other distros  |
| Red Hat Enterprise Linux (RHEL) | enterprise-focused (so it's paid), used in businesses |
| Fedora                          | cutting-edge features, supported by Red Hat           |
| Kali Linux                      | designed for ethical hacking and cybersecurity        |
| Arch Linux                      | advanced users, very customisable                     |
| CentOS/Rocky Linux/ AlmaLinux   | server use, RHEL-compatible                           |
## Linux is Open Source
Linux is [[Open Source|open source]], released under the GNU General Public Licesne (GPL), meaning:
1. Linux can be downloaded and installed for *free*
2. Admins can *study and customise* the OS according to their needs

The name "Linux" stems from its creator, Linux Torvalds. While the term technically refers to *just* the Linux kernel, most people use it to refer to the entire Linux ecosystem (or they call it **GNU/Linux** due to the vital GNU components).[^1]
## Linux Architecture
The [[Kernel|kernel]] acts as a bridge between apps and the hardware. In Linux, the kernel is [[Open Source|open source]] and *modular*.

![[Linux Architecture.png|350]]
![[Linux Operating System Diagram.png|350]]
## Upstream and Downstream in Software Development
### Upstream
The **upstream** is the ==original source== or foundation of a software project. It's where development begins. 

For Red Hat Enterprise Linux (RHEL), the upstream source is **Fedora**, a community-driven Linux distribution sponsored by Red Hat. Developers work on new features, enhancements and bug fixes in Fedora, that serves as testing grounds for future RHEL releases.
### Downstream
The **downstream** refers to ==derivative projects== or distributions that are based on the original source.

In the context of RHEL, **CentOS Stream** is a downstream variant. CentOS receives updates and changes from RHEL *after* they've been tested and stabilised in Fedora. 
## Other Linux Features
- [[Linux File System]]
- [[Linux Commands]]
- [[Editors in Linux]]


[^1]: http://www.gnu.org/