# Footprinting  Web Server

1.	Ghosteye

2.	Skipfish
	* Skipfish -o outputdirectorylocation -S /usr/share/skipfish/dictionaries/complete.wl Target

3.	Httprecon (Windows)

4.	ID Serve (Windows)

5.	Netcat
	* nc ip port
	* nc ip 80
		* GET / HTTP/1.1

6.	Telnet
	* telnet ip port

7.	Nmap Scripts
	* http-enum
	* http-trace -d domain
	* nmap --script hostmap-bfk -script-args hostmap-bfk.prefix=hostmap- websitename
	* http-waf-detect

8.	uniscan
	* uniscan -u domain -q
		* or web directories
	* uniscan -u domain -we
		* enable file check robot.txt and sitenmap.xml
	* uniscan -u domain -d 
		* dynamic testing
		* report generated at /usr/share/uniscan/report

9.	Gobuster
	* gobuster dir -u target -w wordlistlocation 

Web Server Attack – Bruteforce FTP Credentials
1.	hydra
	* hydra -L Usernamewordlistlocation -P Pwwordlistlocation ftp://ip
