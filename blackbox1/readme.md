# Black Box Penetration Test 1 

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
172.16.64.10/24 

3. Find active hosts with fping 
```
fping -a -g 172.16.64.10/24  2>/dev/null 
```
There are four targets 

4. Nmap scan targets
```
sudo nmap -sC -sV -iL hosts.txt 
```
IP: 172.16.64.101 
22/ssh 
8080/ apache 
9080/ apache 
+ http://172.16.64.101:8080/host-manager (CODE:302|SIZE:0)                                                                
+ http://172.16.64.101:8080/index.html (CODE:200|SIZE:11321)                                                       
+ http://172.16.64.101:8080/manager (CODE:302|SIZE:0)   

172.16.160.102 = site under construction 

IP: 172.16.64.140
80/ apache httpd 
dirb found: /index.html /project /server-status 
visit /project admin:admin 
dirb http://172.16.64.140/project -u admin:admin

==> DIRECTORY: http://172.16.64.140/project/backup/                                                                                                                                                  
==> DIRECTORY: http://172.16.64.140/project/css/                                                                                                                                                     
==> DIRECTORY: http://172.16.64.140/project/images/                                                                                                                                                  
+ http://172.16.64.140/project/includes (CODE:403|SIZE:304)       


IP 172.16.64.182 
22/ssh 


IP: 172.16.64.199
135/tcp
139/tcp
445/tcp 
1433 ms-sql-s SQL server 2014 
 