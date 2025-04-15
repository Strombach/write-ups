# Lab
This lab has a stock check feature which fetches data from an internal system.

To solve the lab, use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.

# Solution

Entering the site again we see again (see SSRF Lab_1) that the functionality to check the stock is present and seems to works in the same way. The client has a URI sent to the server that fetches the number of items in stock.  
![](./img/Lab_2_Check_stock_on_page.png)

![](./img/Lab_2_Check_stock_burp.png)


The decoded URI:
```http://192.168.0.1:8080/product/stock/check?productId=1&storeId=1```
Using the same IP in the request didn't work. We get an 400 error back.    
![](./img/Lab_2_Admin_req_error.png)


In the lab instruction it says "scan", so the admin is probably on another host.
Using the Intruder in Burpsuite to send a request to a different IP until we get a successful response. Enumerating from host IP 1 to 255 to cover the whole IP range.  
![](./img/Lab_2_Intruder_setup.png)

Using the Intruder to send requests, we see that the IP 192.168.0.149 returns a 200 status code where every other failed request returning a 500, meaning we got a successful request when trying to find the ```/admin``` endpoint on 192.168.0.149.  
![](./img/Lab_2_Intruder_results.png)


By sending the successful request to the Repeater we can send the request again and see the HTML of the admin dashboard and see the endpoint we need to hit through the "stockApi" parameter.  
![](./img/Lab_2_Repeater_admin_endpoint.png)


Like in Lab_1 we get a 302, and get redirected to /admin again.
![](./img/Lab_2_Delete_endpoint.png)


And by going back to the /admin endpoint we see the message and the list of users left.  
![](./img/Lab_2_Dashboard_results.png)

![](./img/Lab_2_Solved.png)