# TIHLSF THINGS I HAVE LEARNED SO FAR

(from tryhackme.com)

**Introductory Networking**

- OSI Model

Open Systems Interconnection - 7 layers, Application, Presentation, Session, Transport, Network, Data Link, Phyisical

Anxious Pale Shakespeare Treated Nervous Drunks Patiently

7. Application

- Provides networking options to programs running on a computer.
- Data given to Application layer is passed down to presentation layer.

6. Presentation

- Handles translation, encryption, compression and other transformations of data.

5. Session

- Sets up connections with other computers, also maintains the connection. Session created is unique to the connection.

4. Transport

- TCP and UDP protocols. TCP ensures all packets gets sent to the right place even when it fails. UDP does the oppisite, doesn't care if failed.
- TCP is used when accuracy is favoured over speed (file transfer, loading webpages).
- UDP is used when speed is more important (video streaming).

3. Network

- Responsible for locating the destination of request.
- Logical addresses (IP addresses)

2. Data Link

- Receives packet and IP adress of remote computer from Network layer and adds MAC address of receiver.
- Every network enabled computer has a **N**etwork **I**nterface **C**ard that comes with MAC address to identify.
- Makes sure data is in a format suitable for transmission.

1. Physical

- Converts binary data of transmission into signals and vice versa.
-


