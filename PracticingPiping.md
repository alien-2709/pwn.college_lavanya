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
Through this challenge , I learnt that you can redirect output of any command not only 'echo' and that  /challenge/run will still  print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out. i.e it communicates over standard error and prints flag over standard out.

## References 
Did not use any references for this challenge.

# APPENDING OUTPUT
To run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag.( The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag!)

## My solve
**Flag:** `pwn.college{UlG7YS7RL5kKhqa1FUgo2meaje_.QX3ATO0wiM4kjNzEzW}`

First , I redirected the output in truncation mode '>' , then the instructions were printed in the terminal . Next , I redirected the output using append mode '>>' ,which further printed the instructions and ran a few checks , and finally , I catted the file ' /home/hacker/the-flag ' in order to obtain the flag.

```bash
hacker@piping~appending-output:~$ /challenge/run pwn > /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ /challenge/run college >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{UlG7YS7RL5kKhqa1FUgo2meaje_.QX3ATO0wiM4kjNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```

## What I learned
Through this challenge , I learnt about a new mode called 'append' mode '>>' which is used to append the second half of the redirect to the first without overwriting it. If we use '>' i.e. in truncation mode then the second half wont be appended to the first half , it would be overwritten. I also learnt that a common use-case of output redirection is to save off some command results for later analysis. Often times, you want to do this in aggregate: run a bunch of commands, save their output, and grep through it later.

## References 
Did not use any references for this challenge. 


# REDIRECTING ERRORS
In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off.

## My solve
**Flag:** ` pwn.college{A6AxByYqAD49Nbsn0rcewVKVLSc.QX3YTN0wiM4kjNzEzW}`

Firstly , I used /challenge/run and redirected its output to myflag by using '>'/'1>' which is  F.D 1-A file descriptor for standard output , followed by redirecting the errors to instructions using '2>' which is F.D.2-A file descriptor for standard errors. Next , I catted out the instructions , leading to a few checks being run in the terminal and then I catted out myflag to obtain the flag.

```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat instructions
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!

[TEST] You should have redirected my stderr to instructions. Checking...

[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{A6AxByYqAD49Nbsn0rcewVKVLSc.QX3YTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge I learnt that just like standard output, you can also redirect the error channel of commands.  A File Descriptor (FD) is a number that describes a communication channel in Linux. We're already familiar with three:

FD 0: Standard Input  

FD 1: Standard Output  

FD 2: Standard Error  

When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:  


hacker@dojo:~$ echo hi > asdf  

hacker@dojo:~$ echo hi 1> asdf  


And To redirect errors we use '2>'.  

hacker@dojo:~$ echo hi 2> errors.log  



## References 
Did not use any references for this challenge.


# REDIRECTING INPUTS
Using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE , find the flag.

## My solve
**Flag:** `pwn.college{gU2G-hSjesVVm7tIBEqQvi5sJRb.QXwcTN0wiM4kjNzEzW}`

Firstly , I wrote 'COLLEGE' into the file 'PWN' using echo and '>' . Next , I redirected the PWN file to '/challenge/run' and thus obtaines the flag.

```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{gU2G-hSjesVVm7tIBEqQvi5sJRb.QXwcTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that just like you can redirect output from programs, you can redirect input to programs using a character '<'. 

## References 
Did not use any references for this challenge.


# GREPPING STORED RESULTS
1.Redirect the output of /challenge/run to /tmp/data.txt.  

2.This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.  

3.grep that for the flag!  


## My solve
**Flag:** `pwn.college{oTAK8Dk0HTbtqz1WwwWHQSgZ9M2.QX4EDO0wiM4kjNzEzW}`

Firstly , I redirected the output of '/challenge/run' to '/tmp/data.txt' which resulted in a series of instructions being printed in the terminal . Next, I grepped for the flag where I used 'pwn' as the SEARCH_STRING and was thus able to obtain the flag.

```bash
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements
hacker@piping~grepping-stored-results:~$ grep pwn /tmp/data.txt
pwns
pwn
pwning
pwn.college{oTAK8Dk0HTbtqz1WwwWHQSgZ9M2.QX4EDO0wiM4kjNzEzW}
pwned
```

## What I learned
Through this challenge , I learnt how to search through the resulting file using 'grep' after redirecting the output.

## References 
Did not use any references for this challenge.

# GREPPING LIVE OUTPUT
/challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag.

## My solve
**Flag:** `pwn.college{wgM0j3ci9SOt-55X5x1DcqyNmN-.QX5EDO0wiM4kjNzEzW}`

Firstly I used my understanding of the '|' operator (pipe) that discounts the need for storing results in a file and instead directly allows you to grep for the flag in one line . '/challenge/run flag ' is the left hand side which is the standard output which pipes into 'grep pwn' which is the standard input of the command.

```
hacker@piping~grepping-live-output:~$ /challenge/run flag| grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwning
pwned
pwns
pwn.college{wgM0j3ci9SOt-55X5x1DcqyNmN-.QX5EDO0wiM4kjNzEzW}
pwn
```

## What I learned
I learnt about the pipe operator '|' which discounts the need to store results in a file . The structure is such that standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.

## References 
Did not use any references for this challenge.


# GREPPING ERRORS
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
