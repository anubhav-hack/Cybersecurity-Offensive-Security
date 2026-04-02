# GameZone - TryHackMe

![Initial Access](screenshot/62.png)

## Task 2 - Deploy the vulnerable machine 

Q1) Deploy the machine and access its web server.

![Initial Access](screenshot/63.png)

**Ans** No answer needed

Q2) What is the name of the large cartoon avatar holding a sniper on the forum?

**Ans** Agent 47

## Task 3 - Qbtain access via SQLI 

 SQL is a standard language for storing, editing and retrieving data in databases. A query can look like so:

**SELECT * FROM users WHERE username = :username AND password := password**

In our GameZone machine, when you attempt to login, it will take your inputted values from your username and password, then insert them directly into the query above. If the query finds data, you'll be allowed to login otherwise it will display an error message.

Here is a potential place of vulnerability, as you can input your username as another SQL query. This will take the query write, place and execute it.

**Ans** No answer needed

Lets use what we've learnt above, to manipulate the query and login without any legitimate credentials.

If we have our username as admin and our password as: ' or 1=1 -- - it will insert this into the query and authenticate our session.

The SQL query that now gets executed on the web server is as follows:

**SELECT * FROM users WHERE username = admin AND password := ' or 1=1 -- -**

The extra SQL we inputted as our password has changed the above query to break the initial query and proceed (with the admin user) if 1==1, then comment the rest of the query to stop it breaking.


**Ans** No answer needed

GameZone doesn't have an admin user in the database, however you can still login without knowing any credentials using the inputted password data we used in the previous question.

Use ' or 1=1 -- - as your username and leave the password blank.

Q4) When you've logged in, what page do you get redirected to?

![Initial Access](screenshot/64.png)

![Initial Access](screenshot/65.png)

**Ans**  portal.php

## Task 4 - Using SQLMap 

Q5) In the users table, what is the hashed password?

![Initial Access](screenshot/78.png)

![Initial Access](screenshot/79.png)

![Initial Access](screenshot/80.png)

![Initial Access](screenshot/81.png)

**Ans:** ab5db915fc9cea6c78df88106c6500c57f2b52901ca6c0c6218f04122c3efd14

Q6) What was the username associated with the hashed password?

**Ans:** agent47

Q7) What was the other table name?

![Initial Access](screenshot/82.png)

**Ans:** post

## Task 4 - Cracking a password with JohnTheRipper 

Q8) What is the de-hashed password?

![Initial Access](screenshot/83.png)

**Ans:** videogamer124

Q9) Now you have a password and username. Try SSH'ing onto the machine.

What is the user flag?

![Initial Access](screenshot/84.png)

![Initial Access](screenshot/85.png)

**Ans** 649ac17b1480ac13ef1e4fa579dac95c

## Task 5 - Exposing services with reverse SSH tunnels

Q10) We will use a tool called ss to investigate sockets running on a host.

If we run ss -tulpn it will tell us what socket connections are running

Argument	Description
-t	Display TCP sockets
-u	Display UDP sockets
-l	Displays only listening sockets
-p	Shows the process using the socket
-n	Doesn't resolve service names

How many TCP sockets are running?

![Initial Access](screenshot/86.png)

**Ans:** 5

Q11) What is the name of the exposed CMS?

![Initial Access](screenshot/87.png)

![Initial Access](screenshot/88.png)

![Initial Access](screenshot/89.png)

**Ans:** Webmin

Q12) What is the CMS version?

**Ans:** 1.580

## Task 6 - Privilege Escalation with Metasploit 

Q13) What is the root flag?

![Initial Access](screenshot/90.png)

![Initial Access](screenshot/91.png)

![Initial Access](screenshot/92.png)

![Initial Access](screenshot/93.png)

![Initial Access](screenshot/94.png)

![Initial Access](screenshot/95.png)

**Ans:** a4b945830144bdd71908d12d902adeee

![Initial Access](screenshot/96.png)



