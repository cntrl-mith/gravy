---
aliases:
  - SUID
  - GUID
  - Sticky Bit
draft: false
tags:
  - SNA
  - Linux
---
## Linux File System
![[Linux File System.png|600]]

| Directory | Description                                                                                                                                                  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/`       | root directory                                                                                                                                               |
| `/bin`    | fundamental binary files                                                                                                                                     |
| `/sbin`   | similar to `/bin` but related to system bootup & repair                                                                                                      |
| `/etc`    | system-wide configuration files, go-to place for system admisn                                                                                               |
| `/home`   | personal space for users                                                                                                                                     |
| `/var`    | variable data, such as databases, logs, emails, print queues                                                                                                 |
| `/usr`    | user-related programs, libraries and files                                                                                                                   |
| `/lib`    | shared library files supporting the binaries in `/bin` and `/sbin`                                                                                           |
| `/opt`    | optional or add-on software packages                                                                                                                         |
| `/tmp`    | temporary files, cleared on system reboot                                                                                                                    |
| `/boot`   | files necessary for booting the system                                                                                                                       |
| `/dev`    | device files for all hardware devices on the system                                                                                                          |
| `/proc`   | doesn't contain files, has system & process information                                                                                                      |
| `/root`   | home directory for root user, not to be confused with `/` or `/home`                                                                                         |
| `/run`    | temporary files related to running processes, created at an early stage of the boot process                                                                  |
| `/srv`    | has data for services provided by the sytem                                                                                                                  |
| `/sys`    | similar to `/proc`, virtual file system providing a unified interface through which the kernel provides info about devices, drivers and some kernel features |
| `/mnt`    | generic mount point for filesystems or devices                                                                                                               |
| `/media`  | generally used by the system as a mount for removable media like CDs, digital cameras, or other media devices                                                |
## File System Ownership and Permissions
- all files have a **individual** and **group** ownership
- 3 access permissions: *read* (r), *write* (w) and *execute* (x)
- *each* of the 3 permissions are assigned to 3 defined **categories of users**: 
	1. **owner**: owner of the file or application
	2. **group**: group that owns the file or application
	3. **others:** all users with access to the system, aka *world*.
- individual owners or members of the group can change permissions
- only the root can change ownership
- permissions for a file can be seen using `ls -l` command

> [!Example]+ `ls -l` Example
> User Ali creates an executable file named **test**, output of `ls -l` would be:
> `rwx rwx r-x 1 Ali student 0 Sep 26 12:25 test`
> 
> The first set represents **owner** access (so the owner can read, write and execute test).
> The second is **group** access, and the last is all **other** users (aka world). (so other users can't write to test).
> 
> - `1` represents the number of **hard links** to the file
> - `Ali` is the owner
> - `student` is the group that owns the file
> - `0` is the file's byte size
> - `Sep 26 12:25` is the last modified time
> - `test` is the file name
>   
>`{u} {g} {o} {hardlinks} {owner} {g owner} {last_modified} {name}`
### Setting File Permissions
There are two ways to set permissions using the `chmod` command:
#### Symbolic Mode
format: `$ chmod {user category}+/-{access permission} {filename}` 
(`+` for adding, `-` for removing permission)

Let's say *testfile* has the permissions `-r--r--r--`.
(the first `-` just means that it's a regular file)

| Command                 | User (u) | Group (g) | other (o) |
| ----------------------- | -------- | --------- | --------- |
| `$ chmod g+x testfile`  | r--      | r-x       | r--       |
| `$ chmod u+wx testfile` | rwx      | r-x       | r--       |
| `$ chmod ug-x testfile` | rw-      | r--       | r--       |
#### Absolute Mode
We use **octal** (base eight) values represented like below:

| Letter | Permission | Value |
| ------ | ---------- | ----- |
| r      | read       | 4     |
| w      | write      | 2     |
| x      | execute    | 1     |
| -      | none       | 0     |
Thus, for each column (user, group or other) you can set values from 0-7.
- `0`= ---
- `1`= --x
- `2`= -w-
- `3`= -wx
- `4`= r--
- `5`= r-x
- `6`= rw-
- `7`= rwx
``` 
$ chmod 755 index.html
$ ls -l index.html
-rwxr-xr-x  1 root  wheel  0 May 24 06:20 index.html

$ chmod 644 index.html
$ ls -l index.html
-rw-r--r--  1 root  wheel  0 May 24 06:20 index.html
```
### Special File Permissions
![[LInux Special Permissions.png|400]]

| Special Bit | Applies to      | Purpose                                           | Symbol        | Octal | Example         |
| ----------- | --------------- | ------------------------------------------------- | ------------- | ----- | --------------- |
| SUID        | Executable File | run with owner's permission                       | s in user x   | 4xxx  | /usr/bin/passwd |
| SGID        | Executable/Dir  | run with group's permission, or keep group in dir | s in group x  | 2xxx  | /shared_folder  |
| Sticky Bit  | Directory       | only file owner can delete their files            | t in others x | 1xxx  | /tmp            |

#### SUID (Set User ID)
SUID means that when the file is executed, it is executed with the same permissions as the **owner** of the file.
#### SGID
When the file is executed, the user executing the file will have the same permission as the group owner of the file. If applied to a directory, all subdirectories and files created within it **inherit the same group ownership**.
#### Sticky Bit
All the files in a directory with sticky bit can only be deleted or renamed by the **file owners** or the **root**.