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

# SCRIPTING WITH ARGUMENTS
For this challenge, you need to write a script at /home/hacker/solve.sh that:

1.Takes two arguments  
2.Outputs them in REVERSE order (second argument first, then the first argument)
- For example:
```
hacker@dojo:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@dojo:~$
```
- Once your script works correctly, run /challenge/run to get your flag

## My solve
**Flag:** `pwn.college{cmMJzfIJdagQbnLHbFKiJIN-Uab.0VNzMDOxwiM4kjNzEzW}`

1.Using cat , I first created a shell script called solve.sh that contains echo " $2 $1 " so that the result would be in reverse order .  
2.I ran 'bash solve.sh pwn college ' to obtain the reverse that is ' college pwn '.  
3.Next, I ran /challenge/run to obtain the flag.  

```bash
hacker@chaining~scripting-with-arguments:~$ cat > solve.sh << 's'
> echo "$2 $1"
> s
hacker@chaining~scripting-with-arguments:~$ bash solve.sh pwn college
college pwn
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{cmMJzfIJdagQbnLHbFKiJIN-Uab.0VNzMDOxwiM4kjNzEzW}
```

## What I learned
* The script can access these arguments using special variables:

- $1 contains the first argument ("hello")
- $2 contains the second argument ("world")
- $3 would contain the third argument (if there had been one)
- ...and so on
```
hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
```
## References 
No references

# SCRIPTING WITH CONDITIONALS
For this challenge, write a script at /home/hacker/solve.sh that:  


1. Takes one argument
2. If the argument is "pwn", output "college"
3. For any other input, output nothing

## My solve
**Flag:** `pwn.college{ghPLJP1Lz_DFPZ-FnAvRGK3hZoW.0lNzMDOxwiM4kjNzEzW}`

1.I made a shellscript called solve.sh which has a shebang '#!/bin/bash' .  
2.Then , using the conditionals ,  *if - then - fi* .
3.Then I ran /challenge/run to obtain the flag.

```
hacker@chaining~scripting-with-conditionals:~$ cat > solve.sh << 's'
> #!/bin/bash
> if [ "$1" == "pwn" ];then
> echo "college"
> fi
> s
hacker@chaining~scripting-with-conditionals:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-conditionals:~$ bash solve.sh foo
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{ghPLJP1Lz_DFPZ-FnAvRGK3hZoW.0lNzMDOxwiM4kjNzEzW}
```

## What I learned
* In bash, you can use if statements to make decisions:

```
if [ "$1" == "ping" ]
then
    echo "pong"
fi
```
* The above, in English, is if the first argument is "ping", print out "pong". The syntax is somewhat unforgiving for a few reasons. First, you must have spaces after if (if you're used to a language like C, this is different), after [, and before ]. Second, if, then, and fi must all be on different lines (or separated by semicolons); you can't lump them into the same statement. It's also a bit weird: instead of endif or end or something like that, the terminator of the if statement is fi (if backwards). 

## References 
No references. 

# SCRIPTING WITH DEFAULT CASES
For this challenge, write a script at /home/hacker/solve.sh that:  
- Takes one argument
- If the argument is "pwn", output "college"
- For any other input, output "nope"
Once your script works correctly, run /challenge/run to get your flag.

## My solve
**Flag:** `pwn.college{YRW-ZQjt2A6mkCgQWPAoMWpYBOx.01NzMDOxwiM4kjNzEzW}`

1.Made a shellscript called solve.sh .  
2.Using *if-else-fi* , I provided the appropriate instructions.  
3.After checkinf , I ran '/challenge/run' to obtain the flag.

```
hacker@chaining~scripting-with-default-cases:~$ cat > solve.sh << 's'
> #!/bin/bash
> if [ "$1" == "pwn" ];then
> echo "college"
> else
> echo "nope"
> fi
> s
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh foo
nope
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{YRW-ZQjt2A6mkCgQWPAoMWpYBOx.01NzMDOxwiM4kjNzEzW}
```

## What I learned
* The else clause executes when the if condition is false:
```
if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
```
* Note that the else doesn't have a condition --- it catches everything that didn't match previously. It also doesn't have a then statement. Finally, the fi goes after the else block to denote the end of the whole complex statement! It is also optional.

## References 
No references.

# SCRIPTING WITH MULTIPLE CONDITIONS
For this challenge, write a script at /home/hacker/solve.sh that:  

- Takes one argument
- If the argument is "hack", output "the planet"
- If the argument is "pwn", output "college"
- If the argument is "learn", output "linux"
- For any other input, output "unknown"
Once your script works correctly, run /challenge/run to get your flag.

## My solve
**Flag:** `pwn.college{cbihzL6J2i7VJDpuCKFv1xyc7BV.0FOzMDOxwiM4kjNzEzW}`

1. Using cat , I created a shellscript called solve.sh .
2. Starting with #!/bin/bash , I used *if-elif-else* to fit the conditions.
3. using '/challenge/run' , I found the flag.


```
hacker@chaining~scripting-with-multiple-conditions:~$ cat > solve.sh << 's'
> #!/bin/bash
> if [ "$1" == "pwn" ];then
> echo "college"
> elif [ "$1" == "hack" ];then
> echo "the planet"
> elif [ "$1" == "learn" ];then
> echo "linux"
> else
> echo "unknown"
> fi
> s
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{cbihzL6J2i7VJDpuCKFv1xyc7BV.0FOzMDOxwiM4kjNzEzW}
```

## What I learned
* to check multiple conditions, You can use elif (short for else if):
  ```
  if [ "$1" == "one" ]
  then
    echo "1"
  elif [ "$1" == "two" ]
  then
    echo "2"
  elif [ "$1" == "three" ]
  then
    echo "3"
  else
    echo "unknown"
  fi
  ```
* Note that you do need a then after the elif, just like the if. As before the else at the end catches everything that didn't match.

## References 
No references. 

# READING SHELL SCRIPTS
/challenge/run is a shell script that requires you to put in a secret password, but that password is hardcoded into the script iself! Read the script (using, say, cat), figure out the password, and get the flag.

## My solve
**Flag:** `pwn.college{0pEDcX5p71R_EauMjpUvCJwTrKj.0lMwgDOxwiM4kjNzEzW}`

1. catted out /challenge/run to read the password.
2. ran /challenge/run and entered the password given and obtained the flag.

```bash
hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"
fi
hacker@chaining~reading-shell-scripts:~$ /challenge/run
hack the PLANET
CORRECT! Your flag:
pwn.college{0pEDcX5p71R_EauMjpUvCJwTrKj.0lMwgDOxwiM4kjNzEzW}
```

## What I learned
I learnt how to read a shellscript using cat.

## References 
No references.
