## Lab: Username enumeration via different responses
 This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:

    Candidate usernames
    Candidate passwords

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

# Solution
Accessing the login page and entering a random password to get the endpoint into Burpsuite.  
![[./img/Lab_1_First_Access.png]]