# Simple Mail Transfer Protocol

Handles the sending of email, works along POP/IMAP to allow the user to send outgoing mail and retrieve incoming mail, respectively.

### Three basic functions:

  * Verifies who is sending emails through SMTP server
  * Sends outgoing mail
  * If it fails, deliver back to sender.

### POP and IMAP

Post Office Protocol and Internet Message Access Protocol, responsible for transfer of email between client and mail server.

POP is more simple, downloads inbox from the mail server to client.

IMAP will sync the current box with new mail on server, meaning changes to inbox made on one computer over IMAP will persists.

### How does SMTP work?

Like a mail sorting office:

![image](https://user-images.githubusercontent.com/80155116/111982220-93a9b180-8b6d-11eb-8201-9ef30dfff18c.png)

1. Email client connects to SMTP server of domain, e.g. smtp.google.com. Which starts the SMTP handshake, over port 25. 
2. Client submits the sender and recipient's email address, the body of the email and attachements to server.
3. SMTP server checks whether domain name of recipient and sender is same.
4. SMTP server of server makes connection to recipient's SMTP server. If recipient's server is not available, the email gets put into SMTP queue.
5. Recipient's SMTP server verifies incoming email - by checking if domain and user name have been recognised. Finally forwarding the email to POP/IMAP server.
6. Email then shows up in recipient's inbox.

## Enumerating SMTP

### Enumerating Server Details

Vulnerable servers will provide initial foothold into a network. *smtp_version* module in metasploit does this, it will scan range of IP addresses and determine version of any mail servers it encounters.

### Enumerating Users

Two internal commands:
 1. VRFY - confirming names of valid users 
 2. EXPN - reveals actual address of user's aliases and lists of email.

We can do this manually over telnet but we'll use MetaSploit, ``sudo apt update`` to update.

``msfconsole`` to start MetaSploit.

### Port Scanning

``nmap -sV -sC -oN nmap-$ip.out $ip and cat nmap-$ip.out | grep open``

![image](https://user-images.githubusercontent.com/80155116/112123733-65d47380-8c26-11eb-8eed-cae86922abe5.png)

### Metasploit

``msfconsole -q`` to load.

``search smtp_version`` to search for the module, full module name is ``auxiliary/scanner/smtp/smtp_version``.

``use 0`` to use module and ``show options`` to list the options.

![image](https://user-images.githubusercontent.com/80155116/112238333-4f233080-8ca9-11eb-8bb9-5a03948873f5.png)

``RPORT`` is using 25, so its correct. However, ``RHOSTS`` hasn't been set up.

Set ``THREADS`` to 32 to speped up. 

![image](https://user-images.githubusercontent.com/80155116/112239443-577c6b00-8cab-11eb-9dd2-755b136cd56f.png)

Run the exploit,

![image](https://user-images.githubusercontent.com/80155116/112239566-94486200-8cab-11eb-9d71-f0cca29330c8.png)

*polosmtp.home* is the system mail name, *Postfix* is the name of the Mail Transfer Agent (MTA).

Now look up ``smtp_enum``, full module name is ``auxiliary/scanner/smtp/smtp_enum``.

We are gonna use ``top-usernames-shortlist.txt`` from Usernames subsection of seclists ``/usr/share/seclists/Usernames``.

![image](https://user-images.githubusercontent.com/80155116/112239988-61eb3480-8cac-11eb-8042-8a54290061f1.png)

USER_FILE need to be set to the wordlist's path, RHOSTS also needs to be changed to our attacking machine.




