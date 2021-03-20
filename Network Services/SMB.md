# Server Message Block Protocol

A client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.

#### *Response-Request Protocol*

- Transmits multiple messages between client and server to establish connection.
- Client usually uses TCP/IP.

When connection is established, client sends SMB commands to server that allow themn to access shares, open files, read and write files. 

*SMB is a file system.. over the network.*

SAMBA for UNIX.

### Enumerating SMB

**Enumeration** - process of gathering information on a target to find potential attack vectors to aid in exploitation.

SMB is often a great starting point for enumeration.

#### 1. Port Scanning

Use Nmap, `-A` tag to enable OS Detection, Version Detection, Script Scanning and Traceroute.

`-p-` to scan all ports, not just top 1000.

#### 2. Enum4Linux

Tool for enumerating SMB shares.

![image](https://user-images.githubusercontent.com/80155116/111865572-c10b2980-89cc-11eb-829c-6317c5fee2db.png)

![image](https://user-images.githubusercontent.com/80155116/111866306-6b854b80-89d1-11eb-8bd3-7e01df28fbc6.png)

Using Enum4Linux to enumerate SMB, important thing to note here are the **shares**, especially that one that's named 'profiles'.

### Exploiting SMB

Taking advantage of system misconfiguration: Anonymous SMB Share Access is a common exploit.

We know from the enumeration stage, the SMB share **location** and **name** of SMB share we are interested in.

#### SMB Client

We use client to access resource to servers.

Remotely access the SMB share using syntax: ``smbclient //[IP]/[SHARE]`` followed by tag ``-U [name]`` to specify name and ``-p [port]`` to specify port.


Using SMB Client to find out if the share has been configured to allow anonymous access by 

1. using username "Anonymous"
2. connecting to share we found on enumeration stage
3. not supplying a password.

![image](https://user-images.githubusercontent.com/80155116/111866232-e732c880-89d0-11eb-86a8-a533f9cf2d5a.png)


Here we use SMB command ``get <FILE> <newFileName>`` to download the text file from the share,
and then we run the text file:

![image](https://user-images.githubusercontent.com/80155116/111866398-0da53380-89d2-11eb-80df-dd12e6ca81a1.png)


![image](https://user-images.githubusercontent.com/80155116/111866430-375e5a80-89d2-11eb-8133-bab3241ec7cd.png)

**Important info: Name of owner, context of email -> SSH enabled to access main server due.**

Now we have the content of the .ssh file! These are the authorization keys.

![image](https://user-images.githubusercontent.com/80155116/111866519-f0249980-89d2-11eb-9a87-645f94fd0cdb.png)

id_rsa is most useful for us, it's the default name of an SSH identity file.

![image](https://user-images.githubusercontent.com/80155116/111866986-07b15180-89d6-11eb-9885-b07c03c25e3a.png)

now change the permission of id_rsa to 600, user who owns this file (me) can do everything, group and everyone else have no permission.

### ``chmod 600 id_rsa``

this is unrelated but this is my unsuccessful attempt at trying to find the username (cactus). couldn't find it so i looked up the answer. *please let me know if you know how.*

![image](https://user-images.githubusercontent.com/80155116/111867066-8ad2a780-89d6-11eb-8f2c-35d8299279ad.png)

### ``ssh -i id_rsa cactus@10.10.11.186`` to login.

![image](https://user-images.githubusercontent.com/80155116/111867128-f288f280-89d6-11eb-949a-b42900f9247b.png)

*this is unrelated too but just wanted to showcase how i used grep to find out what the flag -i does.*

![image](https://user-images.githubusercontent.com/80155116/111867150-14827500-89d7-11eb-858a-5d2b7a5dd2ac.png)


