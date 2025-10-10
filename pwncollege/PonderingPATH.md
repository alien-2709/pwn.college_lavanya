# THE PATH VARIABLE
In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command.

## My solve
**Flag:** `pwn.college{005QHU8pcP-Obu3p9Vh1bygk6OF.QX2cDM1wiM4kjNzEzW}`

1. Using echo $PATH to view the current path.
2. Setting PATH="" to remove the path so that bash cannot find the rm command.
3. running /challenge/run to obtain the flag .


```bash
hacker@path~the-path-variable:~$ echo $PATH
/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ echo $PATH

hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{005QHU8pcP-Obu3p9Vh1bygk6OF.QX2cDM1wiM4kjNzEzW}
```

## What I learned
* There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:
```
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
* Without a PATH, bash cannot find the ls command.
* In Linux, PATH is an environment variable that tells the shell where to look for executable programs when you type a command.

## References 
No references.

# SETTING PATH
This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory.

## My solve
**Flag:** `pwn.college{4r48hjGuutkoETClMSyKiSbocMX.QX1cjM1wiM4kjNzEzW}`

1. Setting PATH=/challenge/mpre_commands so that the command win can be invoked by its name.
2. Running /challenge/run win to obtain the flag.

```
hacker@path~setting-path:~$ PATH=/challenge/more_commands
hacker@path~setting-path:~$ /challenge/run win
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{4r48hjGuutkoETClMSyKiSbocMX.QX1cjM1wiM4kjNzEzW}
```

## What I learned
* PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:
```
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
* If you maintain useful scripts that you want to be able to launch by bare name. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:
```
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

## References 
No references. 

# FINDING COMMANDS
In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory.

## My solve
**Flag:** `pwn.college{I-lgJ2CYlIuBxY6RZf82h7wCEtK.01NzEzNxwiM4kjNzEzW}`

1. Using echo $PATH , first I listed out the different paths present.
2. Using 'which win' , I found the path of the win command , in whose directory , the flag file also exists.
3. I cd'd to the directory and found the flag file.
4. I catted it out to obtain the flag.

```bash
hacker@path~finding-commands:~$ echo $PATH
/run/challenge/bin:/run/dojo/bin:/bin:/challenge/paths/16873:/challenge/paths/19378:/challenge/paths/15925:/challenge/paths/15847:/challenge/paths/2624:/challenge/paths/2959:/challenge/paths/6323:/challenge/paths/10093:/challenge/paths/29609:/challenge/paths/5558:/challenge/paths/32671:/challenge/paths/13117:/challenge/paths/7056:/challenge/paths/7397:/challenge/paths/3923:/challenge/paths/12149:/challenge/paths/13270:/challenge/paths/12071:/challenge/paths/13956:/challenge/paths/19452:/challenge/paths/9647:/challenge/paths/16904:/challenge/paths/19224:/challenge/paths/15443:/challenge/paths/31881:/challenge/paths/15080:/challenge/paths/25792:/challenge/paths/13409:/challenge/paths/22390:/challenge/paths/8061:/challenge/paths/25722:/challenge/paths/9731:/challenge/paths/14458:/challenge/paths/26675:/challenge/paths/8885:/challenge/paths/18417:/challenge/paths/21516:/challenge/paths/25202:/challenge/paths/11307:/challenge/paths/24509:/challenge/paths/32708:/challenge/paths/14883:/challenge/paths/27063:/challenge/paths/1737:/challenge/paths/8672:/challenge/paths/5497:/challenge/paths/31654:/challenge/paths/488:/challenge/paths/16187:/challenge/paths/21000:/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~finding-commands:~$ which win
/challenge/paths/14883/win
hacker@path~finding-commands:~$ cd /challenge/paths/14883
hacker@path~finding-commands:/challenge/paths/14883$ ls
flag  win
hacker@path~finding-commands:/challenge/paths/14883$ cat flag
pwn.college{I-lgJ2CYlIuBxY6RZf82h7wCEtK.01NzEzNxwiM4kjNzEzW}
```

## What I learned
* When you type the name of a command, something inside one of the many directories listed in your $PATH variable is what actually gets executed .
* But which file, precisely? You can find out with the aptly-named *which* command:
```
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
* Mirroring what the shell does when searching for commands, which looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

## References 
No references.

# ADDING COMMANDS
In this challenge , win does not exist. Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it

## My solve
**Flag:** `pwn.college{UpVxikjfIkneE9QmkQ_5nee8F1R.QX2cjM1wiM4kjNzEzW}`

1. Create win file in the /home/hacker directory using touch.
2. Since its a shell script , I used cat > win << 's' to add the command cat /flag inside it.
3. Then as /challenge/run checks all the paths in PATH for the win file and executes only when it is found, we append the path of /home/hacker to PATH using PATH=$PATH:/home/hacker where : acts as the seperator.
4. Then as executable access is required by /challenge/run to execute win , I used chmod a+x win to do that.
5. Now , I invoked /challenge/run and obtained the flag.


```
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ cat win
hacker@path~adding-commands:~$ cat > win << 's'
> #!/bin/bash
> cat /flag
> s
hacker@path~adding-commands:~$ PATH=$PATH:/home/hacker
hacker@path~adding-commands:~$ chmod a+x win
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{UpVxikjfIkneE9QmkQ_5nee8F1R.QX2cjM1wiM4kjNzEzW}
```

## What I learned
* I learnt how to append a path to PATH using PATH=$PATH:/home/hacker.
* I learnt how to make /challenge/run access a file that was created in a path different from those contained in PATH.

## References 
No references.

# HIJACKING COMMANDS
this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

## My solve
**Flag:** `pwn.college{sXYdfwJFlg4p0fH86Le102Qgvu2.QX3cjM1wiM4kjNzEzW}`

1. Used cat to create a shell script rm storing the operation cat /flag.
2. Appended /home/hacker to the beginning of PATH so that its the first path that /challenge/run will check while executing.
3. added executable access to /challenge/run using chmod.
4. ran /challenge/run and obtained the flag.

```
hacker@path~hijacking-commands:~$ cat > rm << 's'
> #!/bin/bash
> cat /flag
> s
hacker@path~hijacking-commands:~$ PATH=/home/hacker:$PATH
hacker@path~hijacking-commands:~$ chmod a+x rm
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{sXYdfwJFlg4p0fH86Le102Qgvu2.QX3cjM1wiM4kjNzEzW}
hacker@path~hijacking-commands:~$
```
or
```
hacker@path~hijacking-commands:~$ cat > rm << 's'
> #!/bin/bash
> cat /flag
> s
hacker@path~hijacking-commands:~$ which cat
/run/dojo/bin/cat
hacker@path~hijacking-commands:~$ PATH=""
hacker@path~hijacking-commands:~$ PATH=/home/hacker:/run/dojo/bin:$PATH
hacker@path~hijacking-commands:~$ echo $PATH
/home/hacker:/run/dojo/bin:
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{sXYdfwJFlg4p0fH86Le102Qgvu2.QX3cjM1wiM4kjNzEzW}
```



## What I learned
* To hijack commands in linux terminal.
* I also learnt about the *nano* command and how to use it to create a shell script. 

## References 
No references.
