# BECOMING ROOT WITH SU
But THIS challenge (and only this challenge) does have a root password. That password is hack-the-planet, and you must provide it to su to become root! Go do that, and read the flag.

## My solve
**Flag:** `pwn.college{IALf9vUalzimSa83BD0VIUnwBsv.QX1UDN1wiM4kjNzEzW}`

1.Through my understanding of su , I used it to become the root providing the given password.  
2.Next, I ran 'cat /flag' to obtain the flag.

```bash
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{IALf9vUalzimSa83BD0VIUnwBsv.QX1UDN1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that :  
* Becoming root is a fairly common action that Linux users take, and there are two utilities that exist for this purpose: su and sudo.
* that su (the substitute user command) is not typically used to elevate to root access anymore.
* su is a setuid binary:
```
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```
* Because it has the SUID bit set, su runs as root. Running as root, it can start a root shell! Of course, su is discerning: before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password:  
```

hacker@dojo:~$ su
Password: 
su: Authentication failure
hacker@dojo:~$
```
* This check against the root password is what obsoletes su. Modern systems very rarely have root passwords, and different mechanisms (that we will learn later) are used to grant administrative access.

## References 
Did not use any references for this challenge. 

# OTHER USERS WITH SU
In this level, you must switch to the zardus user and then run /challenge/run. Zardus' password is dont-hack-me.

## My solve
**Flag:** `pwn.college{oqV7zUqxmsOZ_rTNY9GiHSz0m2N.QX2UDN1wiM4kjNzEzW}`

1.I used su followed by the username 'zardus' in order to switch to the zardus user .  
2.I provided the password and ran '/challenge/run'.  
3.Thus, I was able to obtain the flag.  

```
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{oqV7zUqxmsOZ_rTNY9GiHSz0m2N.QX2UDN1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that with no arguments, su will start a root shell (after authenticating with root's password). However, you can also give a username as an argument to switch to that user instead of root. For example:  

```
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```

## References 
Did not use any references for this challenge. 

# CRACKING PASSWORDS
This level gives you a leak of /etc/shadow (in /challenge/shadow-leak). Crack it (this could take a few minutes), su to zardus, and run /challenge/run to get the flag.

## My solve
**Flag:** `pwn.college{sMMFzKkiUsLgL2U0IMKbw7Nvs82.QX3UDN1wiM4kjNzEzW}`

1.I used john the ripper to crack the password using 'john /challenge/shadow-leak' where '/challenge/shadow-leak ' was the leak that could give me access . 
2.After finding out the password of zardus which was *aardvark*, I su 'd to zardus and ran '/challenge/run'.  
3.Thus , I obtained the flag.

```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:10 98% 1/3 0g/s 272.4p/s 272.4c/s 272.4C/s zardus999991939..zardus1915
aardvark         (zardus)
1g 0:00:00:21 100% 2/3 0.04741g/s 276.1p/s 276.1c/s 276.1C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{sMMFzKkiUsLgL2U0IMKbw7Nvs82.QX3UDN1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that :
* When you enter a password for su, it compares it against the stored password for that user. These passwords used to be stored in /etc/passwd, but because /etc/passwd is a globally-readable file, this is not good for passwords, these were moved to /etc/shadow.
* Separated by :s, the first field of each line is the username and the second is the password. A value of * or ! functionally means that password login for the account is disabled, a blank field means that there is no password (a not-uncommon misconfiguration that allows password-less su in some configurations)
```
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```
* The long string such as Zardus' $6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1. is the result of one-way-encrypting (hashing) .
* When you input a password into su, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, su grants you access to the user.
* If you don't know the password, you can still get it if you have the hashed value of the password. Even though /etc/shadow is, by default, only readable by root, leaks can happen. For example, backups are often stored, unencrypted and insufficiently protected, on file servers, and this has led to countless data disclosure.
* If a hacker gets their hands on a leaked /etc/shadow, they can start cracking passwords and wreaking havoc. The cracking can be done via the famous John the Ripper, as so:
```
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
```

## References 
Did not use any references for the challenge.

# USING SUDO
In this level, we will give you sudo access, and you will use it to read the flag.

## My solve
**Flag:** `pwn.college{AZ433oGA9flgVFn7DHXOrhRFLsy.QX4UDN1wiM4kjNzEzW}`

I used sudo followed by 'cat /flag' to obtain the flag.

```bash
hacker@users~using-sudo:~$ whoami
hacker
hacker@users~using-sudo:~$ sudo whoami
root
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{AZ433oGA9flgVFn7DHXOrhRFLsy.QX4UDN1wiM4kjNzEzW}
```

## What I learned
* a typical Linux system had a root password that administrators would use to su to root (after logging into their account with their normal account password) which could leak and they don't lend themselves well to larger environments (e.g., fleets of servers).
* To address this,we have moved from administration via su to administration via sudo (sudo originally stood for superuser do, but has changed to "su 'do'", and because su stands for "substitute user", the current meaning of sudo is "substitute user, do").
* Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root:
```
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```
* Unlike su, which relies on password authentication, sudo checks policies to determine whether the user is authorized to run commands as root. These policies are defined in /etc/sudoers.
```
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```

## References 
Did not use any references for this challenge.

