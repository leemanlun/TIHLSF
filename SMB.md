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

Using Enum4Linux to enumerate SMB, important thing to note here are the shares, especially that one that's named 'profiles'

### Exploiting SMB

Taking advantage of system misconfiguration: Anonymous SMB Share Access is a common exploit.

We know from the enumeration stage, the SMB share **location** and **name** of SMB share we are interested in.

#### SMB Client

We use client to access resource to servers.

Remotely access the SMB share using syntax: ``smbclient //[IP]/[SHARE]`` followed by tag ``-U [name]`` to specify name and ``-p [port]`` to specify port.

![image](https://user-images.githubusercontent.com/80155116/111866232-e732c880-89d0-11eb-86a8-a533f9cf2d5a.png)

Using SMB Client to find out if the share has been configured to allow anonymous access by 

1. using username "Anonymous"
2. connecting to share we found on enumeration stage
3. not supplying a password.



