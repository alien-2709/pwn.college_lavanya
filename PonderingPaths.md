# THE ROOT
To launch a terminal , invoke pwn by using its absolute path and capture the flag.

## My solve
**Flag:** `pwn.college{o-S97NEpqJvFYybo7VuC-oj73xV.QX4cTO0wiM4kjNzEzW}`

I used my understanding of the file system in linux and how an absolute path is one which starts with the root directory that is '/'. The flag is hidden in the root directory in a program called pwn and we need to invoke it using its absolute path i.e. /pwn. The following is my solve:

```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{o-S97NEpqJvFYybo7VuC-oj73xV.QX4cTO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about the file system in Linux and how to invoke a program through its absolute path .

## References 
Did not use any references for this challenge.

# Program and Absolute Paths
This challenge asks us to  find the flag through the path of *run challenge program* present in the root directory by using its absolute path .The correct absolute path to invoke the directory will capture the flag.

## My solve
**Flag:** `pwn.college{ILtD9BjRNGlPkNEjS4najKfezlG.QX1QTN0wiM4kjNzEzW}`

I was able to solve this challenge by using the understanding of absolute paths and how they start with a '/' called the root directory and like a tree with its roots , in order to find the absolute path , we go out to in i.e. from the root we go into the directories , then the subdirectories and so on .

```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{ILtD9BjRNGlPkNEjS4najKfezlG.QX1QTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I was able to learn how to invoke the absolute path in Linux using the terminal . The absolute path always begins with '/' and continues to the directories inside the root , leading to the path of the program.

## References 
Did not use any references for this challenge.

# POSITION THYSELF
This challenge requires the execution of the program  /challenge/run from a specific path which it will tell us.We must cd to that directory before rerunning the program.

## My solve
**Flag:** `pwn.college{sHIe1F6SC1Fj5uCRuPC8kOxHE_r.QX2QTN0wiM4kjNzEzW}`

I used my understanding of navigating directories in the Linux terminal by using the cd command and passing a path to it as an argument .I first ran /challenge/run in the home directory ~ which the terminal did not accept as correct and provided the new path where the program will execute that is */usr/bin*(executable files installed).

```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/bin directory.
Please use the `cd` utility to change directory appropriately.
```
Next I used cd command to navigate to that directory (*/usr/bin*) and then executed the /challenge/run program.

```
hacker@paths~position-thy-self:~$ cd /usr/bin
hacker@paths~position-thy-self:/usr/bin$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{sHIe1F6SC1Fj5uCRuPC8kOxHE_r.QX2QTN0wiM4kjNzEzW}
```
## What I learned
Through this challenge I learnt about a command called cd (change directory) which is used to navigate through directories in the Linux terminal by passing a path to it as the argument. I also learnt that ~ stands for the current working directory that is it shows the current path that your shell is located at.

## References 
Did not use any references for this challenge. 

# POSITION ELSEWHERE
This challenge requires the execution of the program  /challenge/run from a specific path which it will tell us.We must cd to that directory before rerunning the program.

## My solve
**Flag:** `pwn.college{0vzpEJ4jP60lqUZmxcdMeUEw5_C.QX3QTN0wiM4kjNzEzW}`

I used my understanding of navigating directories in the Linux terminal by using the cd command and passing a path to it as an argument .I first ran /challenge/run in the current directory ~ which the terminal did not accept as correct and provided the new path where the program will execute that is */usr/aarch64-linux-gnu/include/gnu*.

```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /usr/aarch64-linux-gnu/include/gnu directory.
Please use the `cd` utility to change directory appropriately.
```
Next I used cd command to navigate to that directory (*/usr/aarch64-linux-gnu/include/gnu*) and then executed the /challenge/run program.
```
hacker@paths~position-elsewhere:~$ cd /usr/aarch64-linux-gnu/include/gnu 
hacker@paths~position-elsewhere:/usr/aarch64-linux-gnu/include/gnu$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{0vzpEJ4jP60lqUZmxcdMeUEw5_C.QX3QTN0wiM4kjNzEzW}
```

## What I learned
Similar to the previous challenge ,through this challenge I learnt about the workings of the command called cd (change directory) which is used to navigate through directories in the Linux terminal by passing a path to it as the argument.

## References 
Did not use any references for this challenge .


# POSITION YET ELSEWHERE
This challenge requires the execution of the program  /challenge/run from a specific path which it will tell us.We must cd to that directory before rerunning the program.


## My solve
**Flag:** `pwn.college{AxLaQDVXieGY2If8oowOq6mUKJf.QX4QTN0wiM4kjNzEzW}`

I used my understanding of navigating directories in the Linux terminal by using the cd command and passing a path to it as an argument .I first ran /challenge/run in the current directory ~ which the terminal did not accept as correct and provided the new path where the program will execute that is */etc*(system configuration).

```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /etc directory.
Please use the `cd` utility to change directory appropriately.
```
Next I used cd command to navigate to that directory (*/etc*) and then executed the /challenge/run program.
```
hacker@paths~position-yet-elsewhere:~$ cd /etc
hacker@paths~position-yet-elsewhere:/etc$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{AxLaQDVXieGY2If8oowOq6mUKJf.QX4QTN0wiM4kjNzEzW}
```

## What I learned
Once again I learnt about navigation of directories using ths cd command by passing the path as an argument.

## References 
Did not use any references for this challenge.

# IMPLICIT RELATIVE PATHS, THROUGH /
For this challenge we'll need to run /challenge/run using a relative path while having a current working directory of /.

## My solve
**Flag:** `pwn.college{o8wnYv4H-Jo4HO-byIf0v7oEB72.QX5QTN0wiM4kjNzEzW}`

I first understood what relative paths were , how they do not start with '/'(root) and how they change relative to the directory in which you are in i.e. the current working directory.
Firstly I used pwd to find which directory I was in and found out it was the home directory i.e /home/hacker(~).

```
hacker@paths~implicit-relative-paths-from-:~$ pwd
/home/hacker
```
Next I navigated to the directory '/' using cd as stated in the challenge and then ran /challenge/run using its relative path i.e challenge/run as our current working directory (cwd) was '/'.
```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{o8wnYv4H-Jo4HO-byIf0v7oEB72.QX5QTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt what relative paths were . They are the paths that do not start with the root i.e. '/' and they change depending upon the current working directory. For example , if we wanted to access a file located at /tmp/a/filename and the cwd is /tmp , then the relative path would be a/filename.Thus I was able to understand implicit relative paths through '/'.

## References 
Did not use any references for this challenge.

# EXPLICIT RELATIVE PATHS , FROM /.
This challenge requires the usage of '.' in our relative paths.

## My solve
**Flag:** `pwn.college{8bvYEYZud1jxP0HqVs4kLgo1kUb.QXwUTN0wiM4kjNzEzW}`

To solve this challenge , I first used pwd to check which directory I was currently in. It showed me that i was in the home directory (/home/hacker) and thus I needed to navigate to the directory '/' using cd where the challenge program can run.

```
hacker@paths~explicit-relative-paths-from-:~$ pwd
/home/hacker
hacker@paths~explicit-relative-paths-from-:~$ cd /
```
Next , I used the knowledge of the implicit entry '.' (same directory ) and its usage in relative paths to capture the flag i.e. challenge/run is the same as ./challenge/run or ././challenge/run.
```
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8bvYEYZud1jxP0HqVs4kLgo1kUb.QXwUTN0wiM4kjNzEzW}
```

## What I learned
I first understood the usage of '.' (same directory) and '..'(parent directory) which are the two implicit entries that every directory in Linux has. Next, I learnt that as '.' stands for the same directory , its usage in absolute paths or relative paths will not affect it. For example if your current directory is '/' : in absolute paths: /challenge is the same as /challenge/. and in relative paths: challenge is the same as ./challenge. I also learnt about 'naked' paths which are paths which directly specify the directory to descend into from the current directory.

## References 
Did not use any references for this challenge.

# IMPLICIT RELATIVE PATH
In this challenge , we must explicitly use relative paths to launch run in (/challenge/run) i.e. we must tell Linux that we explicitly want to execute a program in the current directory using '.'.

## My solve
**Flag:** `pwn.college{o9yy4NGFiRO_6kwxdtS1PuwFHZC.QXxUTN0wiM4kjNzEzW}`

I first used pwd to find the present  directory and found that it was the home directory(/home/hacker), so I navigated to the root directory '/' using cd.

```
hacker@paths~implicit-relative-path:~$ pwd
/home/hacker
hacker@paths~implicit-relative-path:~$ cd /
```
Next , I navigated to the /challenge directory . Now , as Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path, we cannot just type run . Instead, we must tell Linux we explicitly want to launch run using '.'.
```
hacker@paths~implicit-relative-path:/$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{o9yy4NGFiRO_6kwxdtS1PuwFHZC.QXxUTN0wiM4kjNzEzW}
```

## What I learned
From this challenge, I learnt how Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path and how this acts as a safety measure as if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities.I also learnt how to explicitly use relative paths to launch run i.e. by using '.' to tell Linux explicitly that you want to launch the program in the current directory.

## References 
Did not use any references for this challenge.

# HOME SWEET HOME
In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

1.Your argument must be an absolute path.  

2.The path must be inside your home directory.  

3.Before expansion, your argument must be three characters or less.

You must specify your path as an argument to /challenge/run.

## My solve
**Flag:** `pwn.college{sBcWQpaARN_QWhUzgN3wvFZjyTC.QXzMDO0wiM4kjNzEzW}`

I used the path ~/d as an argument to /challenge/run to obtain a copy of the flag. I chose d as the argument must be three characters or less and ~/d makes the argument 3 characters. The following is my solve:

```
hacker@paths~home-sweet-home:~$ cd 
hacker@paths~home-sweet-home:~$ /challenge/run ~/d
Writing the file to /home/hacker/d!
... and reading it back to you:
pwn.college{sBcWQpaARN_QWhUzgN3wvFZjyTC.QXzMDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how every user has a home directory ,typically under /home and if your username is hacker then your home directory is /home/hacker. The home directory is where users store most of their personal files.Next , I understood that ~  is shorthand for /home/hacker and  whenever bash sees ~ provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. The expansion of ~ is an absolute path, and only the leading ~ is expanded i.e. ~ / ~ is expanded to /home/hacker/~ and not /home/hacker/home/hacker .I also learnt that the command cd uses ~ as the default destination.

## References 
Did not use any references for this challenge.





