# Nessus

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
192.168.99.70/24

3. Find active hosts with fping 
```
fping -a -g 192.168.99.70/24 2>/dev/null > fpinghosts.txt 
```
The target is 192.168.99.50.

4. Discover target OS and services 
```
nmap -sV -O 192.168.99.50
```
This is a windows machine. 

5. Start Nessus 
```
sudo service nessusd start 
https://kali:8834 
```

6. Configure scan
Advanced Scan -> Don't scan nessus host, TCP scan, only windows plugins 

7. Export results into report 
