# Sniffing

## Perform active sniffing

### Perform MAC flooding using macof

```
macof -i eth0 -n 10
```
-i: specifies the interface and -n: specifies the number of packets to be sent (here, 10).
```
macof -i eth0 -d targetip
```

### Perform a DHCP starvation attack using Yersinia

```
yersinia -I
	q to exit the help options
	F2 to select DHCP mode.
	x to list available attack options.
	1 to start a DHCP starvation attack.
	q to stop the attack
```

### Perform ARP poisoning using arpspoof

```
arpspoof -i eth0 -t gateway target
```
Issuing the above command informs the access point that the target system (10.10.10.10) has our MAC address (the MAC address of host machine (Parrot Security)). In other words, we are informing the access point that we are the target system.
So all the packets destined to target mac will go through us. Gateway -> attacker -> victim

```
arpspoof -i eth0 -t target gateway
```
Through the above command, the host system informs the target system (10.10.10.10) that it is the access point (10.10.10.1).
attacker tells the victim that it is the access point and all packets of victim will go through the attacker. Victim -> Attacker -> Gateway

### Perform an Man-in-the-Middle (MITM) attack using Cain & Abel

1. Open Cain
2. Configure tab 
3. Checkthe ip addres and adpater
4. Click ok
5. Click on 'Start/Stop Sniffer'
6. Click Sniffer tab
7. Click on + button or right click and select Scan MAC Addresses
8. Check All hosts in my subnet
9. All Tests
10. Click APR Tab at the bottom
11. Click + icon
12. New ARP Poison route
13. Select the devices
14. left is target right is client
15. 10.10.10.10 10.10.10.16
16. Click on created Route
17. Click on Start/Stop APR
18. Go to 10.10.10.16
19. ftp to 10.10.10.10
20. Goto machine where cain is installed
21. Click Passwords tab
22. Right panel FTP

### Spoof a MAC address using TMAC and SMAC

## Perform network sniffing using various sniffing tools

### Perform password sniffing using Wireshark

1. http.request.method == POST
2. Edit -> Find Packet
3. Select String
4. Packet Details
5. Narrow (UTF-8/ASCII)
6. Type in pwd
7. Expand the HTML Form URL Encoded: application/x-www-form-urlencoded node

### Analyze a network using the Omnipeek Network Protocol Analyzer
### Analyze a network using the SteelCentral Packet Analyzer

## Detect network sniffing

### Detect ARP poisoning in a switch-based network
### Detect ARP attacks using XArp
### Detect promiscuous mode using Nmap and NetScanTools Pro

```
nmap --script=sniffer-detect [Target IP Address/ IP Address Range]
```

The NetScanTools Pro main window appears. In the left-hand pane, under the Manual Tools (all) section, scroll down and click the Promiscuous Mode Scanner option.
