---
aliases:
  - 
draft: false
tags:
  - SNA
  - Linux
  - Linux_Commands
---
## The Linux Commands

| Commands                      |         Description                                                         |
| ----------------------------- | ---------------------------------------------------------------- |
| `ls`                          | lists directories                                                |
| `pwd`                         | print working directory                                          |
| `cd`                          | navigate through directories                                     |
| `mkdir`                       | create directories                                               |
| `mv`                          | move or rename files                                             |
| `cp`                          | copying files                                                    |
| `rm`                          | remove files                                                     |
| `touch`                       | create new file                                                  |
| `in`                          | create shortcuts to other files                                  |
| `clear`                       | clear the terminal                                               |
| `cat`                         | display the file contents                                        |
| `echo`                        | print the command argument                                       |
| `less`                        | display paged outputs                                            |
| `man`                         | manual pages for a description of what a command does            |
| `uname`                       | get basic info about the OS                                      |
| `whoami`                      | get the active username                                          |
| `tar`                         | extract and compress files                                       |
| `grep`                        | search for a string within an output                             |
| `head`                        | return specified number of lines from the *start* of a file      |
| `tail`                        | return specified number of lines from the *end* of a file        |
| `diff`                        | find the difference between two files                            |
| `cmp`                         | compare two files to see if they're identical                    |
| `comm`                        | combination of `diff` and `cmp`                                  |
| `sort`                        | sort the contents of a file while outputting                     |
| `export`                      | export environmental variables                                   |
| `zip`                         | zip files                                                        |
| `unzip`                       | unzip files                                                      |
| `ssh`                         | Secure Shell command                                             |
| `service`                     | start and stop services                                          |
| `ps`                          | display active processes                                         |
| `kill` and `killall`          | kill active processes via their process ID or name               |
| `df`                          | display disk filesystem information                              |
| `mount`                       | mount file systems                                               |
| `chmod`                       | change file permissions                                          |
| `chown`                       | granting ownership of files or folders                           |
| `ifconfig`                    | display network interfaces and IP addresses                      |
| `traceroute`                  | trace all the network hops to reach destination                  |
| `wget`                        | direct download files from the internet                          |
| `ufw`                         | firewall command                                                 |
| `iptables`                    | base firewall for all other firewall utilities to interface with |
| `apt`, `pacman`, `yum`, `rpm` | package managers depending on distribution                       |
| `sudo`                        | escalate privileges                                              |
| `cal`                         | view a command line calendar                                     |
| `alias`                       | create custom shortcuts for regularly-used commands              |
| `dd`                          | majorly used for creating bootable USB sticks                    |
| `whereis`                     | locate the binary, source, and manual pages of for a command     |
| `whatis`                      | find what a command is used for                                  |
| `top`                         | view active processes and their system usage                     |
| `useradd` and `usermod`       | add a new user or change existing user data                      |
| `passwd`                      | create or update passwords for existing users                    |
### Permission Level

| Command/Term | Description       | Purpose                                                                          | Authentication Method                                                 | User Role                                            |
| ------------ | ----------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ---------------------------------------------------- |
| `su`         | switch user       | Temporarily switches to another user (defaults to root if none specified).       | Requires target user's password.                                      | Temporarily becomes the target user.                 |
| `sudo`       | superuser do      | Runs a single command as another user (usually root).                            | Requires the invoking user's password (configured in `sudoers` file). | Runs specific commands with elevated privileges.     |
| `sudoer`     | sudoer            | A user with permission to run `sudo` commands.                                   | Configured in the `/etc/sudoers` file.                                | Authorised to run commands with elevated privileges. |
| `sudo su`    | sudo to superuser | Combines `sudo` with `su` to to switch to the root user using `sudo` privileges. | Requires the invoking user's password (configured in `sudoers` file). | Temporarily becomes root, using `sudo` privileges.   |
| `root`       | root user         | The administrative superuser account with full access to all commands and files. | Logs in directly as root or uses `su`/ `sudo`.                        | Has unrestricted access to the system.               |