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

![image](https://user-images.githubusercontent.com/80155116/111865572-c10b2980-89cc-11eb-829c-6317c5fee2db.png)

### Exploiting SMB



