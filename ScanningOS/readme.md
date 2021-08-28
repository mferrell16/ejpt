# Scanning and OS Fingerprinting 

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
10.142.111.240/24 

3. Find active hosts with fping 
```
fping -a -g 10.142.111.240/24 2>/dev/null > fpinghosts.txt 
```

3. Find active hosts with nmap 
```
nmap -sn 10.142.111.240/24 > nmapscan.txt
```

4. Create list for nmap of live hosts 
```
cat nmapfile.txt | grep "report" | cut -d " " -f 5 > livehosts.txt
```
5. Compare lists and notice that fping scan skipped 10.142.111.213 ?????

6. Run a Syn scan on hosts 
```
sudo nmap -sS -iL livehosts.txt  
```
7. Identify OS and service version if possible 
```
nmap -sV -O -iL livehosts.txt 
```
