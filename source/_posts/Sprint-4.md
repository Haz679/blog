---
title: Sprint 4
---

# Reverse Engineering Guest Speaker
We were fortunate enough to have Ruben from Symantec to give us a workshop on reverse engineering with binary ninja. He directed us to a website that had several challenges that we could attempt, each with increasing difficulty and thus complexity. The hardest part abou these challenges was definitely having no knowledge of reverse engineering whatsoever, so naturally, I had no idea as to what I was looking for. To make matters worse, Binary Ninja wasn't working on my mac due to the limited amount of RAM I have installed so I had to pair up with Pags, one of my colleagues to complete the challenge.

It was very interesting to say the least, especially with how binary ninja worked to display what the cpu instructions looked like. The complexity of how low level information is traversed through the system is something that every tech student should know and understand. It's by far the means to reverse engineering (pun intended) the knowledge that is taught in the subject (at a high level) to gain a deeper understand of how a machine works. Essentially what I mean by that is, a student is taught what functions, methods and libraries are, however are practically oblivious to how the code is looked at in the background. I think you get the gist.

Ruben also mentioned malware analysis in his talk, which definitely struck my attention.

# Hack the Box
Being new to Hack the Box, I was expecting to just create an account, get the invite code and away I go...boy was I wrong.

The /invite/ page is actually a vulnerable login form that needs to be exploited in order to reveal the flag. I was able to get  the help of Jason and Rowan to guide me in the right direction. It went something like this:

1) Me trying XSS and SQLi and immediately getting blocked

![](blocked.png)

2) Jason redirected me to the invite page's source code. In the console tab, there was an image of a skll that seemed interesting. There was also a js method that I found that allowed you to generate the invite code. At this stage, I had to google how to call functions in javascript since my programming knowledge is very limited. I discovered that the console allows the calling of these methods on the browser. Once I called the function, I was given a base64, which is where i used cyberchef to decode:

![](cyberchef.png)

3) The message read that I needed to a POST request to that given url. So I used postman to do so. Once again, I was given yet another base64:

![](postman.png)

![](cyberchef2.png)

3) Once the code was inputted into the invite field...

![](congrats.png)

...and there you have it

I was able to get root on Curling, however since it is currently an active box, writeup is to be announced!!

# Final Expo
On the last Friday, all the Summer Studio students banded together to put on an expo to showcase their work over the 4 weeks. From 12pm to 1pm, we had a pizza lunch before speeches from the head organisers as well as the subject leaders. The expo was located all over Building 11, with each studio having their own room to display their work.

Our setup wasn't as organised as I'd wish, however we managed to impress where we could. Unfortunately, I didn't get the opportunity to present, however I was able to go to a different studio (Neural Networks) to see the progress of other students and of their stuff is cool to say the least. One team was developed an algorithm to identify the percentage of a certain cat you are. Another group developed a scanner to calculate the amount of white blood cells in your bloodstream.

To finish up, it was awesome to see what the other studios have done and I'm escpecially proud of everyone in our studio.  


