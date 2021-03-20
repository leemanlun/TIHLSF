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
  
