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

2. Domain Doisser (https://centralops.net/co/DomainDossier.aspx)
	* Information Obtained
		* Domain whois Record
		* Network whois Record
		* Traceroute
		* Service Scan
		* DNS Records

4. web data extractor (windows)
5. Website Mirroring HTTrack (windows)
6. cewl 
```
cewl -d 2 -m 5 -w outputfile domain
```
-d -> depth, -m -> minimum word length

## Email Footprinting
1. EmailTrackerPro (windows)
2. WhoIs Footprinting
3. whois lookup
4. DNS Footprinting
5. nslookup - http://www.kloth.net/services/nslookup.php
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

1. Recon-ng

### Network Reconnnaissance
```
recon-ng
help
marketplace intsall all
module search
workspace create CEH
workspace list
db insert domains
	certifiedhacker.com
show domains
modules load brute
module load recon/domain-hosts/brute_hosts
run
```
```
modules load recon/domain-hosts/bing_domain_web
run
```
Perform reverse IP Lookup
```
modules load recon/hosts-hosts/reverse_resolve
run
```
Reporting
```
modules load reporting/html
options set FILENAME Path.html
options set CREATOR Name
options set CUSTOMER Nmae
```

### Personal Information

Extract Contacts assosciated with domain

```
recon-ng
workspaces create reconperson
modules load recon/domains-contacts/whois_pocs
info command
options set SOURCE website
run
```

Contacts are obtained
Now, lets validate these

```
modules load recon/profiles-profiles/namechk
options set SOURCE PersonName
```

Checks existance of user profiles

```
modules load recon/profiles-profiles/profiler
```

Follow reporting steps

2. Maltego
	
* Transforms Used
	* Domain whois Record
	* DNSNmae-MX(Mail Server)
	* DNSName-NS(Name Server)
	* IP Address [DNS]
	* To Location\
	* WHOIS[IBM Watson]

3. OSR Framework
	* Check for the existence of a profile on different social networking sites.
	* Check for existing domain using words or nicknames.
	* Check for existing domain using words or nicknames.
	* Gathers information about email account.
	* Gathers information about users on social networking pages.
	* Checks for the existence of a given series of phone numbers
```
phonefy.py
```
```
usufy.py -n Username -p platform
```
```
usufy.py -n Username -p platform
```
```
domainfy.py -n name -t all
```
```
mailfy.py
```
```
searchfy.py
```

4. BillCipher (https://github.com/bahatiphill/BillCipher)
5. OSINT Famework	

## Network Topology Mapping Tools

1. Microsoft Visio
2. Solarwinds Network Topology Mapper
3. LucidChart
4. InterMapper
5. LANFlow
