# CTF-Win7
Windows 7 CTF, hosted on TryHackMe.com and Vulnhub

Associated links:
TryHackMe.com: https://tryhackme.com/room/blue
Vulnhub: Coming soon!

CTFs
Win7

Source: DarkStar7471 aka J0n

Description:

--A realistic (at the time of writing) Windows box that is relatively simple in complexity.
Flag(s): Three spread throughout the system in the following locations:

The root of the C drive, meant to represent initial contact with the system and a good sanity check for pen testers.
C:\Windows\System32\config, this is the actual location fo the SAM database
Admin's (Jon's) documents folder, elevated user's and staff documents can be very useful in prolonged engagements.
Notes:

--If using VMware, use NAT. This can be very picky about being on host-only for whatever reason and often times just doesn't work.
How to:

Ifconfig
a. 
2. Nmap
1.
a. 

1. \*Can also use netdiscover
2. -vv : Very verbose
3. -sS : Syn scan
4. --script vuln : Check for vulnerabilities using the nmap scripting engine
b. 
3.
c. 
3.
3. 
4.
4. 
5.
5. 
6.
6. 
7.
7. 
8.
8. 
9.
9. 
10.
10. 
11.
11. 

CTRL + Z

Background after this completes, you may have to reboot if this borks the windows SMB service



This gets a much more powerful meterpreter shell, DOS shells are kinda lame to work in for our current purposes.















CTRL + Z to background this new shell

This should return you to meterpreter

Once in the meterpreter shell, type ps

This will list all processes running on the system. We will use this information to migrate to a higher-privileged process. Just because we are nt authority\system doesn't mean our process is.

Look for a process running as nt authority\system from this list generated

Good candidates here are powershell and cmd or programs such as word that may have been left running on this system

Once a process is found, type migrate PROCESSID, where PROCESSID is the id of the process we are migrating to (left column of the ps table generated previously)

This migration process may fail, migrating processes is only successful realistically about 25% of the time.

Once you control a higher-privileged process, type hashdump

This will display the password hashes stored in the SAM database of the unit

This password can be copied to text file and cracked. The specific one in use at the time of writing is within rockyou.txt
