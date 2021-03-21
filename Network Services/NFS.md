# Network File System

Allows system to share directories and files with others over a network

1. Client request to mount a directory from a remote host on local directory
2. Server checks if user has permission to mount whatever was requested
3. Server then returns a file handle which uniquely identifies each file and directory
4. To access files using NFS, RPC call is placed to NFSD on server.

You can use NFS to transfer files from Windows to Non-Windows.

## Enumerating NFS

### NFS-Common

Every system with NFS needs this installed, contains lockd, statd, **showmount**, nfsstat, gssd, idmap and **mount.nfs**.

Port scanning: 
``nmap -A -p- -oN nmap-$ip.out $ip`` and ``cat nmap-$ip.out | grep open``

### Mounting NFS shares

``sudo mount -t nfs IP:share /tmp/mount/ -nolock``

![image](https://user-images.githubusercontent.com/80155116/111902307-d3a36280-8aa1-11eb-82f9-e9b9d4446c77.png)

To list the NFS shares:

``/usr/sbin/showmount -e [IP]``

![image](https://user-images.githubusercontent.com/80155116/111902720-a788e100-8aa3-11eb-813d-2cf85294b561.png)

*not sure why this doesn't work, i had to manually trasverse to the location*

![image](https://user-images.githubusercontent.com/80155116/111902742-bb344780-8aa3-11eb-9e7d-249fd1f9fec1.png)

So now we have the share name ``/home``.

Make a folder on local machine to mount the share to ``mkdir /tmp/mount``, since it is /tmp, it will be removed upon restart.

Now run the mount command mentioned earlier to the folder ``sudo mount -t nfs $ip:home /tmp/mount/ -nolock``.

![image](https://user-images.githubusercontent.com/80155116/111902863-50cfd700-8aa4-11eb-911f-f58f82317d03.png)

``ls -la`` to list all the hidden files! we're interested in the .ssh folder, might contain keys.

![image](https://user-images.githubusercontent.com/80155116/111903015-fd11bd80-8aa4-11eb-8624-81a4b8ca6bb9.png)

authorized_keys —> An authorized key in SSH is a public key used for granting login access to users

id_rsa → this is the private key of the user which used to login to the system

id_rsa.pub → this is the key that used send others to encrypt when they send message to us.

### To gain SSH access

1. ``cp id_rsa /tmp`` copy id_rsa to /tmp
2. ``chmod 600 id_rsa`` change permission
3. ``ssh -i id_rsa cappucino@$ip``

## Exploiting NFS

### Shell Privilege Escalation

We'll try this since we have low shell on the machine, depending on how it's configured.

### root_squash

Prevents anyone connecting NFS from getting root access to the NFS volume, root squashing is enabled on default.

### SUID

When files are with SUID bit set, it means the files can be run with permission of owner/group, we'll use this to get shell with these privileges.

### Here's how to do it

* We can upload files and control their permissions
* We can set permission of whatever we upload(in this case a bash shell executable)
* We then log in with SSH, execute the file to get root shell.

``NFS Access ->

        Gain Low Privilege Shell ->

            Upload Bash Executable to the NFS share ->

                Set SUID Permissions Through NFS Due To Misconfigured Root Squash ->

                    Login through SSH ->

                        Execute SUID Bit Bash Executable ->

                            ROOT ACCESS
``
Download the bash file and move it to the mount on local. ``cp ~/Downloads/bash .``

``sudo chown root bash`` to make sure it's own by root user.




