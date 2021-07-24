# Find the Secret Server 

> Makayla Ferrell | July 23rd, 2021

### Steps 

1. Connect to VPN 
```
sudo openvpn <filename> 
```

2. Verify connection to first two webservers and no connection to third server 
```
curl http://<IP> 
```

3. Check current routes 
```
route 
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         10.0.2.2        0.0.0.0         UG    100    0        0 eth0
10.0.2.0        0.0.0.0         255.255.255.0   U     100    0        0 eth0
10.175.34.0     0.0.0.0         255.255.255.0   U     0      0        0 tap0
172.16.88.0     10.175.34.1     255.255.255.0   UG    0      0        0 tap0
192.168.241.0   10.175.34.1     255.255.255.0   UG    0      0        0 tap0

4. Add route to third web server 
```
sudo ip route add 192.168.222.0/24 via 10.175.34.1 
```
This will route the third network (secret one) through the same gateway as the first two 

5. Check route again to make sure it was added 
```
route
```

6. Visit or Curl website to prove connectivity. 
