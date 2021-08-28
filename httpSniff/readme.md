# HTTP(s) Traffic Sniffing 

< Makayla Ferrell | July 23rd, 2021


### Steps

1. Connect to VPN 
```
sudo openvpn <filename> 
```

2. Open wireshark 
Click to start sniffing on tab0 (vpn interface)

3. Visit http website first and view username and password 
Note: right click and follow TCP stream to view easier. 
```
user=hello&pass=goodbye&login=loginH
```
4. repeat for https website and see encrypted form 
s