# Burp Suite Basics 

> Makayla Ferrell | July 25th, 2021

### Steps 


1. Connect to VPN 
```
sudo openvpn <filename> 
```

2. Open burp and set target scope 


3. View site source code 

<html>
<head></head>
<center><h1>Site under construction!</h1></center>
<hr /><br />
<!-- TODO: -->
<!-- add a 302 redirect to the new page -->
<!-- remember to remove robots.txt when done -->
A new site will be announced soon..
</html>


4. Check robots.txt 
User-agent: *
Disallow: /cgi-bin/
Disallow: /includes/
Disallow: /images/
Disallow: /scripts/
Disallow: /*?debug=*
Disallow: /connections/
Disallow: /backup/
Disallow: /settings/

5. Use burp intruder with robots.txt list with GET request to find other active pages 
Connections is the only active page. 

6. Visit /connections
This page says "Debug is FALSE"

7. Use burp repeater to play with /connections/?debug param 

8. Vist /connections?debug=TRUE 
Database: 127.0.0.1; User: root; Password: 1f!@3zL309aKpei1KbmM<br />
