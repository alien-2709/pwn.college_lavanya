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

```
hacker@dojo:~$ echo hi > asdf  
hacker@dojo:~$ echo hi 1> asdf
```


And To redirect errors we use '2>'.  
```
hacker@dojo:~$ echo hi 2> errors.log
```



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
The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!

Try it now. Like the last level, this level will overwhelm you with output, but this time on standard error. grep through it to find the flag.

## My solve
**Flag:** `pwn.college{MSOqUL1_IeR2ujPh6d4YczbfWJw.QX1ATO0wiM4kjNzEzW}`

Firstly , through my understanding of the instructions given , I used a shell operator '>&' along with the standard error file descriptor (FD2) and then piped the now combined standard error and standard output in order to grep through the errors and find the flag.

```
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{MSOqUL1_IeR2ujPh6d4YczbfWJw.QX1ATO0wiM4kjNzEzW}
pwned
pwn
pwns
pwning
```

## What I learned
Through this challenge , I learnt how to grep through errors directly i.e. The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|).

## References 
Did not use any references for this challenge.


# FILTERING WITH GREP -V
/challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag.

## My solve
**Flag:** `pwn.college{ALOvuYQsI0QRj8WQAOTcdypKlEb.0FOxEzNxwiM4kjNzEzW}`

Through my understanding of grep -v which is used to filter out all the lines that we do not want , I output '/challenge/run' and piped it with 'grep -v DECOY' such that , the output in the terminal would be the real flag and all the fake flags have been filtered out using ' grep -v '.

```
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{ALOvuYQsI0QRj8WQAOTcdypKlEb.0FOxEzNxwiM4kjNzEzW}
```

## What I learned
I learnt about a new format to use 'grep' in that is followed by '-v'(invert match) .While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern. This is extremely helpful while needing to filter out a large amount of files containing the same characters and obtain the one that doesnt match.

## References 
Did not use any reference for this challenge.


# DUPLICATING PIPED DATA WITH TEE
 This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you.
 
## My solve
**Flag:** `pwn.college{o-1O5lH-_Akn2MqxgW00i-BvOkF.QXxITO0wiM4kjNzEzW}`

1.First I piped '/challenge/pwn' into '/challenge/college' which will lead to instructions being printed which ask for the usage of 'tee' to intercept the output of 'pwn' and figure out the code.  
2.I used 'tee pwn' to intercept .  
3.Next I catted out pwn in order to obtain the secret code.
4.I filled in the secret code as an argument to /challenge/pwn and thus was able to obtain the flag.

```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn|tee pwn|/challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "o-1O5lH-"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret o-1O5lH- | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{o-1O5lH-_Akn2MqxgW00i-BvOkF.QXxITO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about  The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line.
For e.g.  
```
hacker@dojo:~$ echo hi | tee pwn college  
hi  
hacker@dojo:~$ cat pwn  
hi  
hacker@dojo:~$ cat college  
hi
```

Here, by providing two files to tee, we ended up with three copies of the piped-in data: one to stdout, one to the pwn file, and one to the college file.

## References 
Did not use any references for this challenge.  


# PROCESS SUBSTITUTION FOR INPUT
Recall what you learned in the diff challenge from Comprehending Commands. In that challenge, you diffed two files. Now, you'll diff two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag.  


Use process substitution with diff to compare the outputs of these two programs and find your flag.  


## My solve
**Flag:** `pwn.college{k8sM_rItaOjYynOhOE49GWiv1jt.0lNwMDOxwiM4kjNzEzW}`

I recalled diff from the previous challenges and used it here along with process substitution in order to obtain the flag.

```
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
29a30
> pwn.college{k8sM_rItaOjYynOhOE49GWiv1jt.0lNwMDOxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to hook input and output of programs to arguments of commands. This is done using Process Substitution. For reading from a command (input process substitution), use <(command). When you write <(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:  

```
hacker@dojo:~$ echo <(echo hi)  
/dev/fd/63  
hacker@dojo:~$  
```
bash replaced <(echo hi) with the path of the named pipe (/dev/fd/63)  file that's hooked up to the command's output. While the command is running, reading from this file will read data from the standard output of the command. Typically, this is done using commands that take input files as arguments. 

you can specify this multiple times:  

```
hacker@dojo:~$ echo <(echo pwn) <(echo college)  
/dev/fd/63 /dev/fd/64  
hacker@dojo:~$ cat <(echo pwn) <(echo college)  
pwn  
college
```


## References 
Did not use any references for this challenge.

# WRITING TO MULTIPLE PROGRAMS
In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands.

## My solve
**Flag:** `pwn.college{c7YVNziHcP9KMm8RDAivLMSYmSk.QXwgDN1wiM4kjNzEzW}`

I first ran '/challenge/hack' , the output of which is piped into '/challenge/the' where the usage of the 'tee' command duplicates its output as input , so the stdin goes into '/challenge/the' and the stdout goes into '/challenge/planet'.Thus we are able to obtain the flag.

```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{c7YVNziHcP9KMm8RDAivLMSYmSk.QXwgDN1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that for writing to a command (output process substitution), use >(command). If you write an argument of >(rev), bash will run the rev command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary named pipe file. When commands write to this file, the data goes to the standard input of the command  

```
hacker@dojo:~$ echo Hello | rev  
olleH  
 hacker@dojo:~$ echo Hello | tee >(rev)  
Hello  
olleH
```

Above, the following sequence of events took place:  


1.bash started up the rev command, hooking a named pipe (presumably /dev/fd/63) to rev's standard input  

2.bash started up the tee command, hooking a pipe to its standard input, and replacing the first argument to tee with /dev/fd/63. tee never even saw the argument >(rev); the shell substituted it before launching tee.  

3.bash used the echo builtin to print Hello into tee's standard input  

4.tee read Hello, wrote it to standard output, and then wrote it to /dev/fd/63 (which is connected to rev's stdin)
rev read Hello from its standard input, reversed it, and wrote olleH to standard output.  


## References 
Did not use any references for this challenge.  


# SPLIT-PIPING STDERR AND STDOUT
In this challenge, you have:  


1./challenge/hack: this produces data on stdout and stderr  

2./challenge/the: you must redirect hack's stderr to this program  

3./challenge/planet: you must redirect hack's stdout to this program  

Go get the flag  


## My solve
**Flag:** `pwn.college{g8SDnPCHWF9iL36IR-TwWr3Ms4m.QXxQDM2wiM4kjNzEzW}`

In this challenge , I first redirected the output of '/challenge/hack' to '/challenge/planet' using '>'. So , '>(/challenge/planet)' sends the stdout of '/challenge/hack' into '/challenge/planet'.Next, I redirected the standard errors of '/challenge/hack' to '/challenge/the' using 2> . So, '2>(/challenge/the)' sends the stderr of '/challenge/hack' into '/challenge/the'. Thus , the flag is obtained.

```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{g8SDnPCHWF9iL36IR-TwWr3Ms4m.QXxQDM2wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt the cumulative use of the redirection operations and file descriptors i.e. (>(),2>).

## References 
Did not use any references for this challenge.


# NAMED PIPES
You'll need to create a /tmp/flag_fifo file and redirect the stdout of /challenge/run to it. If you're successful, /challenge/run will write the flag into the FIFO.  

## My solve
**Flag:** `pwn.college{8onpZMj_mvZKP3_HZ-BjB3XRAa-.01MzMDOxwiM4kjNzEzW}`

1.Using mkfifo ,I created a persistent named pipe called '/tmp/flag_fifo'.  
2.Next, Using '>' , I redirected the output of '/challenge/run' to '/tmp/flag_fifo'.  
3.Next , I catted out '/tmp/flag_fifo' to obtain the flag.  


```bash
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!


You did not redirect /challenge/run's stdout to /tmp/flag_fifo!
hacker@piping~named-pipes:~$ cat /tmp/flag_fifo
You've correctly redirected /challenge/run's stdout to a FIFO at 
/tmp/flag_fifo! Here is your flag:
pwn.college{8onpZMj_mvZKP3_HZ-BjB3XRAa-.01MzMDOxwiM4kjNzEzW}
```

## What I learned
Through this challenge I learnt the following:  
1.You can  create your own persistent named pipes that stick around on the filesystem! These are called FIFOs, which stands for First (byte) In, First (byte) Out.  

2.These are created by using the *mkfifo* command which created a persistent named pipe which starts with a 'p' unlike '-' in other files.  

3.Advantages of fifo:   
a.You control where FIFOs are created  

b.They persist until you delete them.  

c.Any process can write to them by path (e.g., echo hi > my_pipe)  

d.You can see them with ls and examine them like files  

4.Disadvantage: One problem with FIFOs is that they'll "block" any operations on them until both the read side of the pipe and the write side of the pipe are ready.  

5.Key differences:  
a.No disk storage: FIFOs pass data directly between processes in memory - nothing is saved to disk.  

b.Ephemeral data: Once data is read from a FIFO, it's gone (unlike files where data persists)  

c.Automatic synchronization: Writers block until the readers are ready, and vice-versa. This is actually useful! It provides automatic synchronization. Consider the example above: with a FIFO, it doesn't matter if cat myfifo or echo pwn > myfifo is executed first; each would just wait for the other. With files, you need to make sure to execute the writer before the reader.  

d.Complex data flows: FIFOs are useful for facilitating complex data flows, merging and splitting data in flexible ways, and so on. For example, FIFOs support multiple readers and writers.  



## References 
Did not use any references for this challenge.  






