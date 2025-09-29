# REDIRECTING OUTPUT
In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

## My solve
**Flag:** `pwn.college{EILruJgFDa_Aj-bgSeu6aaXE_zl.QX0YTN0wiM4kjNzEzW}`

I used my understanding of the example given and used to output command 'echo' and the word 'PWN' to file 'COLLEGE' using '>' such that if I cat out COLLEGE , then the flag will be outputted.

```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{EILruJgFDa_Aj-bgSeu6aaXE_zl.QX0YTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new character called '>' which is used to redirect a word to another file such that upon reading the file , the output in the content in the word.

## References 
Did not use any references for this challenge.

# REDIRECTING MORE OUTPUT
In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will, of course, end up in the myflag file.

## My solve
**Flag:** `pwn.college{wt-BNkXSLnx6SbvdqezJRqClPEw.QX1YTN0wiM4kjNzEzW}`

Firstly as the flag is the output of /flag , I used '>' to redirect the output to the file 'myflag' such that after catting out 'myflag' , we obtain the flag.

```bash
hacker@piping~redirecting-more-output:~$ /challenge/run /flag > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{wt-BNkXSLnx6SbvdqezJRqClPEw.QX1YTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that you can redirect output of any command not only 'echo' and  

## References 
Add an references or videos you used while solving the challenge.
