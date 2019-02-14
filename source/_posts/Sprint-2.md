---
title: Sprint 2 Mid Week
---

## Ethical hacking on stakeholders

Ethical hacking is the means of penetrating into the network of an organisation for the purpose of exploiting vulnerabilities under the legal consent of the hiring organisation. This in essence provides the organisation with the peace of mind that their network will be less open to outside attackers that would exploit these same vulnerabilities for their own benefit as well as the embarrassment of the victim

The purpose of ethical hacking is to ensure that the assets and data that belong to stakeholders remain secure and out of reach of the prying eyes of the public

Hacking ‘ethically’ requires these so called hackers to act under a code that protects the organisation from any harm 

In a simple example, the code would read like this:

- Understand the characteristics of the of the company
- Determine the sensitivity and confidentiality of the information
- Communicate, be transparent
- Do not violate set limits
- Do not disclose information to third parties

Hence such a code provides peace of mind to the stakeholders themselves that any portion of the company they own or data that the company posesses, such as investments for Superannuation and banking to health records are protected by law.  


### Bibliography
- Panmore Institute. (2019). Ethical Hacking Code of Ethics: Security, Risk & Issues - Panmore Institute. [online] Available at: http://panmore.com/ethical-hacking-code-of-ethics-security-risk-issues [Accessed 12 Feb. 2019].
- Computerhope.com. (2019). What is Ethical Hacking?. [online] Available at: https://www.computerhope.com/jargon/e/ethihack.htm [Accessed 12 Feb. 2019].

## Bug Bounties on stakeholders
Bug bounty allow security teams to earn a sum of money for a bug that is found in an organisation's website. This bounty encourages persistance and hard work in the search, futureproofing the company from future attacks. Such a program can be an issue as bugs may be disclosed to the public on purpose, exposing data and other sensitive information unbenownst to the componay and likewise to their stakeholders.

A bug bounty program will have a scope in place

A scope states the type of the bugs to be found and where the hacker can poke and probe. It will also include a respobsible disclosure statement as well as the reward for finding certain bugs. The responsible disclosure affects both the finders and security teams alike and prevents either party from misconduct such as giving away sensitive information or not acting to improve security when a bug has been found

### Bibliography
- Houston, S. (2019). The Importance of Scope - Bug Bounty Hunter Methodology | Bugcrowd. [online] Bugcrowd. Available at: https://www.bugcrowd.com/the-importance-of-scope-bug-bounty-hunter-methodology/ [Accessed 12 Feb. 2019].
- HackerOne. (2019). Vulnerability Disclosure - Guidelines Process & Programs | HackerOne. [online] Available at: https://www.hackerone.com/disclosure-guidelines [Accessed 12 Feb. 2019].

## Test Web Apps under RDP
Web app hacking requires a plethora of knowldge with regards to how the web works, its protocols, the OSI model and the respective tools that are used to break in. Under a respoonsible disclosure program, the exloits that are unveiled and broken using such tools must not be distributed openly to the public so as to make the information a vector of attack in the future

## Research Task - XSS
The studio was given a lecture by CSEC member Luke Fuehrer. During the lecture he covered the history of web applications throughout the development of the internet. This was alongside the need to provide improved security to such applications as the amount of data that organisations were handling was expanding over time. The security vulnerability that he covered was Cross-site scripting, or XSS for short. This is essentially the exploitation of the javascript that runs in the background of a web application for malicious means on both server-side and client-side operations. He explained the 3 main types of XSS attacks and how they work. One of the take home messages that he wished to implant into his audience was that once you know how to mitigate the attack, as a student you now know the methods with which you can use the execute the attack without detection. It was also mentioned that it's not what you do, but how you do it. It is simply a fallacy to try and know everything, however once you seen a common pattern, you are reminded of a previous exploit from a past learning experience.

We were tasked to research an XSS attack and find a common solution to that type of attack. I managed to find am attack that involved ebay from 2017. This involved redirecting the user to a spoofed site. An attacker would use a PHP script to steal the credentials of the user. These credentials would then be sold off for a cost


# Problem Statement
Company XYZ is currently hosting multiple web apps to run different customer portals. Howwever, a lack of security knowledge means the compny is unable to properly train their staff on the dangers of and threats that surround the web.

To improve our web hacking skills, were given an array of deliberately vulnerable web apps. Of these I chose to explore Web for Pentester and Natas. In the past, I've gone through Bandit, another wargame hosted by Overthewire, the same site that hosts Natas. I figured that my prior experience would help to solve Natas, I seemed to bit off more than I can chew.

Initially going through Natas for the first time, I reached a level that required the use of an HTTP proxy, most notably Burp Suite, which in itself was one the many tools mentioned in Luke's talk. In essence, any level afterwards I had trouble in seeing where to go or what to do. To solve this, I spent time looking at writeups. These are the solutions that have been posted by other users during that attempt to solve the challenges. These helped a lot as it allowed me to put myself in their mindset, empathising the methodolgy. As Luke stated, "it's not what you do, it's how you do it", in that there are multiple ways to traverse the web app.

![burp suite](img/burp.png)
