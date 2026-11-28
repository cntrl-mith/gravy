---
aliases:
  - pipes
  - redirection
  - File Descriptors
draft: false
tags:
  - SNA
  - Linux
  - Linux_Commands
---
## File Descriptors
- **def:** Numbers that processes use to determine which I/O channels it has to open.
- Each I/O system call (*read*, *write*, etc.) takes a file descriptor that indicates which channel the call should operate on.

| Number | Channel Name | Description     | Default Connection                                           | Usage                |
| ------ | ------------ | --------------- | ------------------------------------------------------------ | -------------------- |
| 0      | stdin        | Standard Input  | Reads input from **Keyboard**                                | Read-only            |
| 1      | stdout       | Standard Output | Sends normal outputs to the **Terminal**                     | Write-only           |
| 2      | stderr       | Standard Error  | Sends error messages to the **Terminal**                     | Write-only           |
| 3+     | *filename*   | Other Files     | None; separate **connections to other files** must be specified. | Read, write, or both |

## Pipes (|)
- **def:** Sends the *output* of one command as the *input* to another command.
- **syntax:** `bash {command1}|{command2}`
- **common use cases:**
	- Chaining multiple commands.
	- Filter data using `grep, awk, sed` etc.
	- Count lines/words by adding ` wc -l` or `wc -w` after a pipe.
- **Example Pipelines:**
	- `ls -l | grep "filename"`
	  List files and filter for ones containing filename.
	- `ps aux | grep "bash"`
	  Lists all processes and filters related to the bash shell.
	- `cat file.txt | sort | uniq`
	  Prints contents of a file, sorts it, then removes duplicate lines.
## Redirection
Redirection is the process of changing how processes accept input or display output.

| Redirection    | Command Syntax                         | Description                                                               |
| -------------- | -------------------------------------- | ------------------------------------------------------------------------- |
| Output         | `> {file}`                             | Redirects outputs to a file, **overwriting** the contents if it exists.   |
| Output         | `>> {file}`                            | Appends outputs to the file *without* overwriting.                        |
| Input          | ` < {file}`                            | Takes input for a command from a file.                                    |
| Error          | `2> {file} `                           | Redirects `stderr` to overwrite the specified file.                       |
| Error          | ` 2>> {file}`                          | Append `stderr` error messages to the specified file.                     |
| Output & Error | `&> {file}`<br>OR<br>`> {file} 2>&1`   | Redirects *both* standard input and error to **overwrite** the same file. |
| Output & Error | `&>> {file}`<br>OR<br>`>> {file} 2>&1` | Redirects *both* standard input and error to **append** to the same file. |
>[!Tip] 2> /dev/null
>The `2> /dev/null` redirects error messages to `/dev/null`, which vanishes any data written to it, to be discarded.

> [!info] Heredoc (<<)
> Short for *here document*, heredoc is a way to provide ==multiline== inputs directly in the terminal, without typing them out one by one or storing separately in a file.
### Order of Redirection
The order of redirection makes a difference.

`> output.log 2>&1` first redirects standard output to `output.log`, *then* redirects standard errors to the same place (which is `output.log`).

`2>&1 > output.log` does it in the **opposite order**; it first redirects standard errors to the default place for standard output (which is the **terminal**, so no change) *then* redirects standard output to `output.log`.

This is why some people preferto use the merging redirection operator `&>` over `> {file} 2>&1`.

That being said, system admins who use other shells prefer to avoid the newer merging redirection operator since it *isn't standardised*.
### REdirection Examples
#### Output Redirection
1. Saves a timestamp to /tmp/saved-timestamp file for later reference.
```
[user@host ~]$ date > /tmp/saved-timestamp
```
2. Copy the last 100 lines from `/var/log/dmesg` to the `/tmp/last-100-boot-messages`.
``` 
[user@host ~]$ tail -n 100 /var/log/dmesg > /tmp/last-100-boot-messages
```
3. Concatenate all 4 step files into one in the `tmp` directory.
``` 
[user@host ~]$ cat step1.sh step2.log step3 step4 > /tmp/all-four-steps-in-one
```
4. List the home directory's hidden and regular file names and save the output to the `my-file-names` file.
``` 
[user@host ~]$ ls -a > my-file-names}
```
5. Appends a line to the existing `many-lines-of-information` file.
```
[user@host ~]$ echo "new line of information" >> /tmp/many-lines-of-information
```
#### Error Redirection
1. Redirects errors from the `find` command to the `/tmp/errors` file while viewing the normal command output on the terminal.
``` 
[user@host ~]$ find /etc -name passwd 2> /tmp/errors
```
2. Save process output to the /tmp/output file and error messages to the /tmp/errors file.
``` 
[user@host ~]$ find /etc -name passwd > /tmp/output 2> /tmp/errors
```
3. Save process output to the /tmp/output file and discard error messages.
```
[user@host ~]$ find /etc -name passwd > /tmp/output 2> /dev/null
```
4. Store output and generated errors together to the /tmp/all-message-output file.
```
[user@host ~]$ find /etc -name passwd &> /tmp/all-message-output
```
5. Append output & generated errors to the `/tmp/all-message-output` file.
``` 
[user@host ~]$ find /etc -name passwd >> /tmp/all-message-output 2>&1
```