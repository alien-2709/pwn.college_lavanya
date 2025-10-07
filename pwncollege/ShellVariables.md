# PRINTING VARIABLES
Print out the FLAG variable and solve this challenge.

## My solve
**Flag:** `pwn.college{IdjES6KweSDtzd9eGgJGLHVVOgf.QX3UTN0wiM4kjNzEzW}`

I used echo to print the value of the variable 'FLAG' by typing '$' before 'FLAG'.

```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{IdjES6KweSDtzd9eGgJGLHVVOgf.QX3UTN0wiM4kjNzEzW}
```

## What I learned
In this challenge , I learnt about how linux terminal can be used to program like other programming languages. Here 'echo' is used as 'printf' and $variable for the value.

## References 
Did not use any references for this challenge.

# SETTING VARIABLES
To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.

## My solve
**Flag:** `pwn.college{ctb5oFuS3ninz6owVhfFbvhIv6W.QX5UTN0wiM4kjNzEzW}`

Through my understanding of the examples given and taking into account the case sensitivity (including property of no spaces) of the variables , I was able to assign the variable 'PWN' the value of 'COLLEGE' using '=' and obtain the flag.

```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{ctb5oFuS3ninz6owVhfFbvhIv6W.QX5UTN0wiM4kjNzEzW}
```

## What I learned
Through this challenge I learnt about how to assign values to shell variables in shell script using the '='.Also , I learnt about how we should be careful to have no spaces between the words or else , the shell will take the variable as a command. 

## References 
Did not use any references for this challenge.

# MULTI-WORD VARIABLES
Set PWN to COLLEGE YEAH using quotes.

## My solve
**Flag:** `pwn.college{gK4onmV_vIApPi-Lf3ZM0CM21O9.QXwYTN0wiM4kjNzEzW}`

Using my understanding of variable assignment , I used quotes so that the spaces in the value of the variable is also assigned.

```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{gK4onmV_vIApPi-Lf3ZM0CM21O9.QXwYTN0wiM4kjNzEzW}
```

## What I learned
I learnt that in order to assign a value that contains spaces to a variable , we need to put it in quotes otherwise the shell wouldnt accept it.

## References 
Did not use any references for this challenge.

# EXPORTING VARIABLES
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run).

## My solve
**Flag:** `pwn.college{klO_CrNNywkFCoQMRQJ65MH7Llw.QXyYTN0wiM4kjNzEzW}`

1.First I exported the variable PWN and properly set it to COLLEGE.  
2.I set the value of COLLEGE as PWN but did not export it.  
3.Next , I invoked /challenge/run and obtained the flag.  


```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{klO_CrNNywkFCoQMRQJ65MH7Llw.QXyYTN0wiM4kjNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## What I learned
I learnt the following:  
1.by default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them.  
For e.g.    

```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
```
the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable.  
2.In order for it to recieve the value of VAR , we need to state it explicitly i.e we need to export the variables using 'export'.  
```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```



## References 
Did not use any references for this challenge.  

# PRINTING EXPORTED VARIABLES 
Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable

## My solve
**Flag:** `FLAG=pwn.college{g-TX3VDP6MkNu1YA8_pgAOgARRm.QX4UTN0wiM4kjNzEzW}`

I ran the env command that printed out every exported variable in my shell and found the flag.

```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=cd5246196dd17a8efd2bcfdc2f4f82a9799ae386f5b4d19aa0118ff9b498f95b
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{g-TX3VDP6MkNu1YA8_pgAOgARRm.QX4UTN0wiM4kjNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```

## What I learned
I learnt that 'env' command prints out all the exported variables .  

## References 
Did not use any references for this challenge.  

# STORING COMMAND OUTPUT
Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag.

## My solve
**Flag:** `pwn.college{QRAReCwoH1-uuTj28Ybyf0vc0Is.QX1cDN1wiM4kjNzEzW}`

First, I used my understanding of the examples given in order to assign the output of '/challenge/run' to the variable 'PWN'.Next , I printed it out using echo.

```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo "$PWN"
pwn.college{QRAReCwoH1-uuTj28Ybyf0vc0Is.QX1cDN1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about *Command Substitution* and how to use it to read the output of a command directly into a variable.

## References 
Did not use any references for this challenge.  


# READING INPUT
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE

## My solve
**Flag:** `pwn.college{4yKsMu2PB0PTtJvyMOHq0cch6TH.QX4cTN0wiM4kjNzEzW}`

I used my understanding of the concept of reading variables to solve this challenge . I used command 'read' along with an argument '-p' in order to specify a prompt and read the variable 'PWN'. Next , as per the challenge instructions , I gave 'PWN' the value of 'COLLEGE' and thus obtained the flag.

```
hacker@variables~reading-input:~$ read -p "INPUT: " PWN 
INPUT: COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{4yKsMu2PB0PTtJvyMOHq0cch6TH.QX4cTN0wiM4kjNzEzW}
```

## What I learned
I learnt how to use 'read' builtin to read a variable and assign a value to it.I also learnt that 'read' reads data from your standard input.

## References 
Did not use any references for this challenge.  


# READING FILES
Read /challenge/read_me into the PWN environment variable, and we'll give you the flag. The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command.

## My solve
**Flag:** `pwn.college{o49CYGab25WIKnV88a_7hCJa22z.QXwIDO0wiM4kjNzEzW}`
I used redirection i.e I redirected '/challenge/read_me' into the standard input of 'read', and so when 'read' reads into PWN, it reads from the file.

```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{o49CYGab25WIKnV88a_7hCJa22z.QXwIDO0wiM4kjNzEzW}
```

## What I learned
I learnt how to read a file through this challenge i.e. by using redirection instead of writing a long program using cat.

## References 
Did not use any references for this challenge.
