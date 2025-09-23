# CAT:NOT THE PET ,BUT THE COMMAND
The challenge is to read the copied file 'flag" in the home directory by using cat.

## My solve
**Flag:** `pwn.college{0566YnK-NAFU_MT6FzDsk_xn56U.QXxcTN0wiM4kjNzEzW}`

I used my understanding of cat and read the file flag stored in the home directory by using cat flag.

```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{0566YnK-NAFU_MT6FzDsk_xn56U.QXxcTN0wiM4kjNzEzW}
```

## What I learned
A new command I learnt from this challenge is cat and how it is used for reading out files . I learnt how cat will concatenate multiple files if multiple arguments are provided and if there are no arguments , it will read from the terminal input and output it.

## References 
Did not use any references for this challenge.

# CATTING ABSOLUTE PATHS
The challenge is to read a file 'flag' using cat at its absolute path.

## My solve
**Flag:** `pwn.college{IDPkDw3m-Cw4_QEHGY8jK9ut8cx.QX5ETO0wiM4kjNzEzW}`

Using my understanding from the given example , I used cat to read the flag file stored in the '/' directory by using its absolute path (/flag) as an argument.

```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{IDPkDw3m-Cw4_QEHGY8jK9ut8cx.QX5ETO0wiM4kjNzEzW}
```

## What I learned
In this challenge , I learnt how to read a file using cat by using the file's absolute path.

## References 
Did not use any references for this challenge.

# MORE CATTING PRACTICE
This challenge involves using cat to find the flag which is placed in a directory that you cannot use cd to navigate to i.e. we must use the file's absolute path.

## My solve
**Flag:** `pwn.college{0z-qGpq8inopfW4WLDBhw7-1WGe.QXwITO0wiM4kjNzEzW}`

To solve this challenge , I used my understanding of cat and made the absolute path of the file 'flag' as the argument for cat thus being able to retrieve it without using cd to navigate to that directory.

```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /lib/systemd/system-sleep/flag. Go cat it out **without** cding 
into that directory!
hacker@commands~more-catting-practice:~$ cat /lib/systemd/system-sleep/flag
pwn.college{0z-qGpq8inopfW4WLDBhw7-1WGe.QXwITO0wiM4kjNzEzW}
```

## What I learned
I learnt how to read a file using cat without using cd to navigate to that directory.

## References 
Did not use any references for this challenge.





