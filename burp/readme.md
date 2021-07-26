# Burp Suite 

> Makayla Ferrell | July 25th, 2021

### Steps 


1. Connect to VPN 
```
sudo openvpn <filename> 
```

2. Open burp and set target scope 

3. Run burp spider to find hidden folders 
Finds /Y7gMEMZtin

4. Use repeater 'follow redirection' to find /Y7gMEMZtin/login.php 

5. In bottom of response find a debug login 

<!-- 
************************************************************************************
	ALERT: Remove this in production!!	
************************************************************************************

DEBUGGIN MODE 
To avoid the authentication page, send in the query string DEBUG=policeDebug 

e.g. login.php?DEBUG=policeDebug
-->
 
 6. Visit 10.100.13.5/Y7gMEMZtin/login.php?DEBUG=policeDebug 
 This takes you to the dashboard for the police force. 
 