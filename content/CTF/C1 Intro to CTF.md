---
tags:
  - CTF
---
## Overview
### Gamification
Applying the characteristics of *game elements* (score, badge, leadership etc.), often to a *non-game* context (like academic learning).
### Capture the Flag (CTF)
-  A [[#Gamification|gamification]] of cybersecurity, often incorporated into training.
- **objective:** Enable learning new skills and sharpen tools learnt in a *hands-on* way.
- **advantages:**
	- builds critical thinking skills
	- shows tenacity and passion to future employers
	- competing with a group shows teamwork
	- an environment that encourages experimenting and failure
- **explore:**
	- Top 10 CTF (Capture The Flag) Websites https://www.youtube.com/watch?app=desktop&v=tlEZgOVDKY8
	- https://ctftime.org/ctf-wtf/: a special kind of information security competition. (lab)
	- https://ctf101.org/: learn about different tools used for each category 
	- https://ctfd.io/whats-a-ctf/: a kind of computer security competition
- **videos:**
	- https://www.youtube.com/watch?v=8ev9ZX9J45A
	- https://www.youtube.com/watch?v=uNV74WOBswQ
## Definition of Terms
- **Cryptography**
	- method of protecting data using codes
	- *crypt* = hidden/vault, *graphy* = writing
- **Web Vulnerabilities**
	- https://owasp.org/www-community/vulnerabilities/  
	- *In CTF:* web security challenges where the user needs to exploit a bug to gain higher-level privilege
	- *common vulnerabilities:*
		- lack of input validation on user input
		- lack of sufficient logging
		- fail-open error handling (changing directories in a server)
		- improperly closing the database connection
- **Reverse Engineering**
	- *In CTF:* process of taking a compiled (machine code, bytecode) program and converting it back to a ==human-readable== form
	- requires high-skill
- **Binary Exploration**
	- broad topic about finding & exploiting a vulnerability in a program to gain control of a *shell* or *modifying the program's functions*
	- given flawed programs to exploit; usually needs to be **reverse-engineered** to be solved
	- *Tools:* Terminal, GNU Debugger (gdb), gef, IDA
- **Forensics** (Computer + Network)
	- Any challenge to examine and process a *hidden* piece of information out of static data files (non-executable files like pictures)
	- https://trailofbits.github.io/ctf/forensics/ 
	- https://cybertalents.com/competitions/digital-forensics-ctf
## CTF Rules
- no flag sharing
- CTF Rules - Ph0wn CTF
- Code of Conduct - Ph0wn CTF
## CTF Resources
For beginners:
- https://tryhackme.com/
- https://picoctf.org/
- Hack The Box: Hacking Training For The Best | Individuals & Companies
- https://ctflearn.com/
- CTF 101
- John Hammond – YouTube
- Recommended Tools for CTF – HU Cybersecurity Center (hucerc.com)
- SKR CTF (Malaysian based)
- CTFtime.org / All about CTF (Capture The Flag) 
## CTF Strategies
- Analysis and Exercises for Engaging Beginners in Online CTF Competitions for Security Education 
- New Approaches to Cybersecurity Education: CTF 101 Elective
# References
- https://community.owasp.org/vulnerabilities/
# Lecturer's Add-Ons
- CTF is a fairly rare module, with APU apparently being the only university to implement it in Malaysia.
- Attempt CTFs every day, do a different type each day (Monday cryptography, Tuesday web vuln etc.)
- Do *only* these categories of CTF for now. Other categories like General Skills, AI and Blockchain are less important for the module and cybersecurity.
- Perform write-ups after solving CTFs, make them short bullet-points. Feel free to do them in other languages.
- 