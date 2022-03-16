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
