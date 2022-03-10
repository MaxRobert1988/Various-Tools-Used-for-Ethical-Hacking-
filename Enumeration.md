# Enumeration

## Perform NetBIOS enumeration

### Perform NetBIOS enumeration using Windows command-line utilities
```
nbtstat -a IP
```
Cached Contents of remote computer
```
nbtstat -c
```
To display information about the target such as connection status, shared folder/drive and network information
```
net use
```
	
### Perform NetBIOS enumeration using NetBIOS Enumerator (Windows)


### Perform NetBIOS enumeration using an NSE Script
```
nmap -sV --script nbstat.nse Target
```

## Perform SNMP enumeration

### Perform SNMP enumeration using snmp-check

To check if a port is filtered 
```
nmap -sU Target
```
The snmp-check command enumerates the target machine, listing sensitive information such as System information and User accounts.
```
snmp-check Traget
```
### Perform SNMP enumeration using SoftPerfect Network Scanner (Windows)

* Steps to Follow
	* Options
	* Remote SNMP
	* Mark all/none button to select all the items available for SNMP scanning and close the window.
	* enter an IP range 
	* Start Scan

## Perform LDAP enumeration

### Perform LDAP enumeration using Active Directory Explorer (AD Explorer) (Windows)


## Perform NFS enumeration

### Perform NFS enumeration using RPCScan and SuperEnum

```
cd SuperEnum
echo "Target IP" >> Target.txt
./superEnum
chmod +x superenum
./superenum
Enter Filename
Let it run
```
```
cd RPCScan
python3 rpc-scan.py Target --rpc
```
## Perform DNS enumeration

### Perform DNS enumeration using zone transfer

```
dig ns IP
dig @nameserver target axfr
```
```
nslookup
set querytype=soa
target domain
ls -d nameserver
```

### Perform DNS enumeration using DNSSEC zone walking

```
dnsrecon -h
dnsrecon -d domain -z
```

## Perform RPC, SMB, and FTP enumeration

### Perform RPC and SMB enumeration using NetScanTools Pro

* Manual Tools (all)
	* nix RPC Info
	* Enter Taregt Hostname
	* The result appears, displaying the enumerated Program ID, Version, Protocol, and Port of the target system.

* Manual Tools(all)
	* SMB Scanner
	* Start SMB Scanner
	* Edit Target List
	* Enter IP
	* Add to list
	* Edit share login credentials
	* Enter login credentials
	* Add to list
	* Click Get SMB Versions
	* Right click on any machine 
	* view shares


### Perform RPC, SMB, and FTP enumeration using Nmap

```
nmap -T4 -A Target
```

## Perform enumeration using various enumeration tools

### Enumerate information using Global Network Inventory

* Steps to follow
	* New Audit Wizard
	* Single Address Scan
	* Connect as - Enter Credentials
	* Finish
	* Scan Summary
	* Operating System Tab
	* BIOS Tab
	* NetBIOS Tab
	* User Groups

### Enumerate network resources using Advanced IP Scanner


### Enumerate information from Windows and Samba host using Enum4linux

```
enum4linux
enum4linux -u martin -p apple -n target
```
Enum4linux starts enumerating and displays data such as Target Information, Workgroup/Domain, domain SID (security identifier), and the list of users, along with their respective RIDs (relative identifier),
```
enum4linux -u martin -p apple -U Target
```
OS Information
```
enum4linux -u martin -p apple -o Target
```
enumerate the password policy
```
enum4linux -u martin -p apple -P Target
```
enumerate the target machine’s group policy information
```
enum4linux -u martin -p apple -G Target
```
enumerate the share policy information
```
enum4linux -u martin -p apple -S Target
```
