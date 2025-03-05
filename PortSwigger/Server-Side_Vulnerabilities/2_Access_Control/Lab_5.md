## Lab: User ID controlled by request parameter with password disclosure
This lab has user account page that contains the current user's existing password, prefilled in a masked input.

To solve the lab, retrieve the administrator's password, then use it to delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution
Start with login in with provided credentials
![](Lab_5_Login.png)
![](Lab_5_Login_Account_Request.png)
Trying to change request to ```?id=admin```
![](Lab_5_Try_Admin.png)
This didn't work, got redirected back to the login page.
![](Lab_5_Login_Page.png)
But with ```?id=administrator``` we get the statuscode 200 and can see that we are logged in as administrator
![](Lab_5_Query_Administrator.png)
![](Lab_5_Administrator_Access.png)
In the HTML document we find a input field, labeled "Password", with a value. Could this be a password in plaintext with just the "hidden" attribute?
![](Lab_5_HTML_Value.png)
Let's try:
![](Lab_5_Administrator_Login.png)
Successful login!
And now we can see the Admin Panel
![](Lab_5_Administrator_Account_Page.png)And can now delete users
![](Lab_5_Admin_Panel.png)
![](Lab_5_Successfully_Deleted_User.png)