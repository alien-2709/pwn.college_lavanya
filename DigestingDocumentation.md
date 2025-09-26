# LEARNING FROM DOCUMENTATION
The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:  

Welcome to the documentation for /challenge/challenge. To properly run this program, you will need to pass it the argument of --giveflag. 

## My solve
**Flag:** `pwn.college{0YWrrjgOAAlCwPrqR-2pkezuU06.QX0ITO0wiM4kjNzEzW}`

According to the documentation , I used '--giveflag' as the argument for the program '/challenge/challenge' in order to obtain the flag.

```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{0YWrrjgOAAlCwPrqR-2pkezuU06.QX0ITO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that documentation is just a way to figure out how to use all these programs and a specific case of that is figuring out what arguments to specify on the command line. For eg. 'ls'alone does not list all files (including hidden files) , in order for it to do so , 'ls -a' is used where '-a' is the argument used to show all hidden files.

## References 
Did not use any references for this challenge.


# LEARNING COMPLEX USAGE
| Welcome to the documentation for /challenge/challenge! This program allows you to print arbitrary files to the terminal, when given the --printfile argument. The argument to the --printfile argument is the path of the flag to read. For example, /challenge/challenge --printfile /challenge/DESCRIPTION.md will print out the description of the level!|

Given that documentation, go get the flag!

## My solve
**Flag:** `pwn.college{E3iyryyUDyOFhqD77-xAC4eo5kx.QX1ITO0wiM4kjNzEzW}`

As the documentation stated , I first used '--printfile' as the first argument and '/flag' as the second argument of '/challenge/challenge' in order to obtain the flag.

```
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{E3iyryyUDyOFhqD77-xAC4eo5kx.QX1ITO0wiM4kjNzEzW}
```

## What I learned
In this challenge , I learnt that certain commands are very complex and may require more than one argument . One example of this is 'find -name /file ' where '-name' and '/file' are both arguments . Similarly in this challenge as well , We used two arguments '--printfile' and '/flag'.

## References 
Did not use any references for  this challenge.

# READING MANUALS
The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for challenge.

## My solve
**Flag:** `pwn.college{sNUHva0YtfIRkT9O34ZGYYdNo8i.QX0EDO0wiM4kjNzEzW}`

Firstly , I accessed the man page of challenge by using 'man challenge' . In the man page , There was a lot of information about challenge and the different arguments to use . An argument called '--svatfk NUM '(where NUM=093) stood out as it had the option of print the flag. 

```
hacker@man~reading-manuals:~$ man challenge

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --svatfk NUM
              print the flag if NUM is 093

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                        May 2024                                                       CHALLENGE(1)
 Manual page challenge(1) line 2/31 (END) (press h for help or q to quit)

```
Thus , I used /challenge/challenge followed by 'svatfk 093' as an argument in order to obtain the flag .

```
hacker@man~reading-manuals:~$ /challenge/challenge --svatfk 093
Correct usage! Your flag: pwn.college{sNUHva0YtfIRkT9O34ZGYYdNo8i.QX0EDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new command called 'man' . 'man' is short for manual and will display (if available) the manual of the command you pass as an argument.
I also learnt the important sections of a man page of a command :  
1.NAME  

	This gives the name (and short description) of the command or
	concept discussed by the page.

2.SYNOPSIS  

	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

3.DESCRIPTION  

	Details of the command or concept, with detailed descriptions
	of the various options.

4.SEE ALSO  

	Other man pages or online resources that might be useful.

I also learnt that you can scroll around the manpage with your arrow keys and PgUp/PgDn. When you're done reading the manpage, you can hit q to quit and manpages are stored in a centralized database

## References 
Did not use any references for this challenge.


# SEARCHING MANUALS
By reading the man page of challenge , find the flag.

## My solve
**Flag:** `pwn.college{MvVDHWOvzA48ah6OcU6pYwT-1pM.QX1EDO0wiM4kjNzEzW}`

I first read the man page of challenge by using the 'man' command followed by 'challenge'. This gave rise to a manual related to challenge having all the required information. 
```
hacker@man~searching-manuals:~$ man challenge
```
In the man page , I used '/' to search for 'flag ' i.e /flag which led me to the argument '--awfpee' upon the usage of which , the flag was obtained.

 ```
  --awfpee  This argument will give you the flag!
hacker@man~searching-manuals:~$ /challenge/challenge --awfpee
Initializing...
Correct usage! Your flag: pwn.college{MvVDHWOvzA48ah6OcU6pYwT-1pM.QX1EDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about the different ways to traverse through a man page i.e.  

1.Scroll man pages with the arrow keys (and PgUp/PgDn) .    


2.Search with /. Search backwards with ?.  


3.You can hit n to go to the next result and N to go to the previous result. 

## References 
Did not use any references for this challenge.


# SEARCHING FOR MANUALS
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


# HELPFUL PROGRAMS
 This challenge involves practice reading a program's documentation with --help.

## My solve
**Flag:** `pwn.college{M3iYx7e2Wp_V7xLWvtYbBhVNd5A.QX3IDO0wiM4kjNzEzW}`

Firstly , I used the argument '--help' along with /challenge/challenge in order to obtain help and more information about how to obtain the flag. Next , through help I found out that in order to obtain the flag , I must get the secret value by using the argument '-p' .The secret value as obtained was 372 which is filled in the argument -g GIVE_THE_FLAG ( where GIVE_THE_FLAG = 372). Thus , I was able to obtain the flag.

```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 372
hacker@man~helpful-programs:~$ /challenge/challenge -g 372
Correct usage! Your flag: pwn.college{M3iYx7e2Wp_V7xLWvtYbBhVNd5A.QX3IDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that some programs don't have a man page, but might tell you how to run them if invoked with a special argument, this argument is called --help / -h /-? / help or other esosteric values like /?.

## References 
Did not use any references for this challenge.


# HELPFUL BULLETINS
This challenge's challenge command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it.

## My solve
**Flag:** `pwn.college{kMODx-VO7TCSlxVNHGEFDN_Z-_e.QX0ETO0wiM4kjNzEzW}`

Through my understanding of the builtin 'help' . I first used it followed by the shell builtin 'challenge' to obtain the secret value and option to find the flag . After finding out the secret value which was "kMODx-VO" , I used the argument --secret SECRET(where SECRET =kMODx-VO) in order to obtain the flag.

```
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "kMODx-VO".
hacker@man~help-for-builtins:~$ challenge --secret kMODx-VO
Correct! Here is your flag!
pwn.college{kMODx-VO7TCSlxVNHGEFDN_Z-_e.QX0ETO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt what builtins were .Some commands ,rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help. 

## References 
Did not use any references for this challenge.

