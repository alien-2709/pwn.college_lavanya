# INTRO TO ARGUMENTS
In this challenge, to get the flag, we must run the hello command  with a single argument of hackers.

## My solve
**Flag:** `pwn.college{084L-wht08ZVIDPbOkuadrF5JjZ.QX4YjM1wiM4kjNzEzW}`

For this challenge , I first understood that a command line consists of a command-space-arguments. There can be multiple arguments as shown in the example. When you type a line of text and hit enter , the shell parses your input into a command and its arguments . Looking at the example of echo give by the challenge . I ran the hello command followed by the hackers argument as stated in the challenge to obtain the flag.
```
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{084L-wht08ZVIDPbOkuadrF5JjZ.QX4YjM1wiM4kjNzEzW}
```

## What I learned
Through this challenge , I was able to learn about command and its arguments , how there can be multiple arguments to a single command and how the shell parses your input into a command and its arguments.
I was also able to learn about the command 'echo' and how it echoes the arguments back into the terminal.(sort of like printf in c )


## References 
Did not use any references for this challenge.
