# Lab: Reflected XSS into HTML context with nothing encoded
This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the alert function.

# Solution

First we get presented with a search box and a list of blog posts.  
![](./img/Lab_1_First_look.png)


Searching for something returns the search term in a text field above the search box.  ![](./img/Lab_1_Searching_results.png) 


And a query is added to the URL.
```/?search=Test```


Let's test to add a script tag to the search box.  
![](./img/Lab_1_Adding_script_tag.png)


And the input doesn't seem to sanitize any input and the ```alert``` function is executed.  
![](./img/Lab_1_Solved.png)