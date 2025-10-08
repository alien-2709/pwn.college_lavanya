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

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash

```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.  

# Challenge Name
type what the challenge asks

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

# Challenge Name
type what the challenge asks

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

# Challenge Name
type what the challenge asks

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

