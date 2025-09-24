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

# GREPPING FOR A NEEDLE IN THE HAYSTACK.
Using grep , search for  the flag (which begins with pwn.college) in the file /challenge/data.txt where thousands of lines of text are present.

## My solve
**Flag:** `pwn.college{4xKVwWO89Ej5PtgtSF7e8Aa0Sz1.QX3EDO0wiM4kjNzEzW}`

For this challenge , I first understood how to use grep to read big files that cannot be read out by cat . I used *grep SEARCH_STRING path/to/file* , in order to search for pwn.college in the big file /challenge/data.txt.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{4xKVwWO89Ej5PtgtSF7e8Aa0Sz1.QX3EDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new command called grep which is used to read out required sections of files that are so big that cat cannot be used. One of the ways to use grep is *grep SEARCH_STRING path/to/file* where grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

## References 
Did not use any references for this challenge.

# COMPARING FILES
There are two files in /challenge:

1./challenge/decoys_only.txt contains 100 fake flags.  

2./challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag.  

Use diff to find what's different between these files and get your flag.

## My solve
**Flag:** ` pwn.college{kb350L8jbCYKPJwp1P7pyQd94Yo.01MwMDOxwiM4kjNzEzW}`

Through my understanding of diff as shown in the example , I used diff followed by the two files as arguments such that the difference between them will be given as output in the terminal. This output would be the flag as it is the only element thats different between the two files full of fake flags .Thus , I was able to obtain the flag.

```
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
66a67
> pwn.college{kb350L8jbCYKPJwp1P7pyQd94Yo.01MwMDOxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about the usage of diff to compare two files and how the difference between the files will be given as output in the form of 

## References 
Add an references or videos you used while solving the challenge.

# LISTING FILES
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


# TOUCHING FILES
type what the challenge asks

## My solve
**Flag:** `pwn.college{Mj_doy3xeTcNUjxtasnZUNUX5hX.QXwMDO0wiM4kjNzEzW}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
hacker@commands~touching-files:~$ pwd
/home/hacker
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{Mj_doy3xeTcNUjxtasnZUNUX5hX.QXwMDO0wiM4kjNzEzW}
```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.


# REMOVING FILES
type what the challenge asks

## My solve
**Flag:** `pwn.college{oAVOEM_HAfS3kiD4gSa0-YVlDU9.QX2kDM1wiM4kjNzEzW}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
hacker@commands~removing-files:~$ ls
Desktop  d  delete_me  x
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{oAVOEM_HAfS3kiD4gSa0-YVlDU9.QX2kDM1wiM4kjNzEzW}
```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.

# MOVING FILES
type what the challenge asks

## My solve
**Flag:** `pwn.college{YwNUQbXpsY2MprdUWhN6Sk_MtFG.0VOxEzNxwiM4kjNzEzW}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{YwNUQbXpsY2MprdUWhN6Sk_MtFG.0VOxEzNxwiM4kjNzEzW}
```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.

# HIDDEN FILES
type what the challenge asks

## My solve
**Flag:** ``

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
example triple ticks for bash
pwn.college{helloworld}
```

## What I learned
Explain what new topics you learned/information you gained through this challenge.

## References 
Add an references or videos you used while solving the challenge.









