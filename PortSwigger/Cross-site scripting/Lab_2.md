# Lab: Stored XSS into HTML context with nothing encoded
This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the blog post is viewed.

# Solution
The site seems to be a blog where a user can comment on individual blog posts.  
![](./img/Lab_2_Entering_the_blog.png)


![](./img/Lab_2_Comment_form.png)


Adding script tags in the comments form.  
![](./img/Lab_2_Comment_script_tag.png)


![](./img/Lab_2_Solved.png)

Entering the blog post again executes the script.  
![](./img/Lab_2_Alert_execute.png)