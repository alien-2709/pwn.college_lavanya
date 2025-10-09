# CHAINING WITH SEMICOLONS
In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.

## My solve
**Flag:** `pwn.college{g3lhhDFGuEwdCpb3pxNauiEE1oe.QX1UDO0wiM4kjNzEzW}`

Using *;* to seperate '/challenge/pwn' and '/challenge/college'.

```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn;/challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{g3lhhDFGuEwdCpb3pxNauiEE1oe.QX1UDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge,I learnt that the way to chain commands is by using *;*. In most contexts, *;* separates commands in a similar way to how Enter separates lines. 

## References 
No references. 

# BUILDING ON SUCCESS
type what the challenge asks

## My solve
**Flag:** `pwn.college{0rzzKoCFoi_SiP8jU3JfmKucFxN.0lM0MDOxwiM4kjNzEzW}`

1.I ran '/challenge/first-success' and '/challenge/second' wothout using && which showed an error .  
2.Thus, I ran the two commands in one line sepearated by an && and was able to obtain the flag.

```bash
hacker@chaining~building-on-success:~$ /challenge/first-success
hacker@chaining~building-on-success:~$ /challenge/second
Error: /challenge/first-success must be successfully chained with
/challenge/second using &&
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{0rzzKoCFoi_SiP8jU3JfmKucFxN.0lM0MDOxwiM4kjNzEzW}
```

## What I learned
* The && operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0). This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

- Here's the syntax:
  ```
  hacker@dojo:~$ command1 && command2
  ```
  - This means: "Run command1, and IF it succeeds, then run command2."
  
## References 
No references

# HANDLING FAILURE
In this challenge, you need to chain /challenge/first-failure and /challenge/second using the || operator.

## My solve
**Flag:** `pwn.college{Yy746SsZm-ov9K-VL-oLvdKm40M.01M0MDOxwiM4kjNzEzW}`

Using || , I chained '/challenge/first-failure' and '/challenge/second' to obtain the flag.

```
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{Yy746SsZm-ov9K-VL-oLvdKm40M.01M0MDOxwiM4kjNzEzW}
```

## What I learned
* the || operator allows you to run a second command only if the first command fails (exits with a non-zero code). This is called the "OR" operator because either the first command succeeds OR the second command will run.

- Here's the syntax:

```hacker@dojo:~$ command1 || command2```
- This means: "Run command1, and IF it fails, then run command2."
* The || operator is super useful for providing fallback commands or error handling.

## References 
No references

# YOUR FIRST SHELL SCRIPT
Now, it's your turn! Same as last level, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash.

## My solve
**Flag:** `pwn.college{4nisrj-Fm9FstsxcEqDXAi_6IVV.QXxcDO0wiM4kjNzEzW}`

1.Using cat , I created a shell script called 'x.sh' and have it store commands until 's' is typed.  
2.I typed the commands one after the other and at the end typed 's' to stop.  
3.I ran 'x.sh' with bash to obtain the flag.

```
hacker@chaining~your-first-shell-script:~$ cat > x.sh << 's'
> /challenge/pwn
> /challenge/college
> s
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{4nisrj-Fm9FstsxcEqDXAi_6IVV.QXxcDO0wiM4kjNzEzW}
```

## What I learned
* We can create a shell script called pwn.sh (by convention, shell scripts are frequently named with a sh suffix):

```
echo COLLEGE > pwn
cat pwn
```
* And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.

```
hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
```
* You can see that the shell script executed both commands, creating and printing the pwn file.

## References 
No references.  

# REDIRECTING SCRIPT OUTPUT
You need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command.

## My solve
**Flag:** `pwn.college{I14FcKh_XMX6geSX-0FkCV1SBxi.QX4ETO0wiM4kjNzEzW}`

1.Created a shell script called x.sh and stored the commands in it.  
2.Piped the output of x.sh into /challenge/solve to obtain the flag.

```
hacker@chaining~redirecting-script-output:~$ cat > x.sh << 's'
> /challenge/pwn
> /challenge/college
> s
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{I14FcKh_XMX6geSX-0FkCV1SBxi.QX4ETO0wiM4kjNzEzW}
```

## What I learned
* As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did for commands in piping.
  ```
  hacker@dojo:~$ cat script.sh
  echo PWN
  echo COLLEGE
  hacker@dojo:~$ bash script.sh > output
  hacker@dojo:~$ cat output
  PWN
  COLLEGE
  hacker@dojo:~$
  ```
* All of the various redirection methods work: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.

## References 
No references 

# EXECUTABLE SHELL SCRIPTS
Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash.

## My solve
**Flag:** `pwn.college{IQY3viRxkXKjXPyvJ0bS5I3jpTR.QX0cjM1wiM4kjNzEzW}`

1.Created a shellscript called x.sh that invokes '/challenge/solve'.  
2.Next , using chmod , I made it executable by the user, group and world.  
3.I ran ./x.sh to obtain the flag.

```bash
hacker@chaining~executable-shell-scripts:~$ cat > x.sh << 's'
> /challenge/solve
> s
hacker@chaining~executable-shell-scripts:~$ chmod ugo+x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{IQY3viRxkXKjXPyvJ0bS5I3jpTR.QX0cjM1wiM4kjNzEzW}
```

## What I learned
* If your shell script file is executable (recall File Permissions), you can simply invoke it via its relative or absolute path! For example, if you create script.sh in your home directory and make it executable, you can invoke it via /home/hacker/script.sh or ~/script.sh or (if your working directory is /home/hacker) ./script.sh.

## References 
No references.

# UNDERSTANDING SHEBANGS
For this challenge, create a script at /home/hacker/solve.sh that has a proper shebang and outputs "hack the planet". Remember to make it executable, then run /challenge/run to verify your script works correctly.

## My solve
**Flag:** `pwn.college{kvTupfrPxt8ge0Ncw7sgPf6Kmis.0VOzMDOxwiM4kjNzEzW}`

1.Made a shellscript called solve.sh with the appropraite shebang and command.  
2.Added executable access to all using chmod a+x solve.sh.
3.ran /challenge/run to obtainthe flag.

```bash
hacker@chaining~understanding-shebangs:~$ cat > solve.sh << 's'
> #!/bin/bash
> echo "hack the planet"
> s
hacker@chaining~understanding-shebangs:~$ chmod a+x solve.sh
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{kvTupfrPxt8ge0Ncw7sgPf6Kmis.0VOzMDOxwiM4kjNzEzW}
```

## What I learned
* When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a .sh extension, or your Python scripts with a .py extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.
* if the program file starts with the characters #! (often termed a "shebang"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.

- Consider this shell script:

```
#!/bin/bash

echo "Hello Hackers!"
```
- This can be executed as:

```
hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
```
* When ./script.sh was executed, Linux opened the file, read the first line, extracted /bin/bash as the interpreter, and executed /bin/bash ./script.sh to launch the script!

* Note, the shebang line must be the VERY FIRST line of the file .
* Common shebangs you might see:

- #!/bin/bash for bash scripts
- #!/usr/bin/python3 for Python scripts
- #!/bin/sh for POSIX shell scripts --- this is a more primitive predecessor to bash with fewer features, but more compatibility to non-Linux systems!

## References 
No references.
