# MATCHING WITH *
Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag.

## My solve
**Flag:** `pwn.college{8aOezG8Pn0JMYv2IEqC5kHFV0qU.QXxIDO0wiM4kjNzEzW}`

Through my understanding of globbing with * .I used cd to change the directory from '~' to  '/challenge' but instead of using it directly , I used file globbing in a way that it only contains at most 4 characters and so that it navigates to '/challenge' without explicitly stating it. For this to happen I used '/ch*' and obtained the flag.

```
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{8aOezG8Pn0JMYv2IEqC5kHFV0qU.QXxIDO0wiM4kjNzEzW}

```

## What I learned
Through this challenge , I got introduced to the topic of file globbing with '*'. When the shell encounters a '*' character in any argument, it will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. For eg. if you wanted to echo  files - star1 , star2 and star3. We can use globbing and just *echo LOOK:star** which will output all files following this pattern . I also learnt that when zero files are matched, by default, the shell leaves the glob unchanged. for eg.In the earlier example if we *echo Look:hello** then the output would be *hello**.

## References 
Did not use any references for this challenge.

# MATCHING WITH ?
Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag.

## My solve
**Flag:** `pwn.college{YQL6LOu8mKQM8CLWzO1f-bJ0vPF.QXyIDO0wiM4kjNzEzW}`

Firstly , using my understanding of '?' glob ,I replaced c and l in challenge with a '?' and used it as an argument with cd in order to navigate to the '/challenge' directory . Next, I ran '/challenge/run' inorder to obtain the flag.

```
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{YQL6LOu8mKQM8CLWzO1f-bJ0vPF.QXyIDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that unlike '*' in the previous challenge where it could replace multiple characters , '?' is used as a single-character wildcard .For eg. if you have files - star_a , star_b and star_cc and if you *echo Look:star_?* then the output would be *star_a star_b* only , not star_cc.

## References 
Did not use any references for this challenge.

# MATCHING WITH []
There have been placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h.

## My solve
**Flag:** `pwn.college{0oQGiufkbCZKqMTkLlRw8Rq3qAA.QXzIDO0wiM4kjNzEzW}`

Firstly , I navigated to the directory '/challenge/files ' as stated in the challenge . Next I ran /challenge/run with file_[bash] as an argument in order to cover all the files present in the directory and thus , obtain the flag.

```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{0oQGiufkbCZKqMTkLlRw8Rq3qAA.QXzIDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that '[]' is a limited form of '?' where instead of replacing single characters , it replaces a set of potential characters . For eg. if you have files - file_a , file_b , file_c and you *echo Look:file_[ac]* then the output would be *file_a file_c* .

## References 
Did not use any references for this challenge.

# MATCHING PATHS WITH []
type what the challenge asks

## My solve
**Flag:** `pwn.college{ompiuS8Uz-8tNckn9_YBPEPsv9e.QX0IDO0wiM4kjNzEzW}`

Using the instructions given in the challenge , I ran '/challenge/run' with a single argument such that the path of files is expanded i.e. '/challenge/files/file_[bash] .Thus , I was able to obtain the flag.

```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{ompiuS8Uz-8tNckn9_YBPEPsv9e.QX0IDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge, I learnt that globbing happens on a pathing basis and using globbed arguments , we can expand entire paths as well . For eg. if we have files -file_a, file_b, file_c and we *echo Look:/home/hacker/file_[ab]*, then the output will be */home/hacker/file_a /home/hacker/file_b*.

## References 
Did not use any references for this challenge.

# MULTIPLE GLOBS
Thera are some diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

## My solve
**Flag:** `pwn.college{QIHzhR_qkFaggAgnJWN2ncHKsIS.0lM3kjNxwiM4kjNzEzW}`

Firstly , I navigated to the directory '/challenge/files' using 'cd' . Next , I ran '/challenge/run' with an argument **p** which contains at most 3 characters and also covers every word that contains the letter p.Thus , I was able to get the flag.

```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{QIHzhR_qkFaggAgnJWN2ncHKsIS.0lM3kjNxwiM4kjNzEzW}
```

## What I learned
Through this challenge, I learnt how multiple globs can be used and that Bash supports the expansion of multiple globs in a single word.

## References 
Did not use any references for this challenge.

# MIXING GLOBS
There are  diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning".

## My solve
**Flag:** `pwn.college{wVcUEeJq-QOI75T_7etjVS0BGIa.QX1IDO0wiM4kjNzEzW}`

Firstly , I navigated to the '/challenge/files' directory . Next , I ran '/challenge/run ' with the argument [pce]*, which was the suitable argument to match the files "challenging","educational" and "pwning".After several tries I was able to get it right .

```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [pce]*
You got it! Here is your flag!
pwn.college{wVcUEeJq-QOI75T_7etjVS0BGIa.QX1IDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to use multiple globs in the same argument in order to match with the given files .

## References 
Did not use any references for this challenge.


# EXCLUSIONARY GLOBBING
Go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n.

## My solve
**Flag:** `pwn.college{QHBwU8Z56XGctg0a2sa27X20Fe2.QX2IDO0wiM4kjNzEzW}`

I first navigated to the directory '/challenge/files' using 'cd'. Next , as I ran '/challenge/run' with the argument [!pwn]* as the requirement is that the file shouldn't start with a p,w or n and can be followed by anything, thus represent by [!pwn] and '*'.Thus , I was able to get the flag.

```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{QHBwU8Z56XGctg0a2sa27X20Fe2.QX2IDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt how to use '!'/'^' before characters in a '[]' glob in order to say that these characters should not exist in the filename.

## References 
Did not use any references for this challenge.


# TAB COMPLETION
This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename. In order to get the flag , make sure that you must tab-complete it.

## My solve
**Flag:** `pwn.college{Y25iSJTqpfEOrVm4uI54cO-1NTH.0FN0EzNxwiM4kjNzEzW}`

Firstly , as shown in the example , I listed the directories present in '/challenge' . Next I catted  out /challenge/pwn<TAB> where clicking <TAB> autocompleted the filename and thus the flag was obtained.

```
hacker@globbing~tab-completion:~$ ls /challenge
DESCRIPTION.md  pwncollege​
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{Y25iSJTqpfEOrVm4uI54cO-1NTH.0FN0EzNxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that using '*' can lead to mistakes and expansion of unintended files and if this continues eventually it will be too late until the 'rm' command is used. Thus , a safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it.

## References 
Did not use any references for this challenge.


# MULTIPLE OPTIONS FOR TAB COMPLETION
This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

## My solve
**Flag:** `pwn.college{Y6wK3jS_i65gngeXEBWd81q8_01.0lN0EzNxwiM4kjNzEzW}`

Firstly , I 'cd'd' into the directory '/challenge/files' and then as per the instructions /challenge/files/p<TAB> in order to use tab completion . Next , I kept on using tab completion until i reached 'pwncollege-flamingo' where i noticed the option of 'pwncollege-flag' so I catted it out to obtain the flag.

```bash
hacker@globbing~multiple-options-for-tab-completion:~$ cd /challenge/files
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flamingo    pwncollege-hacking
pwn-college            pwncollege-family      pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ /challenge/files/pwncollege-f
pwncollege-family      pwncollege-flamingo    pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ /challenge/files/pwncollege-fl
pwncollege-flamingo    pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ /challenge/files/pwncollege-flamingo
hack-the-planet        pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat pwncollege-flag
pwn.college{Y6wK3jS_i65gngeXEBWd81q8_01.0lN0EzNxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that when there are multiple files with similar names, thus there are multiple options for tab autocompletion . In this case by default bash will auto-expand until the first point when there are multiple options . When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

## References 
Did not use any references for this challenge.


# TAB COMPLETION ON COMMAND
This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it.

## My solve
**Flag:** `pwn.college{I6ZGGsmqvVOaW4KTZU0AixPbK0K.0VN0EzNxwiM4kjNzEzW}`

Firstly . according to the instructions given , I typed in pwncollege and the hit <TAB> for autocompletion. Hitting <TAB> once more after the first autocompletion gave me the flag.

```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-24096 
Correct! Here is your flag:
pwn.college{I6ZGGsmqvVOaW4KTZU0AixPbK0K.0VN0EzNxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that tab completion is for more than files, You can also tab-complete commands.Any command can be auto completed but callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands.

## References 
Did not use any reference for this challenge.





