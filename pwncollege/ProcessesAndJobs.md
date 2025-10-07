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
In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at /tmp/flag_fifo into which (like in the Practicing Piping FIFO challenge) /challenge/run wants to write your flag. You need to kill this process.  

* Check what processes are running.
* Find /challenge/decoy in the list and figure out its process ID.
* kill it.
* Run /challenge/run to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).

## My solve
**Flag:** `pwn.college{ESdU6iC1Ph0T5b3Ebb9UeXDlC4o.0FNzMDOxwiM4kjNzEzW}`

1.First , I used 'ps -ef' to find what processes are running .  
2.I found out the process which included '/challenge/decoy' i.e PID 142 and killed it.
```
hacker@processes~killing-misbehaving-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:35 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 13:35 ?        00:00:00 /run/dojo/bin/sleep 6h
root         137       1  0 13:35 ?        00:00:00 /bin/bash /challenge/.init
root         138       1  0 13:35 ?        00:00:00 /bin/bash /challenge/.init
root         139       1  0 13:35 ?        00:00:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
root         140     138  0 13:35 ?        00:00:00 sleep 6h
root         141     137  0 13:35 ?        00:00:00 sleep 6h
hacker       142     139  0 13:35 ?        00:00:00 /usr/bin/python /challenge/decoy
hacker       153       1  0 13:35 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       157     153  0 13:35 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       167     157  0 13:36 pts/0    00:00:00 ps -ef
hacker@processes~killing-misbehaving-processes:~$ kill 142
hacker@processes~killing-misbehaving-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:35 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 13:35 ?        00:00:00 /run/dojo/bin/sleep 6h
root         137       1  0 13:35 ?        00:00:00 /bin/bash /challenge/.init
root         138       1  0 13:35 ?        00:00:00 /bin/bash /challenge/.init
root         140     138  0 13:35 ?        00:00:00 sleep 6h
root         141     137  0 13:35 ?        00:00:00 sleep 6h
hacker       153       1  0 13:35 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       157     153  0 13:35 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       168     157  0 13:37 pts/0    00:00:00 ps -ef
```
3.Upon checking the process list again , I found out that that process has been killed .   
4.Next , I ran '/challenge/run' and piped it into 'cat /tmp/flag_fifo' in order to print the flag , however there were a large amount of decoy flags present along with the real one.  
```
hacker@processes~killing-misbehaving-processes:~$ /challenge/run | cat /tmp/flag_fifo
pwn.college{oJhcouMVhKCihC210ubOR8Bdodc568JtPXWpH87uiR2V61Z}
pwn.college{rbxWRqjSkCo2Zz5sTekL1Pr1DUbWVRtF2.waFJDz9UlPgT4}
pwn.college{r8CI7.YO5Q.zol4GzTUruJnISfnXCJplMAcX2azRyjAPLo6}
pwn.college{T9I23fSPXimN6arOiSLy6W05GLGbBuHHhWnPWTJ.Zl6Ps1t}
pwn.college{FY7wT2MGw5rQY1qlW5CIjUWul6MEUpz9mkqAzQyidhhECV7}
pwn.college{4.xSdTUEHgsjfs5mGL8LY4YG2Hr-Ri9VQnxXlpEjzepQRf8}
pwn.college{bXrCmHO5G-BBpBZBKwgX1e70qFE2LhARXCQ1wC6O7y6p.2j}
pwn.college{tI.7gW6Dl3hpKr55-RMQbSQZewo7zLk.Dllz6A1EzhJTQlj}
pwn.college{8htx98WLDcQrB2STwY4Hxq3zzYIjQzgogzejA4cYKqdunXO}
pwn.college{vlJtW9ZzrcUdLRrEE87wOt7CnJV8b35hVhqEVEcWThAO1Uu}
pwn.college{OC-qxjnTBqTCekxzVkKwNVLesGxhh4De3xQBH83K41ZcDU7}
pwn.college{uq0sOKqpf1F6FtAiMGKbkaIlf8Yd1Dvm4iWw01XK0BI48LV}
pwn.college{E1ir1Ff7v-qA5JaprzmN5bbTyQQ3a5gJ1Y-.SQmEPX65M4h}
pwn.college{6Kl1cxnzQctexcHUN.UoTIxCUJs9hUXknWu4CT24.YqMYOX}
pwn.college{1y792YetUwIYsyXbaNqIvOtkNQbm0pWmzCCKODtM1fd-oSG}
pwn.college{2zJpA9cYtoTB3kAGWWxOUYKF6iP4YHtdMRPdB.Nkzl4rFE8}
pwn.college{PvHhJGA5JW.qIjxsTtRIHobKj155i750IQTjwsSXo95blDW}
pwn.college{wijHH.LPZKde6XsHvuisZNsz43Yn1Sa2n5GZyjTVx4aZKwq}
pwn.college{8kE3l6hPaDjNwZZeV5iUf.PjugR5YoC0yl5LNYovUOaTqBw}
pwn.college{aTxviPDrsxfySfXAx8E4j49lD2AFPREeNTpGcgA2wE65uu5}
pwn.college{60.qQbgNK5xJj.yp0RYQe0ySPMfHawTkVuFbm7DCxbF9q4I}
pwn.college{fsShhSHsKMJUjGXRegoIA2tnuc4Rc46ausVF28KrHuS-36q}
pwn.college{ynEPGGmH4hOptRe9IQwXy.AK1rIom.ZwskUKZM-23q7TEve}
pwn.college{94hUuYIyuEl9FHgvU4dg0y-V1TP1Gfgynhu8Y5MCnuwWXWm}
pwn.college{wD3hUOW9Onju9yZEdcHQfxUMSMSuMoPaB5giQ.rdE2Lbwwy}
pwn.college{NHN6-CareZjqQ2T-JPCb68AOx1SYa-z3rwO4uRMWqwcIv4Y}
pwn.college{P7.J9y9W1XZDnQSLFNmbEaSI2wSYzwkHaRBKF-xzEsRUJqg}
pwn.college{BwdjS2APU.BKNH2fFJMaw8wi83aZcW5gotkCy.dPwuVUB68}
pwn.college{-JQX28-PAnIBeTx6IXKg0Gr.i9rZdlQEEoJnzphbDJdmqy6}
pwn.college{3a.8usqGb.Tpd3Kf6S74ZrNg6iLIMLEVfoWP9TTDf9gWEYV}
pwn.college{Hcymx9mk-Kd3M0MpkkPWBW16771.1T2vv08KWaiDhpGCroK}
pwn.college{L-NR7EXTocT6gARS8SQqwH4hq3yn-ls0pNBrFioCT04MkFv}
pwn.college{tsv2IPL4C7VNKcIOdIzDp0w742Bxuouq0V-ReP46DR802iE}
pwn.college{8tOstV6O32o78Y4jVoqddH7nW0WbSMLmCD6yxznRjF4pyKk}
pwn.college{NZAos7jwXtf1WuT1IIlgYCzR-DpFn56rF-Z4dHl6pTBlV5v}
pwn.college{erLd4HeMaCdsoiRmjuTh3FhZcJoOUPDhBerMQH5IkzTsmwD}
pwn.college{81Zg2I29P.j2Yy8p9APinxi3RuNn0N2AyQKJSSgDVW-Fjvy}
pwn.college{.zRJRVom.Gw7Nq67Y0NrKzV47RNS5Ws2QuFYaOYIEUIKztE}
pwn.college{0OHD0AX980sdVqhAag0aSyeuOWCW0GmjkH08gF7RkhZKK0I}
pwn.college{gTOKfe3VsivaI2L1zPNjF5EtHpG4RlI2zbXy3.vKdHJoNvt}
pwn.college{U6am2WFzCOQkH7wBSjE981dYWZPKPsZnQt61t-IRRvF7YjP}
pwn.college{wIJdrI2PhUPrkLJMqu0x90UBueDbbjvjnZ..aOdh1azJJu9}
pwn.college{tWsZ1yBfA5aeu2st72l0DLiHJfvD9SVFFub.sIQLRQurv7c}
pwn.college{w2lwT.EK2Ur3f.QQGGITiyfDZXdZU9kiAlhmceFF9bYvIv1}
pwn.college{T9xAJwwyogqUtvPXhTaMq5lp.5x20n1ZMBufVfhSeMPUyYx}
pwn.college{1o9Fdsco4PKKQEE37ZadQ4CbHOPTAts9YzNerTGgsY9r9A6}
pwn.college{DwfzTGkvsh1DVBkwiux-vlCv.RxGgmhqGkJhyDA5oUrb9Nv}
pwn.college{262D2Lqxa6s.x2Iq8iAuHXdRNzpZvn9IqG2sFOnn1kL70uG}
pwn.college{oPRVMvjC93ve9tqrpeJIFBYFtTZuEThKinXS.fjukeXQ382}
pwn.college{AB4ePmVGuALqin9WydwF3KlwgM9-V3T3SADq9ImQ4.Bver6}
pwn.college{itLNFhbngkn4m7OYp4oSzPVuLIlQFqBA2wJaykMltE.N5Gd}
pwn.college{UUd2BtmvheV5.euoTJOFcEgLv5l6L1ytvVhdTerg4FChVv0}
pwn.college{mq9H0qQC9XgupbvJ9Qo0cIPvwQ-WactdaZG41SP-lzUH1ol}
pwn.college{gTcGiG1F8zxdTteqBYMxCpVnbAlvcq0..HVon.BMgNTYYPB}
pwn.college{ZmybqXiN8HIQolqnLljSJ2QYxG2CRqXBHNrJIrBtWbewple}
pwn.college{WgqwiELs8y6q-hWwNxKUjz9HvsYK.d8cANASzROTYxYrsp9}
pwn.college{7LRHgRFOeTloi97p1pKlp-zpAtcDppE-v1XoKvgnPbXHBQh}
pwn.college{k7UO9IxTNqo1UPW57b6UA0N774jcHR5EMJpxWiehADPGC8C}
pwn.college{xNoqKd9Z3DhAwdQB.ygvnrbz.yHzyzrRdJRiOvSPa8n2pu7}
pwn.college{ZdskKDksNNYFW4008Z60vlL5jHaQD1VJ94czPlfib4R34R.}
pwn.college{IEgwnJvLhEYJP3EuORjnouP47jy7m649GxBc5ev9lxR0LeU}
pwn.college{6sWdUE4xKa-yQ5DAsXy2A716OSLhJ4HcZTieLRyBpifq02k}
pwn.college{DeYHdjQsgyXAk7Vygowi0SDuQEvfTAeCtDcL04Gr7MK8FCP}
pwn.college{cwZ7ZPur2UR664gd63klYLQPlQE5kR9XJcx9M77aGo7i3vw}
pwn.college{aA0-K0ejmpbqH3sq9OyZgkUFq-1yJQXqwhOBrHPCrbYXz1D}
pwn.college{CDzlrS0Sq7gQMVV6KuJRH4VudVQGMWf8izAxdfqh4qQdihL}
pwn.college{JpuwnGL5ClFdz-htMQuvkhEB0r2nhYKcuNu4xjBm-htT-jy}
pwn.college{HaJcwZIJdkf7CgC2b3Vc8tKOfis2q18fBu-xkBZqz.fDhEZ}
pwn.college{KqFhV8KwNbgTItX.4dbMIIgLNDnMO30BXkhAcR1M9rNcxy-}
pwn.college{4AhE9ORWrl.pGJSvHGeeprtDXUuv3RQLUUO73iw0Sm8wvli}
pwn.college{rXgv3zOvVIEJM5nzgHDYdEEYr16b68tQ0VIKmphh6ZSGSLb}
pwn.college{gsjw4s3F8Qb.hg0ggUHJ8HRkpuJUqr2TITy7ePP698tCFyc}
pwn.college{ra9YHdDsuPZ6UCcxZoabJBHVCNxrgIuCBlZqEK-CSlN9gEQ}
pwn.college{jp6KOB95fNkt8W2i7ekluF.9F40vwZaQtVnAQ71GLK58hUb}
pwn.college{DpvMP6D4.gtdIaHC2L-SBVDFPAtsZ-cV8z3TyjMlSOxFelT}
pwn.college{cHrnP8r1IymlQ93zR6rX-gpkhxT5kvF1TBmMFcT.XqFiUdi}
pwn.college{-cEXeeJwDvfRfmPuwx59d8nklv4Ivbcc.lbWj9FZtcvuE9s}
pwn.college{Z3Oi7Fe2WVCvfICJyx0XvQcwrPNgUbuO2PIUoJQEtGG9oNw}
pwn.college{LZo4EE9CuHWjGxbV2RLyiB8h8rwWz8y0.km2JctJsLyvgvU}
pwn.college{D-RCLwQbW5ysgHMPeNnp2ykrPWO9UVzbBMo5DAf-ha-9BsH}
pwn.college{7BniSpHGuEWIL.u5kU-AFSTNvwCFwT6L5vexDs.NSkm25c4}
pwn.college{dBsKiHkvP5dWumxIytCAcXb1U0GEaMkNf8qGF13SV0fZQSA}
pwn.college{ZIy0.ZAog6Otqdz7ILrwc7NVFNAP8gbSH0crlfKOM3WhS94}
pwn.college{gAiulELJ3lqMb8d7VjZ79NValQczEaNg1Wv6pPiz3Btl78p}
pwn.college{JKOfKxLV3uvxn61mQJwJorFwqBuea5FBKNyx4G-PI5vga4L}
pwn.college{a7B9r3I2jsGT3VKR4sLV4phVTGYUJ6wDNTm21E3rPJ-LPvL}
pwn.college{RCSi8S3on.PmOOGn6yyE-sOIMvTsju8oPkukBMoYic5YDhA}
pwn.college{EDB8JozkUFKmgXbZMg7dgxz0bfJLar0imuLx82Hpjqn1dT2}
pwn.college{Zwpx3MU.O23ukbPuGN-BUkp6YAKWwAJ3QTJ9DyzOY96-E1d}
pwn.college{h0bDYXaP9uhpCY9OvurbJ-C.OCTEEqepbk9c8jESYsFK0ql}
pwn.college{M1zPJfihbHx5R3qU3GQvy4m8nwEcc5G8jTVL-bxKbQgKXMR}
pwn.college{.ETF5OmnU9usQCNJBHQxf1Sp.nJ2yN4E6NmTU8lV8V4-.Q7}
pwn.college{ABW-E-DB46zGDJsMXP8jimeXbm54Bw4BlE8ab3H9QL.n-1-}
pwn.college{QwZxZlVE4y.qwvMxw5-d-WI3bveRvj8yEH8kkFtPUyY2nf6}
pwn.college{MBlla0WolEDhrG5YhzMCsrXajQbX2wjjjWrYbgTanpRPPq8}
pwn.college{dBnXfyIu-.TyFhY9KXFaDutm7Wn0BUEWMffZI14mxd6fUSJ}
pwn.college{I4C5mf2nwZprKbsE3bc3B1dJW7p587kAaEBFTC4KeffiW0U}
pwn.college{I0xo-45apAa3WMHI-ROa0nDF9Y-qCMKXO6k4OeBCRrAtzl9}
pwn.college{eaa8Mq3Yf2CNkIh8zMGROVBo7Qs4iXNFh9vhbzSiA2RSqFe}
pwn.college{vaVWMrYO.3fLXVVnf0alHny9FlHOwZ5z-0E.OleaYzdFnLC}
pwn.college{ZftZ327RXUgczaR-GbudziOxcEXKehCp1Rfy68DMjgmJG6T}
pwn.college{CbCx5h2dYDCfAhpNLzLbUWq4rewYZ4ZK93edFGbjU1Wr7Bi}
pwn.college{rbsU87fzHMPmjQDADpEdqaMA..EZfFyqHjJ6pxS7QYcbcQ4}
pwn.college{d.tDJhlrISuEl7B-fsYSAgBF8IWNpRNmEcSPqWfVMKh9G2j}
pwn.college{2AiigGQOk-9XJaHopXncMlVv40Ux2Y2eRf.7yQPTeNoEoNs}
pwn.college{qlgc.22P3a9XiyiTtWmHKWtdN98pdhRP35qy1tsrD9Vt.BZ}
pwn.college{YhMz22IH.NJvdfljtk-w-b6hi3wsB7fLEShjMf9oUdAEK17}
pwn.college{PbRJVtxbGItMcdA8yjmw6YFdyVtTM9QBVH99xWLA8F6.E1V}
pwn.college{itZ89iO5nWWo.Bc3AUfCYVZkgYzbt-2fIg16c0dsJuRgOXB}
pwn.college{QL9zdsynG4.A8gdf96VHTbruurRhxAzgqFFpfVJjmgC1iRo}
pwn.college{xyVEko1N9yIsd0HyxKdDRI.WY.41Wm9WgVx3Y65n0zHsRsx}
pwn.college{7BRXtoAK5D-tdDzksP9almcAcIuRsLb6UIlItTP9X6mAgUW}
pwn.college{IE6MIopDtWU.mIraLrPFFXI2aXn3PuFzN2enpLBrqg561Vl}
pwn.college{A.roMmqddySIN0u6vd2GZMxBOSk96wCLNAYIhBNmwtUjvP8}
pwn.college{qm05mND12mip2Q2aKFQBm9lQMmYetLFp5ZVZYSG48tHv9vA}
pwn.college{7tZJaj5Uch05zBkx1d2ZK2rLm3iFbTH2d3YYf1lyK3PG6qw}
pwn.college{BTQnXvKkbuBkE9ES0EeG6M1Qw4w5licBx.eaeXn-GMYjBiP}
pwn.college{cQhayA0AQDhpW--vB-.xutGusW7bQ51kPNxt6rLnI4Xzxzg}
pwn.college{K0j3XQEF45GgubCwYxzrCYtUO58nhgusD3iP6Ux9FWh3Hg6}
pwn.college{2xugb4fWA86G6McN3y7m.L0gqcf..HzxzL-NPpBt8Ts-3oE}
pwn.college{G0h4wxLm9-Sqx6UXNQR-1LW.lh3586UsClUQXE9fPzz.RkT}
pwn.college{m3yxYhNJMarUwYxwKNFIsM-EJbxnhZYkZFTE2CVSdq6J7y7}
pwn.college{N4FADryHIg5q8QWGvuHCEGNZbtSzvgEJWkBpsjYI-aJKvvS}
pwn.college{ZI2X6C7DtDtnhRnzo8Xm6TlP9Ssnnwqzi9But05ODhPEqUD}
pwn.college{t2B1rkfYuvdmFPj5k69zaWfK46mfbiYO5pP.0F3DsQonIXS}
pwn.college{qRfowd7dkH81pyydelp78Rmq7OndVUhnAmT.85cuVPwzSFW}
pwn.college{tHYtzRhuR.K0I145QqT0l6jGybhzKgo15R5dsH9y8toPbwX}
pwn.college{HZY6x9PgNVqn6YsnFQ6aFl387u2z7uEj8p7P-74gKgm4Np7}
pwn.college{gpI21h6z3mdL8mhP.Dp-.P1un.eIxdSMzl.Ujq4E6e0D7fG}
pwn.college{tJ.34Fm6nGNaVVbhqr41QeAnd49ymvqh8DUsA.3xQ5MlVgx}
pwn.college{pmJ-l0koDh4YXxv9KLfb7LU1uSTSXsiRYShOEXr0pZs6Lca}
pwn.college{Fa6-9mab.0SwxWXgKJeJEhl.-1yVLvSg-DnUI-.yGf59Z7m}
pwn.college{zkGIaLzqEBT5RCBZYyZ8YQ6qiAeLZ-JC39q3RkafNGe0BVV}
pwn.college{ArQFQVpKLx7OehhKUdTGgbz1yk21rxsB1nCLx4yr4dnOSgn}
pwn.college{ESdU6iC1Ph0T5b3Ebb9UeXDlC4o.0FNzMDOxwiM4kjNzEzW}<-real flag
```
5.The last flag was the real one.

## What I learned
Through this challenge , I learnt how to kill processes that are misbehaving or interefering with actual work.

## References 
Did not use any references for this challenge.


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

# BACKGROUNDING PROCESSES
This level's run wants to see another copy of itself running, not suspended, and using the same terminal. How? Use the terminal to launch it, then suspend it, then background it with bg and launch another copy while the first is running in the background.

## My solve
**Flag:** `pwn.college{UPMxa-ZXKEJfhYj6DwXALuub0Jm.QX3QDO0wiM4kjNzEzW}`

1.I suspended '/challenge/run' using 'ctrl+Z'.  
2.I then use 'bg' to resume it in the background.  
3.I ran /challenge/run and obtained the flag.

```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         158 S+   bash /challenge/run
root         160 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:48 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 13:48 ?        00:00:00 /run/dojo/bin/sleep 6h
hacker       132       1  0 13:48 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       136     132  0 13:48 pts/0    00:00:00 /run/dojo/bin/bash --login
root         158     136  0 13:53 pts/0    00:00:00 bash /challenge/run
hacker       165     136  0 13:53 pts/0    00:00:00 ps -ef
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 
Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.
hacker@processes~backgrounding-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:48 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 13:48 ?        00:00:00 /run/dojo/bin/sleep 6h
hacker       132       1  0 13:48 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.
hacker       136     132  0 13:48 pts/0    00:00:00 /run/dojo/bin/bash --login
root         158     136  0 13:53 pts/0    00:00:00 bash /challenge/run
root         169     158  0 13:53 pts/0    00:00:00 sleep 6h
hacker       170     136  0 13:53 pts/0    00:00:00 ps -ef
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         158 S    bash /challenge/run
root         169 S    sleep 6h
root         171 S+   bash /challenge/run
root         173 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{UPMxa-ZXKEJfhYj6DwXALuub0Jm.QX3QDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about resuming processes in the background using 'bg' i.e. This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

## References 
Did not use any references for this challenge.  


# FOREGROUNDING PROCESSES
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it

## My solve
**Flag:** `pwn.college{wdc5Hv4feNskQsgvhvFwmWwMc4-.QX4QDO0wiM4kjNzEzW}`

1.I ran '/challenge/run' in order to obtain the instructions for the challenge.  
2.I suspended it using 'Ctrl-Z'.  
3.I backgrounded the process using 'bg' and used 'fg' to foreground it without suspending it .  
4.Thus, I was able to obtain the flag.

```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.

hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{wdc5Hv4feNskQsgvhvFwmWwMc4-.QX4QDO0wiM4kjNzEzW}
```

## What I learned
In the challenge , I learnt how to foreground processes by using 'fg' .

## References 
Did not use any references for this challenge.   

# STARTING BACKGROUNDED PROCESSES
Here , sleep is actively running in the background, not suspended. Now it's your turn to practice! Launch /challenge/run backgrounded for the flag.

## My solve
**Flag:** `pwn.college{MET8OxeRZL49KurAs3CPSza8E6Z.QX5QDO0wiM4kjNzEzW}`

Through my understanding of using '&' to append a command and causing it get it backgrounded while starting . , I ran '/challenge/run &' to obtain the flag. 

```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 146
hacker@processes~starting-backgrounded-processes:~$ 


Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{MET8OxeRZL49KurAs3CPSza8E6Z.QX5QDO0wiM4kjNzEzW}
```

## What I learned
I learnt how to use '&' appended to a command in order to get it backgrounded at the start of the process.

## References 
Did not use any references for this challenge.

# PROCESS EXIT CODES
In this challenge, you must retrieve the exit code returned by /challenge/get-code and then run /challenge/submit-code with that error code as an argument.

## My solve
**Flag:** `pwn.college{ARwPQX_LI17LBHhwLIMG-1E57ha.QX5YDO1wiM4kjNzEzW}`

1.I used echo followed by '/challenge/get-code $?'in order to obtain the exit code for the command '/challenge/get-code'.  
2.Next, I ran /challenge/submit-code with argument '151' which was the exit code obtained previously to get the flag.  

```
hacker@processes~process-exit-codes:~$ echo /challenge/get-code $?
/challenge/get-code 151
hacker@processes~process-exit-codes:~$ /challenge/submit-code 151
CORRECT! Here is your flag:
pwn.college{ARwPQX_LI17LBHhwLIMG-1E57ha.QX5YDO1wiM4kjNzEzW}
```

## What I learned
* Through this challenge , I learnt that every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates. This can be used by the shell, or the user of the shell  to check if the process succeeded in its functionality . You can access the exit code of the most recently-terminated command using the special ? variable prepended  with $ to read its value.
* Commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.

## References 
Did not use any references for this challenge.






