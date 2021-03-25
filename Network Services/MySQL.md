# MYSQL

Relational database management system (RDBMS) based on Structured Query Language (SQL).

### RDBMS

A software or service used to create and manage databases based on a relational model, relational means the data stored in dataset is organised as tables.

### SQL

MySQL is just a brand name for one of the most popular RDBMS implementations, using the language Structured Query Language.

* It is made up of server and utility programs that hhelp in the administration of mySQL databases.
* Server handles all database instructions.
  - MySQL creates a database for storing and manipulating data, defining the relationship of each table.
  - Clients make requests by making specific statements in SQL.
  - Server responds with information that was requested.

## Enumerating MySQL

We are given credentials -> ``root:password`` while enumerating subdomains of a web server.

### Port Scanning

``nmap -sV -sC -oN nmap-$ip.out`` and ``cat nmap-$ip.out | grep open``.

![image](https://user-images.githubusercontent.com/80155116/112405459-2ff2d480-8d77-11eb-89ac-9b536dbaea8a.png)

To test: ``mysql -h $ip -u [username] -p 

![image](https://user-images.githubusercontent.com/80155116/112405682-a263b480-8d77-11eb-9c54-37492cedd652.png)


