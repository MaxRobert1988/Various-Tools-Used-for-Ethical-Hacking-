# Scanning

## Host Discovery

### 1. Using Nmap
Disable Port Scan and host discovery
```
nmap -sn Target
```
If Host is up and blocking probes
```
nmap -Pn Target
```
ARP Ping Scan
```
nmap -PR Traget
```
UDP Ping Scan
```
nmap -PU Target
```
ECHO Ping Scan
```
nmap -PE target
```
Timestamp ping scan
```
nmap -PP target
```
ICMP Address mask ping scan
```
nmap -PM target
```
TCP SYN scan
```
nmap -PS target
```
TCP ACK Scan
```
nmap -PA target
```
IP Protocol ping scan
```
nmap -PO target
```
List of Hosts that nmap will scan, and attempt DNS Resolution
```
nmap -n -sL Target
```


### 2. Using Angry IP Scanner
IP Range -> Preferences -> Ping method as combined udp and tcp -> display -> alive hosts only -> ok 


## Port and Service Discovery

### 1. Using MegaPing (Windows)
port scanner -> destination address -> start

### 2. Using NetScanToolsPro
manual tools(all) -> ping scanner -> Insert IP Range -> use system default DNS -> start
manual tools(all) -> port scanner -> target ip -> tcp full connect -> scan range of ports

### 3. Using Nmap

```
nmap -sT -v Target
nmap -sS -v Target
nmap -sX -v Target
nmap -sM -v Target
nmap -sA -v Target
nmap -sU -v Target
nmap -sN -v Target
nmap -A -T4 Target
```
Idle/IPID Header Scan 
```
nmap -sI -v Target
```
SCTP INIT Scan
```
nmap -sY -v Target
```
SCTP COOKIE ECHO Scan 
```
nmap -sZ -v Target
```
```
nmap -sV Target
nmap -sC Taregt
nmap --traceroute Target
nmap -O Target
nmap -p- Target
nmap -p specificport Target
nmap -p from-to Target
```

### 4. Using Hping3

```
hping3 -A Target -p port -c packetcount
hping3 -8 0-100 -S Target -V
hping3 -F -P -U Target -p port -c count
hping3 --scan 0-100 -S Target
```
ICMP Scan
```
hping3 -1 Target -p port -c count 
```
Entire Subnet Scan
```
hping3 -1 Targetsubnet --rand-dest -I i/f
```
UDP Scan
```
hping3 -2 Target -p port -c count
```

## Perform OS Discovery

### 1. Based on TTL and TCP Window size

Operating System | Linux | Google linux | FreeBSD | OpenBSD | Windows 95 | Windows 2000 | Windows XP | Windows 98,Vista,7,Server 2008 | iOS Cisco Routers | Solaris | AIX
--- | --- | --- | --- |--- |--- |--- |--- |--- |--- |--- |---
Time to Live | 64 | 64 | 64 | 64 | 32 | 128 | 128 | 128 | 255 | 255 | 64
TCP Window Size | 5840 | 5720 | 65535 | 16384 | 8192 | 16384 | 65535 | 8192 | 4128 | 8760 | 16384

TTL can be seen while pinging a host and capturing the requests on wireshark
### 2. using Nmap NSE Scripts

```
nmap -A Target
nmap -O Target
```
```
nmap --script smb-os-discovery target
```

### 3. Using Unicornscan

I - Immediate mode
```
unicornscan Target -Iv
```

## Scanning Beyond IPS/IDS/Firewall

### 1. using various Evasion Techniques

Split packet into tiny fragments
```
nmap -f target
```
Source porrt manipulation
```
nmap -g 80 target
nmap --souce-port 80 target
```
MTU Maximum Transmission Unit
```
nmap -mtu 8 target
```
Decoy Scan along with random ips
```
nmap -D RND:10 Target
```
### 2. Creating Custom packets using colasoft packet builder

* Check adapter settings in adpater windows -> ok
	* Add in menu bar
	* Delta 0.1 seconds
	* ok
	* Send in menu bar
	* burst mode no delay option select
	* after progress on completed close
	* port in menu bar
	* selected packet
	* save


### 3. Creating Custom packets using Hping3 

```
hping3 target --udp --rand-source --data 500
```
TCP SYN Request
```
hping3 -S Traget -p port -c count
```
```
hping3 target --flood
```
## Network Scanning using Metasploit

```
service postgresql start
msfdb init
service postgresql restart
```
```
msfconsole
db_status
nmap -Pn -sS -A -oX Test Traget/subnet
db_import Test
hosts
services
```
SYN Scan
```
search portscan
use auxiliary/scanner/portscan/syn
```
TCP Scan
```
search portscan
use auxiliary/scanner/portscan/tcp
```
SMB Version scan
```
use auxiliary/scanner/smb/smb_version
```
FTP Version scan
```
use auxiliary/scanner/ftp/ftp_version
```
```
hosts
back
hosts -o Path.csv
```
