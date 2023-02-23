

# <p align=center><img src=https://i.imgur.com/i9mDarB.png width=40%></p><p align=center><b>TryHackMe Year of the Fox</b></p>

<sub><font size="1">Difficulty level: <font color="red">HARD</font> </font></sub>

<p align=center><img style="border:10px solid black;" src=https://i.imgur.com/nH8xnTw.jpg width=30%></p>

> Note: the host IP in all screenshots is substituted as <b>yotf.thm</b>

## Table of Contents

This

# Recon & Initial Access

Forming a basic SYN port scan using nmap showed 3 open ports:

<kbd>nmap -sS -sV -O yotf.thm</kbd>

<p align=center><img src=https://i.imgur.com/WfvVMZe.png></p>

>- 80 - Apache httpd 2.4.29 web server
>- 139 - NetBIOS for Samba filesharing service
>- 445 - NetBIOS for Samba filesharing service

Attempting to access the web server requires credentials:

<p align=center><img src=https://i.imgur.com/vIRNoBz.png></p>

This leaves the samba service as the only option for further enumeration.

using enum4linux, I got some fruitful results:

<pre><code>enum4linux -a yotf.thm</code></pre>

<p align=center><img src=https://i.imgur.com/cMFdZnX.png><img src=https://i.imgur.com/1ddIaoJ.png></p>

The **yotf** share was discovered as well as the local users **fox**, **nobody**, and **rascal**.

Using the username **fox** is not allowed without a password, and after trying a few common passwords without success I set up a hydra bruteforce in the background while I continued enumerating some other options.

After not getting any success with further Samba enumeration, I wanted to try bruteforcing the authentication for the web server using the usernames I found.

I made a small username list **USERLIST.txt** and set up the hydra bruteforce.