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

To test: ``mysql -h $ip -u [username] -p ``

![image](https://user-images.githubusercontent.com/80155116/112405682-a263b480-8d77-11eb-9c54-37492cedd652.png)

### Metasploit

``search mysql_sql`` to find the module.

![image](https://user-images.githubusercontent.com/80155116/112405988-3897da80-8d78-11eb-8464-32c83d3b7d08.png)

Use, and then show option.

![image](https://user-images.githubusercontent.com/80155116/112406217-9cba9e80-8d78-11eb-9702-4a97d415701b.png)

Here we need to change the Password, Rhosts, and Username.

Running the module will default to command ``select version()``.

Module version is 5.7.29-0ubuntu0.18.04.1.

Now we change the SQL command to execute from ``select version()`` to ``show databases``.

![image](https://user-images.githubusercontent.com/80155116/112406616-629dcc80-8d79-11eb-9f02-c7c18f342f15.png)

## Exploiting MySQL

### Things we know: 

1. MySQL server dcredentials
2. Version of MySQL running
3. Number of databases and their names

#### Key Terminology

In MySQL, *Schema* is synonymous with Database, CREATE SCHEMA = CREATE DATABASE, it may be different in other database products.

*Hashes* are the product of cryptographic algorithms to turn inputs to a fixed length output.

MySQL hashes are used in different ways:

Indexing data into hash table, each hash has unique ID that serves as a pointer to original data.

search mysql_

### mysql_schemadump

![image](https://user-images.githubusercontent.com/80155116/112407602-3edb8600-8d7b-11eb-95cc-472b28456703.png)

Options for the module: 

![image](https://user-images.githubusercontent.com/80155116/112407681-6894ad00-8d7b-11eb-805d-a630c57035d7.png)

We need to change the relevant options before running: password, rhosts, username and thread.

![image](https://user-images.githubusercontent.com/80155116/112407938-c7f2bd00-8d7b-11eb-90f1-47467945f7c1.png)

![image](https://user-images.githubusercontent.com/80155116/112407967-d4771580-8d7b-11eb-8177-b5074d2871fb.png)

Now we have successfully dumped the tables and column names of the whole database.

### mysql_hashdump

![image](https://user-images.githubusercontent.com/80155116/112408430-a6460580-8d7c-11eb-877d-cf1732221096.png)

Spool and output the hash for Carl.

Finally, we'll use John the Ripper to crack the password: ``john hash.txt``.

The password is ``doggie``.

SSH to carl and now we have the flag.

![image](https://user-images.githubusercontent.com/80155116/112409543-8fa0ae00-8d7e-11eb-9b99-f504fedbf5bd.png)
