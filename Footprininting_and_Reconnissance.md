# Footprinting and Reconnaissance

## Footprinting Through Search Engine

1. Google Dork
	* intext:keyword
	* inurl:word
	* intitle:keyword
	* site:something
	* filetype:pdf,doc
	* link:something
	* related:domain
	* cache:domain
	* Operators
		* OR Operator
			* site:something | site:else
		* AND Operator
			* site:something & site:else
		* '*' Operator
			* site:*.in
3. Reverse Google Image Search
	* **https://citizenevidence.amnestyusa.org/ **
4. FTP Search Engine - Napalm
5. IoT Search Engine - Shodan

## Footprinting Through Web Services

1. Netcraft
	* Information Obtained - 
		* IP Delegation
		* Network - DNS related Information
		* Hosting History
		* Site Technology
		* Passive OS Detection	
2. People Search Engine - PeekYou
3. Email Harvesting - theHarvester
```
theHarvester -d microsoft.com -b baidu.com
```
4. Deep and Dark Web Search


## Footprinting Through Social Networking Sites

1. From Linkedin - theHarvester
```
theHarvester -d eccouncil -b linkedin
```
2. Sherlock
```
python3 sherlock Person Name
```
4. followermonk.com - twitter
 * https://followerwonk.com/

## Website Footprinting

1. ping
```
ping certifiedhacker.com
```
We get the website's IP Address 
```
ping certifiedhacker.com -f -l 1500
```
Fragmentation Error
```
ping certifiedhacker.com -f -l 1472
```
Max Fragmentated bit size - 1472 might change from webiste to website
```
ping -i 3 certifiedhacker.com -n 1
```
-i - > Time to Live -> Maximum vale of ttl is 255
Increase -i until you recieve a reply from the IP obtained in the first ping step


2. Domain Doisser (https://centralops.net/co/DomainDossier.aspx)
	* Information Obtained
		* Domain whois Record
		* Network whois Record
		* Traceroute
		* Service Scan
		* DNS Records

4. web data extractor (windows)

http://www.webextractor.com/download.htm

5. Website Mirroring HTTrack (windows)

https://www.httrack.com/

6. cewl 
```
cewl -d 2 -m 5 -w outputfile domain
```
-d -> depth, -m -> minimum word length

## Email Footprinting
1. EmailTrackerPro (windows)

http://www.emailtrackerpro.com/download.html

## WhoIs Footprinting
1. whois lookup

https://whois.domaintools.com/

## DNS Footprinting
1. nslookup - http://www.kloth.net/services/nslookup.php
```
nslookup
set type=?
```
where ? can be - 
* A - Specifies a computer's IP address.
* ANY - Specifies all types of data.
* CNAME - Specifies a canonical name for an alias.
* MX - Specifies the mail exchanger.
* NS - Specifies a DNS name server for the named zone.
* PTR - Specifies a computer name if the query is an IP address; otherwise, specifies the pointer to other information.
* SOA - Specifies the start-of-authority for a DNS zone.

7. Reverse DNS Lookup
	* https://www.yougetsignal.com/tools/web-sites-on-web-server/
	* DNSRecon
	```
	dnsrecon -r 162.241.216.0-162.241.216.255
	```

## Networking Footprinting

1. Domain Doisser - https://centralops.net/co/DomainDossier.aspx
2. traceroute

## Footprinting using Tools

### 1. Recon-ng
#### Network Reconnaissance
```
> help
> marketplace install all
> module search
> workspace creeate name
[name] > workspace list
[name] > db insert domains
				certifiedhacker.com
[name] > show domains
[name] > modules load brute
[name] > modules load recon/doamin-hosts/brute_hosts
[name] > run
[name] > back

> modules load recon/domain-hosts/bing_domain_web
> run 
```
Reverse IP Lookup
```
> modules load recon/hosts-hosts/reverse_resolve
> run
> show hosts
> back
```
Reporting
```
> modules laod reporting/html
> options set FILENAME pathofdestinationfile.html
> options set CREATOR Yourname
> options set CUSTOMER Customername
> run
```

#### For extracting Personal information

Extracts contacts associated with this domain
```
> workspace create name
>  modules load recon/domains-contacts/whois_pocs
>  info command
>  options set SOURCE facebook.com
>  run
```

Validation of these contacts obtained
```
> modules load recon/profiles-profiles/namechk
> options set SOURCE Personname
> back
> modules load recon/profiles-profiles/profiler
```

### 3. Maltego
	* Transforms Used
		* To DNS Name [Using Name Scheme]
		* To DNS Name [Using Name Schema]
		* To DNS Name
		* To DNS Name-MX(Mail Server)
		* To DNS Name-NS(Name Server)
		* To IPAddress[DNS]
		* To Location 
		* To Entities from whois[IBM Watson]

### 4. OSR Framework

Check for existance of a profile on different social networking sites
```
usufy.py -n Username -p platform
```
Check for existing domain using words or nicknames
```
domainfy.py -n name -t all
```
Gathers information about email accounts
```
mailfy.py
```
Gathers information about users on social networking pages
```
searchfy.py
```
Checks for existance of a given series of phone numebrs
```
phonefy.py
```
Extract entitites using regular expression from provided URLs
```
entify.py
```
### 5. BillCipher

Github Link - https://github.com/bahatiphill/BillCipher

Features
* DNS Lookup
* Whois Lookup
* GeoIP Lookup
* Subnet Lookup
* Port Scanner
* Page Links
* Zone Transfer
* HTTP Header
* Host Finder
* IP-Locator
* Find Shared DNS Servers
* Get Robots.txt
* Host DNS Finder
* Reserve IP Lookup
* Email Gathering (use Infoga)
* Subdomain listing (use Sublist3r)
* Find Admin login site (use Breacher)
* Check and Bypass CloudFlare (use HatCloud)
* Website Copier (use httrack) NEW!
* Host Info Scanner (use WhatWeb) NEW!

### 8. OSINT Famework	

## Network Topology Mapping Tools

1. Microsoft Visio
2. Solarwinds Network Topology Mapper
3. LucidChart
4. InterMapper
5. LANFlow
