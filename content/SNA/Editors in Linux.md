---
aliases:
- VIM
- Nano
draft: false
tags:
- SNA
- Linux
---
## Editors in Linux
Editors are programs that let you create & modify text files, important for writing code, scripts or configuration files. Linux **settings** are literally stored in text files. Two of the most common editors are VIM and Nano.
### VIM
- Vim Modes
	- **Command** Mode
	  keystrokes issue commands to Vim
	- **Insert** Mode
	  keystrokes place text in text file
	- **Execute** Mode
	  keystrokes issue additional commands to Vim
- Change modes
	- `esc` takes you to Command mode
	- `i` from Command to Insert (many other keys also do this)
	- `:`from Command to Execute
### Nano
- simpler than [[#VIM]] (no modes)
- Enter text directly in files
- `cntrl` metakey manages the file:
	- `cntrl + o` saves the file
	- `cntrl + x` exits the file and closes the editor