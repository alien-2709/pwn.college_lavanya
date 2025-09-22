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



