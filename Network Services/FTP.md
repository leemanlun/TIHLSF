# File Transfer Protocol

### Standard port is 21

Application protocol used to allow remote transfer of files over a network. 

FTP session operates using 2 channels:

  1. a **command/control** channel
    - for transmitting commands and replies to those commands.
  2. a **data** channel
    - for transferring of data.
    
 Uses Client-Server model, client intiates connection with server, server validates login credentials then opens session.
 
 *Client can execute FTP commands on server when session is active.*
 
 ### Active vs Passive
 
 Active FTP - client opens a port and listens.
            - server required to *actively* connects to it.
 
 Passive FTP - server opens a port and listens *passively*
             - client connects it.

## Enumerating FTP

Careless implementation of FTP servers allows for exploitation of anonymous FTP login.

1. Make sure FTP client is installed on system. enter ``ftp`` to check, ``sudo apt install ftp`` to install.

2. Run nmap. ``nmap -sV -oN nmap-$ip.out $ip`` and ``cat nmap-$ip.out | grep open``.

![image](https://user-images.githubusercontent.com/80155116/111871089-4c94b280-89ed-11eb-8a3a-f3bde572c85d.png)

*vsftpd* is the variant of FTP.

3. FTP anonymous login. ``ftp $ip`` to login, anonymous as username and no password.

4. Open file. ``get PUBLIC_NOTICE.txt -`` the '-' here opens the file after downloading.

![image](https://user-images.githubusercontent.com/80155116/111871391-a5b11600-89ee-11eb-8002-077a203e72fb.png)



