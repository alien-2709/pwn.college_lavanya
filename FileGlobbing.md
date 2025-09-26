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
**Flag:** `pwn.college{helloworld}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
example triple ticks for bash
pwn.college{helloworld}
```

## What I learned
Through this challenge

## References 
Did not use any references for this challenge.



