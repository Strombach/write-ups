# Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

```SELECT * FROM products WHERE category = 'Gifts' AND released = 1```
To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

# Solution
By navigating through the site we get an endpoint called "filter" that has a parameter called "category" that fetches the selected category.   
![](./img/Lab_1_FIlter_endpoint.png)

And by adding ```' OR 1=1--``` as value to the ```category``` parameter we get a long list with all the products.  
![](./img/Lab_1_SQLi_request.png)


![](./img/Lab_1_Solved.png)