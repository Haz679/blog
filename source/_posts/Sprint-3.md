---
title: Sprint 3
---
# FFA 1 - Monday

Speaking to David and Frank, they seemed to have a solid grounding in the subject. David spoke about traversing the web app that the class was invited to break. There were three main findings as part of his talk:
1) The Rest API is quite open and so through particular links he was able to find a list of user data UNENCRYPTED
2) the source code on the login page shows the user unencrypted
3) invalidating a cookie on the login page reveals the server version. David was able to cross check the common vulnerabilities on Common Vulnerabilites and Exposures (CVE) for that particular version. Frank is working through Natas. This is probably best as it is expected that we reach bandit 30 and natas 15 by the end of today.

# Monday Demo
"You cant hack what you cant see" - Darsh
"enumerate, enumerate, enumaerate" - drsh
There are many tools to breaj the machine
vuln will give you an ova, import to virtual box
setup NAT network

Attacker - 10.0.2.15
Box - 10.0.2.4

Assuming we are in the network and cant get past login
From attackers machine:
NMAP - ip addr
find ip

Enumerate subnet and find ip of victim:
nmap -sP 10.0.2.0/24 (ping scan)
        <subnet>
  
  ping ip to validate

to enumerate:
netdiscover - needs device and range

netdiscover -i etho0 -r 10.0.2.0/24
            <interface> <range>
  
to find open ports:
nmap 10.0.2.4 - not always recommended as the default script may be too noisy or not always work

nmap -sv - enumerates all the versions, e.g. which version of ftp

searchsploit proftpd 1.3.3 - shows expoits for given protocol version, in this case proftpd 1.3.3
Drsh then when to exploit-db.com and searched for proftpd1.3.3c
what was revealed was metaploit (backdoor) and RCE (compromised source backdoor)
created new directory to load directory 
cd Documents/
mkdir

used wget to load exploits

msfconsole (metasploit framework console)
Drsh doesnt recommend to use metasploit to start out - ITS TOO EASY - Jason
By googling the exploit, drsh was able to find - aldeid - wiki page
GOAL:reverse tunnel to execute commands as root

to check if root:
id;

whoami;


Breaking http:
typed in ip to browser
searchsploit httpd 2.4.18
NO RESULTS

try curl:
curl 10.0.2.4
shows cource of webpage

Directory enumaeration to see invisible directories
dirb <url> <path to wordlist (dictory of common dir names)>
 in this case /usr/share/wordlists/dirb/common.txt
  
  had to mod host.conf
  10.0.2.4 vtsec
  type in vtcsec
  
From the dirb we discovered its a wordpress page - notoriously vulnerable
wpscan is deesigned to specifically scan wordpress

Discovered user is admin admin

Drsh went for a reverse shell
found a cheat sheet through pentestmonkey

netcat
nc -nlvp 10.0.2.4 1234
-l listener
-p port number
The listener must be up first before the script can be executed


change 404 page to includea PHP reverse shell
since we're admin, the 404 page can be changed tthrough the webpage
point ip to 10.0.2.15 machine
also point to transmit tp port 1234
why?
The server needs to poin to the attacker
why is ther server trying to connect to the attacker?

The reverse shell is  trying to  create a connection without having a direct way in


upgrade shell - ropnop.com
not necessary but prettier

to check if possible to escalate to root
look at psswd and shadow
use hashcat or John the Ripper to brute force

tmux - terminal splitter




  
  
  
  
# Scrum 2

# Scrum 3

Deliverable 1

Deliverable 2

Deliverable 3
