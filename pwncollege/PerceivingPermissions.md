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
type what the challenge asks

## My solve
**Flag:** `pwn.college{helloworld}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
example triple ticks for bash
pwn.college{helloworld}
```

## What I learned
* Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.
* You can check what groups you are part of with the id command:
  ```
  hacker@dojo:~$ id
  uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
  hacker@dojo:~$
  ```
* 

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

