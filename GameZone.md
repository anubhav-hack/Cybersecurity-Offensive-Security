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

