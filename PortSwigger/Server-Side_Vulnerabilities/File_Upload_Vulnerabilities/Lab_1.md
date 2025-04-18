# Lab: Remote code execution via web shell upload

This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: wiener:peter

# Solution
When using the provided credentials we can see a form for uploading a avatar for the account.  
![](./img/Lab_1_First_Login.png)


We start by uploading an image to see how the request and what the proper functionality looks like.  
![](./img/Lab_1_Upload_req_res.png)


And we can see that the name of the uploaded file is kept and we can access the file with the path seen in the URL field of the browser (```/files/avatars```).  
![](./img/Lab_1_Testing_upload.png)

Let's see if how we can upload a PHP script to solve the lab. We start by creating a PHP file containing this one line: ```<?php echo system($_GET['command']); ?>```
And we seem to be successful.  
![](./img/Lab_1_PHP_script_uploaded.png)


And we have a working webshell where we can execute system commands (in this case "id"):  
![](./img/Lab_1_Testing_command.png)


Using the cat command we can get the content of the file requested in the lab instructions.  
![](./img/Lab_1_Getting_secret.png)


![](./img/Lab_1_Solved.png)