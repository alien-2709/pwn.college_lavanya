# INTRO TO COMMANDS
**In this level, invoke the hello command to get the flag.**

## My solve
**Flag:** `pwn.college{gVUfe3acVCniPYJIrbm4Retln43.QX3YjM1wiM4kjNzEzW}.`

I understood the structure of the command line which consists of command [format] [argument].Using the example given in the challenge itself , I understood that to invoke a command I need to type it in and press enter . I first tried whoami which let me know the username.

```
hacker@hello~intro-to-commands:~$ whoami
hacker
```
Then I invoked hello as stated in the challenged and was able to get the flag.
```
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{gVUfe3acVCniPYJIrbm4Retln43.QX3YjM1wiM4kjNzEzW}
```

## What I learned
From this challenge , I was able to learn how to invoke a command and how commands like variables are case sensitive.

## References 
Did not use any references for this challenge


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

# COMMAND HISTORY
This challenge injects a flag in the history of commands . Using the up arrow key , we must browse through the history and find the flag.

## My solve
**Flag:** `pwn.college{wOFaDJTrm0YS8oAVMLE7t_ik1aS.0lNzEzNxwiM4kjNzEzW}`

Using the up arrow , I scrolled through the history of commands that were typed in the terminal by me and eventually found the flag that was injected in it .

```
hacker@hello~command-history:~$ the flag is pwn.college{wOFaDJTrm0YS8oAVMLE7t_ik1aS.0lNzEzNxwiM4kjNzEzW}^C
```

## What I learned
From this challenge , I learnt what command history was and how to access it . We can access the command history by scrolling up and down using the arrow keys .I also learnt that the shell saves a history of *every* command we make.

## References 
Did not use any references for this challenge.
