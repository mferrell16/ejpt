# Dirbuster

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
fping -a -g 10.104.11.50/24 2>/dev/null 
```
The target is 10.104.11.96. 

4. Run dirb to find hidden directories
```
dirb 10.104.11.96
```
/announce 
/staff 


5. Read message in /staff/readme.md
@Dev Team: ALWAYS make a backup copy of any file in production.

Copy it by changing its extension to old, bak, xxx or whatever you want, but do not blindly overwrite a file!

Thanks
 Your project manager 

6. Find include/config.old 


