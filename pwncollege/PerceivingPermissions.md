## POINTS TO NOTE:
* In Linux, files have different permissions or file modes. You can check out the permissions of a file or directory using ls -l.
```
hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
```
* The first character of each line represents the file type. In pwn_directory's case, the d indicates that it's a directory, and in college_file's case, the - represents that it's a normal file.
* The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting the permissions that the user who owns the file (termed the "owner") has to the file, 3 characters denoting the permissions that the group that owns the file (termed the "group") has to the file, and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

# CHANGING FILE OWNERSHIP
In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use chown to your heart's content as the hacker user (again, typically, this requires you to be root). Use this power wisely and chown away.  

## My solve
**Flag:** `pwn.college{8EDdTXLTw2mUG6gi53XpDLlLm0Y.QXxEjN0wiM4kjNzEzW}`

Using *chown[username][file]*, I shifter to hacker user and catted out the flag.

```
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{8EDdTXLTw2mUG6gi53XpDLlLm0Y.QXxEjN0wiM4kjNzEzW}
```

## What I learned
* Every file in Linux is owned by a user on the system.
* The two most important user accounts are:
   + Your user account! On pwn.college, this is the hacker user, regardless of what your username is.
   + root: This is the administrative account.

* we can change the ownership of files! This is done via the chown (change owner) command:
  ```
  chown [username] [file]
  ```
* Typically, chown can only be invoked by the root user.

## References 
Did not use any references for this challenge.  

# GROUPS AND FILES
In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user. Change the group ownership of the flag file, and read the flag.

## My solve
**Flag:** `pwn.college{8MfMK4TaJAw9dOQvo5P13AzsqKh.QXxcjM1wiM4kjNzEzW}`

1.I used 'id' to find the groups that I am part of as the hacker user .  
2.Next , I used *chgrp* to change the group ownership of the file '/flag'.  
3.I then catted out '/flag' and obtained the flag.

```
hacker@permissions~groups-and-files:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{8MfMK4TaJAw9dOQvo5P13AzsqKh.QXxcjM1wiM4kjNzEzW}
```

## What I learned
* Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.
* You can check what groups you are part of with the id command:
  ```
  hacker@dojo:~$ id
  uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
  hacker@dojo:~$
  ```
* graphical output can be done via the special /dev/fb0 file.
```
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```
* This file is a special device file (type c means it is a "character device"), and interacting with it results in changes to the display output (rather than changes to disk storage, as for a normal file!). Zardus' user account on his machine can interact with it because the file has a group ownership of video, and Zardus is a member of the video group.
* group ownership can be changed with the chgrp (change group) command:
```
chgrp [groupname] [filename]
```


## References 
Did not use any references for this challenge. 

# FUN WITH GROUPS NAMES
In this challenge , the group name is randomized so we will need to find that name and change ownership using 'chgrp' and find the flag.

## My solve
**Flag:** `pwn.college{QCej0MtjDSHhk6dfK2t3e5bDTys.QXycjM1wiM4kjNzEzW}`

1.Using *id" to know the group names and find out the randomized group name which in this case is *grp32205*.  
2.Next, Using 'chgrp grp32205 /flag ' , I changed the ownership and that group.  
3.I catted out the flag using 'cat /flag' . 

```
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp32205) groups=1000(grp32205)
hacker@permissions~fun-with-groups-names:~$ chgrp grp32205 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{QCej0MtjDSHhk6dfK2t3e5bDTys.QXycjM1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to find the the randomized group name if there is one and further learnt how to use chgrp and id.

## References 
 Did not use any references for this challenge.  

# CHANGING PERMISSIONS
In this challenge, you must change the permissions of the /flag file to read it! Typically, you need to have write access to the file in order to change its permissions, but I have made the chmod command all-powerful for this level, and you can chmod anything you want even though you are the hacker user. This is an ultimate power. The /flag file is owned by root, and you can't change that, but you can make it readable.

## My solve
**Flag:** `pwn.college{cTfDEcU4ZJUl7dKQfPKblRaMSbZ.QXzcjM1wiM4kjNzEzW}`

1.First , I listed the permissions and observed the /flag file.  
2.I used my understanding of the 'chmod' command and gave reading access to the user , group and other members i.e chmod ugo+r * .  
3.Then I catted out the flag.

```
hacker@permissions~changing-permissions:~$ ls -l
total 28
-rw------- 1 hacker hacker 175 Sep 29 10:28 COLLEGE
drwx------ 1 hacker hacker   0 Sep 21 14:17 Desktop
-rw------- 1 hacker hacker   8 Sep 29 10:34 PWN
-rw------- 1 root   hacker  60 Sep 23 13:47 d
-rw------- 1 hacker hacker 829 Sep 29 08:13 instructions
drwx------ 1 hacker hacker  12 Sep 25 06:24 leap
-rw------- 1 hacker hacker  95 Sep 29 08:13 myflag
lrwxrwxrwx 1 hacker hacker   5 Sep 26 10:09 not-the-flag -> /flag
-rw------- 1 root   hacker   0 Sep 29 12:33 pwn
-rw------- 1 hacker hacker 437 Sep 29 07:53 the-flag
drwx------ 1 hacker hacker   0 Sep 22 14:54 x
hacker@permissions~changing-permissions:~$ chmod ugo+r *
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{cTfDEcU4ZJUl7dKQfPKblRaMSbZ.QXzcjM1wiM4kjNzEzW}
```

## What I learned
*  each character of three represents the following :
  * r - user/group/other can read the file (or list the directory)
  * w - user/group/other can modify the files (or create/delete files in the directory)
  * x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
  * '-' nothing
* the rw-r--r-- permissions entry decodes to:

   - r: the user that owns the file (user hacker) can read it
   - w: the user that owns the file (user hacker) can write to it
   - -: the user that owns the file (user hacker) cannot execute it
   - r: users in the group that owns the file (group hacker) can read it
   - -: users in the group that owns the file (group hacker) cannot write to it
   - -: users in the group that owns the file (group hacker) cannot execute it
   - r: all other users can read it
   - -: all other users cannot write to it
   - -: all other users cannot execute it
* Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command. The basic usage for chmod is:

- ```chmod [OPTIONS] MODE FILE```
- You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.
- chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute.
- u+r, as above, adds read access to the user's permissions
- g+wx adds write and execute access to the group's permissions
- o-w removes write access for other users
- a-rwx removes all permissions for the user, group, and world.
  
## References
Did not use any references for this challenge.

# EXECUTABLE FILES
In this challenge, the /challenge/run program will give you the flag, but you must first make it executable! Remember your chmod, and get /challenge/run to tell you the flag.

## My solve
**Flag:** `pwn.college{MEYDQUz5FwxaOQVmlc2C0egoeFL.QXyEjN0wiM4kjNzEzW}`

1.I added execute access to all the users , groups , others using 'chmod' i.e ```chmod ugo+x /challenge/run``` .  
2.I ran ```/challenge/run``` to obtain the flag.  

```
hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{MEYDQUz5FwxaOQVmlc2C0egoeFL.QXyEjN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to using 'chmod' to add executable access to runa command.

## References 
Did not use any references for this challenge.  

# PERMISSION TWEAKING PRACTICE: 
This challenge will ask you to change the permissions of the /challenge/pwn file in specific ways a few times in a row. If you get the permissions wrong, the game will reset and you can try again. If you get the permissions right eight times in a row, the challenge will let you chmod /flag to make it readable for yourself :-) Launch /challenge/run to get started.

## My solve
**Flag:** `pwn.college{89YRU1wOLTgOxDuPBPeg_orMT2B.QXwEjN0wiM4kjNzEzW}`

1.I used */challenge/run* to start the rounds .  
2.In each of the rounds , I used chmod to change the permissions of '/challenge/pwn' in the way that can pass the rounds.  
3.After 8  rounds , I was able to change the permissions of /flag using 'chmod' and obtain the flag.

```
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod o-r /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-------
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod g-r /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": rw-------
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u-rw /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---rwxrwx
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod a-rwx,g+rwx,o+rwx /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": ---rwxrwx
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rw-rwxrwx
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u+rw /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": rw-rwxrwx
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rw-rwx-w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod o-rx /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": rw-rwx-w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-rwxrw-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod o+r /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rw-rwxrw-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-r-xr--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod g-w,o-wx /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
 cat /flag
pwn.college{89YRU1wOLTgOxDuPBPeg_orMT2B.QXwEjN0wiM4kjNzEzW}
```

## What I learned
I learbt how to use chmod more effectively .

## References 
Did not use any references for this challenge.  



# PERMISSION SETTING PRACTICE
This level extends the previous level by requesting more radical permission changes, which you will need = and ,-chaining to achieve.

## My solve
**Flag:** `pwn.college{4qz-Ob4HnhiwkQ-QEzbCsTcvtVR.QXzETO0wiM4kjNzEzW}`

1.I ran '/challenge/run' in order to obtain the instructions.  
2.Used my understanding of (u,g,o)=(-,r,w,x) to pass the rounds.  
3.Obtained the flag .

```bash
acker@permissions~permissions-setting-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr-----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=r,o=- /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rwxr-----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x-wxrw-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=wx,o=rw /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": r-x-wxrw-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w--w-r--
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=w,o=r /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": -w--w-r--
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr-x---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rx,o=- /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": rwxr-x---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-xr-x-w-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=rx,o=w /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": r-xr-x-w-
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrw-rw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rw,o=rw /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": rwxrw-rw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x-w----
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=w,o=- /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": r-x-w----
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr-xrw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rx,o=rw /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=r,g=r,o=r /flag
hacker@permissions~permissions-setting-practice:~$ cat /flag
pwn.college{4qz-Ob4HnhiwkQ-QEzbCsTcvtVR.QXzETO0wiM4kjNzEzW}
```

## What I learned
* In addition to adding and removing permissions, as in the previous level, chmod can also simply set permissions altogether, overwriting the old ones. This is done by using = instead of - or +. For example:

- u=rw sets read and write permissions for the user, and wipes the execute permission
- o=x sets only executable permissions for the world, wiping read and write
- a=rwx sets read, write, and executable permissions for the user, group, and world!

* chaining multiple modes to chmod with ,:

- ```chmod u=rw,g=r /challenge/pwn``` will set the user permissions to read and write, and the group permissions to read-only
- ```chmod a=r,u=rw /challenge/pwn``` will set the user permissions to read and write, and the group and world permissions to read-only
- Additionally, you can zero out permissions with -:
  ```chmod u=rw,g=r,o=- /challenge/pwn``` will set the user permissions to read and write, the group permissions to read-only, and the world permissions to nothing at all.

## References
No references.

# THE SUID BIT
Add the SUID bit to the /challenge/getroot program in order to spawn a root shell for you to cat the flag.

## My solve
**Flag:** `pwn.college{QYGbXcvBK4Ia-1EnXHtBgbcKtZy.QXzEjN0wiM4kjNzEzW}`

1.listed the permissions of '/challenge/getroot'.  
2.Using 'chmod u+s [file]' , I was able to add a SUID bit to /challenge/getroot.  
3.I ran '/challenge/getroot' to spawn a root shell and catted the flag in that shell .

```bash
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwxr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwsr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root!
Here is your shell...
root@permissions~the-suid-bit:~# cat /flag
pwn.college{QYGbXcvBK4Ia-1EnXHtBgbcKtZy.QXzEjN0wiM4kjNzEzW}
```

## What I learned
* the "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.
* The permissions of a file with SUID look like this:
  ```
  hacker@dojo:~$ ls -l /usr/bin/sudo
  -rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
  hacker@dojo:~$
  ```
 - The s part in place of the executable bit means that the program is executable with SUID. It means that, regardless of what user runs the program (as long as they have executable permissions), the program will execute as the owner user (in this case, the root user).
* As the owner of a file, you can set a file's SUID bit by using chmod:
  ```chmod u+s [program]```
* Giving the SUID bit to an executable owned by root can give attackers a possible attack vector to become root.
  
## References 
No references.

