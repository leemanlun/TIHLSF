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

