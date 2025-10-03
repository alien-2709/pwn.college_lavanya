# LISTING PROCESSES
Renamed /challenge/run to a random filename, and this time made it so that you cannot ls the /challenge directory. But  also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag.

## My solve
**Flag:** `pwn.college{o6slPMKPntsxSAthhtxE23bS0VJ.QX4MDO0wiM4kjNzEzW}`

I used ps -ef to find the running process list in which I found out that '/challenge/run' has been renamed to '/challenge/12947-run-26928'. Thus , I ran the new renamed '/challenge/12947-run-26928' and obtained the flag.
```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 08:31 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 08:31 ?        00:00:00 /run/dojo/bin/sleep 6h
root         132       1  0 08:31 ?        00:00:00 /challenge/12947-run-26928
root         135     132  0 08:31 ?        00:00:00 sleep 6h
hacker       146       1  0 08:31 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       150     146  0 08:31 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       161     150  0 08:34 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/12947-run-26928
Yahaha, you found me! Here is your flag:
pwn.college{o6slPMKPntsxSAthhtxE23bS0VJ.QX4MDO0wiM4kjNzEzW}
Now I will sleep for a while (so that you could find me with 'ps').
```

## What I learned
Through this challenge I learnt to list running processes using the 'ps' command. Depending on whom you ask, ps either stands for "process snapshot" or "process status", and it lists processes. By default, ps just lists the processes running in your terminal.  
```
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```
In the above example, we have the shell (bash) and the ps process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).  
There are two ways to specify arguments:  
1."Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.  
2."BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.  
```
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```
You can see here that there are processes running for the initialization of the challenge environment (docker-init), a timeout before the challenge is automatically terminated to preserve computing resources (sleep 6h to timeout after 6 hours), the VSCode environment (several code-server helper processes), the shell (bash), and  ps -ef command. It's basically the same thing with ps aux:
```
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```

Both ps -ef and ps aux truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen. If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)! Alternatively, you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation.

## References 
Did not use any references for this challenge.  

# KILLING PROCESSES
In this challenge, /challenge/run will refuse to run while /challenge/dont_run is running! You must find the dont_run process and kill it. If you fail, pwn.college will disavow all knowledge of your mission.

## My solve
**Flag:** `pwn.college{gMZxEuHTnuYZpxOjzsygZOAwsgh.QXyQDO0wiM4kjNzEzW}`

First , I used 'ps -ef' and piped it into 'grep dont_run' in order to find the process and kill it. Next I used 'kill' followed by the number 136 which signifies the number for the process in the list and then rechecked the existence of the process. After running '/challenge/run' , I was able to obtain the flag.

```
hacker@processes~killing-processes:~$ ps -ef | grep dont_run
hacker       136     135  0 08:44 ?        00:00:00 /challenge/dont_run
hacker       164     153  0 08:44 pts/0    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ kill 136
hacker@processes~killing-processes:~$ ps -ef| grep dont_run
hacker       166     153  0 08:45 pts/0    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{gMZxEuHTnuYZpxOjzsygZOAwsgh.QXyQDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to terminate processes in Linux, this is done using the aggressively-named 'kill' command. With default options kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist. I also learnt about 'sleep' which is a program that simply hangs out for the number of seconds specified on the commandline.

## References 
Did not use any references for this challenge.   

# INTERRUPTING PROCESSES
/challenge/run will refuse to give you the flag until you interrupt it.

## My solve
**Flag:** `pwn.college{gwGVjp1jMKlzk7X55wzTrKbs-aZ.QXzQDO0wiM4kjNzEzW}`

First , I ran '/challenge/run' and wasnt able to obtain the flag unless Ctrl+C was used to interrupt it . Thus , I used Ctrl+C and was able to obtain the flag.

```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{gwGVjp1jMKlzk7X55wzTrKbs-aZ.QXzQDO0wiM4kjNzEzW}
```

## What I learned
I learnt how to interrupt a running process using Ctrl+C.

## References 
Did not use any references for this challenge.   


# KILLING MISBEHAVING PROCESSES.
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


# SUSPENDING PROCESSES
This level's run wants to see another copy of itself running and using the same terminal. How? Use the terminal to launch it, then suspend it, then launch another copy while the first is suspended.

## My solve
**Flag:** `pwn.college{sLV28kYGtCaW5e0wvhq54xcCavo.QX1QDO0wiM4kjNzEzW}`

First , I found the process list using 'ps -ef' . Next I ran /challenge/run followed by Ctrl+Z  to obtain the flag.
```
hacker@processes~suspending-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 09:15 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bi
root           7       1  0 09:15 ?        00:00:00 /run/dojo/bin/sleep 6h
hacker       123       0  0 09:15 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive
hacker       129       0  0 09:15 pts/1    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive
hacker       135     123  0 09:15 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       136     129  0 09:15 pts/1    00:00:00 /run/dojo/bin/bash --login
hacker       162       1  0 09:15 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/t
hacker       166     162  0 09:15 pts/2    00:00:00 /run/dojo/bin/bash --login
root         176     136  0 09:15 pts/1    00:00:00 bash /challenge/run
hacker       183     136  0 09:16 pts/1    00:00:00 ps -ef
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         176     136  0 09:15 pts/1    00:00:00 bash /challenge/run
root         184     136  0 09:16 pts/1    00:00:00 bash /challenge/run
root         186     184  0 09:16 pts/1    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{sLV28kYGtCaW5e0wvhq54xcCavo.QX1QDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge,I learnt how to suspend processes using Ctrl+Z.

## References
Did not use any references for this challenge.   


# RESUMING PROCESSES
his challenge's run needs you to suspend it, then resume it using Ctrl+Z followed by 'fg' command.

## My solve
**Flag:** `pwn.college{YM61TtWBjORaxXUm6naegsc-mKv.QX2QDO0wiM4kjNzEzW}`

1.I ran '/challenge/run' and suspended it by pressing Ctrl+Z.  
2.Next , I used the 'fg' command to resume the process and obtain the flag.
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{YM61TtWBjORaxXUm6naegsc-mKv.QX2QDO0wiM4kjNzEzW}
Don't forget to press Enter to quit me!

Goodbye!
```

## What I learned
I learnt how to resume suspended processes in the *foreground* using 'fg' command .

## References 
Did not use any references for this challenge.   

# Challenge Name
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





