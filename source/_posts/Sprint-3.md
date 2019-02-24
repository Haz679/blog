---
title: Sprint 3
---
# Free-for-all 1 - Monday

Speaking to David and Frank, they seemed to have a solid grounding in the subject. David spoke about traversing the web app that the class was invited to break. There were three main findings as part of his talk:
1) The Rest API is quite open and so through particular links he was able to find a list of user data UNENCRYPTED
2) the source code on the login page shows the user unencrypted
3) invalidating a cookie on the login page reveals the server version. David was able to cross check the common vulnerabilities on Common Vulnerabilites and Exposures (CVE) for that particular version. Frank is working through Natas. This is probably best as it is expected that we reach bandit 30 and natas 15 by the end of today.

# Monday Demo
Darshil was able to generously donate his time to demonstrate the basic process of breaking into a vulnerable machine. He used Pentesting 1, a machine downloadble from vulnhub. Below are my notes on what he did, specific quotations from him and anyone else that made a contribution to the demo.

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

netdiscover -i eth0 -r 10.0.2.0/24
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

Directory enumeration to see invisible directories
dirb <url> <path to wordlist (dictory of common dir names)>
 in this case /usr/share/wordlists/dirb/common.txt
  
  had to mod host.conf
  10.0.2.4 vtsec
  type in vtcsec
  
From the dirb we discovered its a wordpress page - notoriously vulnerable
wpscan is designed to specifically scan wordpress

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




  
  
  
  
# Free-for-all 2
We had no free-for-all on the wednesday due to the fact that the time was taken up by the team from Deloitte (see below for info)

# Free-for-all 3
On the Friday, I had the opportunity to talk to Corey, Cameron, and Brendan. Cameron attemped Kioptrix and utilised the Openfuck exploit to gain root. Unfortunately at the time of writing this I misplaced my meticulously written notes which had everything the guys did but in summation both Brendan and Corey were able to root a machine each. I definite challenge for all of them was getting the vm's to work. 

# Deliverable 1 - John the Ripper

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
        
## Bibiography
Openwall, 2019, John the Ripper's Cracking Modes, viewed 18 February 2019, <https://www.openwall.com/john/doc/MODES.shtml>

Openwall, 2019, John the Ripper password cracker, viewed 18 February 2019, <https://www.openwall.com/john/doc/>

Openwall, 2019, John the Ripper usage examples, viewed 18 Februrary 2019, <https://www.openwall.com/john/doc/EXAMPLES.shtml>

Pentestmonkey, 2019, John the Ripper Hash Formats, viewed 18 February 2019, <http://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats>

Oudy, H, 2017, What is John the Ripper?, viewed 28 February 2019, <https://infosecaddicts.com/john-ripper/>

Bytes over Bombs, 2019, Cracking everyhting with John the Ripper, viewed 18 February, <https://bytesoverbombs.io/cracking-everything-with-john-the-ripper-d434f0f6dc1c>

Wikipedia, 2018, John the Ripper, viewed 18 February 2019, <https://en.wikipedia.org/wiki/John_the_Ripper> 




# Wednesday Industry
On Wednesday, the security team from Deloitte presented to the studio. Below is my personal notes but in summary, they introduced the concept of pentesting, outlined what they do including red teaming as well as the tools and techniques they employ. They also gave us a cool to box to break. This talk satisfied SLO 1 as it provided further insight into system vulnerabbilies and how to exploit them. This was demonstrated through an open hacking session where the studio was given the oppurtunity to break into their box with feedback from the team on progression.

Deloitte
If both vms are on NAT, they should be able to interact

What is Pentesting?
Think like criminals
advide clients on how to imporve security
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

Pentesting vs Red teaming
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

# Friday Deliverable
This was essentially my first big dive in attempting boxes. The skill of enumeration was my first wall and I was dedicated to break it simply by getting into walkthroughs and writeups.

I discovered ippsec, a youtuber whom does walkthroughs for retired hack the box machines. After watching a few, I realised that the enumeration is essentially the same in terms of the tools used things to look for.

![](img/ippsec.png)

I took a shot at raven2 to start off. The inital thought was to read through the walkthrough for raven1 and use that as a guide. However, I decided I'd use the skills that drsh displayed in his demo earlier in the week, as well as the methods from the deloitte team.

![](img/Raven1.png)

![](img/login.png)

![](img/nmap.png)

![](img/netdiscover.png)

![](img/port scan.png)





In going through raven2, i quickly discovered that the network settings for virtualbox weren't set up properly as the services that appeared as part of the nmap scan didn't seem right. So once the settings were fixed, the scan yielded a cheeky http at port 80. 

![](img/yep.png)

![](img/nmap-post-settingschange.png)

![](img/portscan-postchange.png)



By instinct i accessed the webpage and navigated my way through for a textbox or something sinister. 

![](img/webpage.png)


One of the links was a blog, which directed me to a wordpress page. At this point I remembered that drsh used wpscan in his demo. In attempting to run:
```bash
wpscan --url 10.0.2.4/wordpress/ --wp-content-dir wp-content
```
the didn't quite yield anything interesting

![](img/wpscan-command.png)


A quick scan of the raven2 walkthrough revealed that I WAS NOT EVEN CLOSE

I had hit a barrier by choosing one of the services that I didn't quite understand how to attack but just went for it anyway:

![](img/xlmrpc.png)

The webpage indicated that only POST requests were accepted. Me thinking this was going to lead to somewhere, I launched burp and intercepted the request. I stumbled upon a site that boasted loading the response with this:

```bash
<methodCall>
<methodName>wp.getUsersBlogs</methodName>
<params>
<param><value>admin</value></param>
<param><value>pass</value></param>
</params>
</methodCall>
```
In the end, this got me nowhere

reference:
https://medium.com/@the.bilal.rizwan/wordpress-xmlrpc-php-common-vulnerabilites-how-to-exploit-them-d8d3c8600b32 21/2


BUT

I "skimmed" through the walkthrough for clues as to where the flags may be because i was losing patience.
Turns out one of them was right under my nose. One of the results of the wpscan pointed to a directory with a few interesting directories. In the end, you get to a file called flag3.png, which sure enough, is actually the flag, WOO HOO!!


![](img/FLAG3.png)


Performed a nikto scan, saw a raven.local. Similar to what drsh did in his demo, I added raven.local in /etc/hosts and pointed it the target ip.

![](img/nikto.png)

Nikto is a perl-based recon tool used to detect web server vulnerabilities such as misconfigurations and outdated versions. It is by no means safe to use under an IDS as it is quite noisy. It does also return false positives as it doesn't execute the vulnerablities but rather checks to see if the server responds to known vulnerable URL's

https://null-byte.wonderhowto.com/how-to/hack-like-pro-find-vulnerabilities-for-any-website-using-nikto-0151729/ 21/2
https://sectools.org/tool/nikto/ 21/2

![](img/raven-local-vim.png)



A dirb scan reveals the possible directories. I discovered that /vendor/ yields further progress. 

![](img/dirb.png)


One of the sub-directories had a timestamp that was noticable different to the others. Clicking on it, gives me the first flag.

![](img/PATH.png)


![](img/flag1.png)


At this point, I realised that moving forward meant researching more about privelage escalation.

![](img/necro1.png)


![](img/necro1.2.png)

# Research
As recommended by Darshil, I continued to research several walkthroughs primarily from different vulnhub machines and retired Hack-the-Box attempts from Ippsec. The vulnhub machines showed potential as the steps taken were somewhat easy to understand. The HTB challenges on the other hand, in my opinion anyway were a massive jump and so I deterred from those and leaned towards boot2root.

Matrix 1
The collest thing about this one was the matrix style code

![](img/scan0011.jpg)

![](img/scan0012.jpg)


Colon, N, 2018, Matrix 1: A Vulnhub VM Walkthrough, viewed 24 Febraruy 2019, <https://medium.com/@nelsoncoln/matrix-1-a-vulnhub-vm-walkthrough-b8ee5d2b178a>

Unfortunately my time mangement is still something to be desired. For some reason I find myself getting to this trans where I have no idea as what I'm doing simply because I have so sense of urgency or organisation. The best example was working towards this weeks presentation. It took me ages to figure out how to simply organsise the damn thing and it still didn't come out to standard and I'm hoping its enough to pass. In closing, I just have to read more and more, keep my eyes on the prize and don't mess it up., or try my best not to at least.
