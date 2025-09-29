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
