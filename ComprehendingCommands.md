# CAT:NOT THE PET ,BUT THE COMMAND
The challenge is to read the copied file 'flag" in the home directory by using cat.

## My solve
**Flag:** `pwn.college{0566YnK-NAFU_MT6FzDsk_xn56U.QXxcTN0wiM4kjNzEzW}`

I used my understanding of cat and read the file flag stored in the home directory by using cat flag.

```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{0566YnK-NAFU_MT6FzDsk_xn56U.QXxcTN0wiM4kjNzEzW}
```

## What I learned
A new command I learnt from this challenge is cat and how it is used for reading out files . I learnt how cat will concatenate multiple files if multiple arguments are provided and if there are no arguments , it will read from the terminal input and output it.

## References 
Did not use any references for this challenge.

# CATTING ABSOLUTE PATHS
The challenge is to read a file 'flag' using cat at its absolute path.

## My solve
**Flag:** `pwn.college{IDPkDw3m-Cw4_QEHGY8jK9ut8cx.QX5ETO0wiM4kjNzEzW}`

Using my understanding from the given example , I used cat to read the flag file stored in the '/' directory by using its absolute path (/flag) as an argument.

```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{IDPkDw3m-Cw4_QEHGY8jK9ut8cx.QX5ETO0wiM4kjNzEzW}
```

## What I learned
In this challenge , I learnt how to read a file using cat by using the file's absolute path.

## References 
Did not use any references for this challenge.

# MORE CATTING PRACTICE
This challenge involves using cat to find the flag which is placed in a directory that you cannot use cd to navigate to i.e. we must use the file's absolute path.

## My solve
**Flag:** `pwn.college{0z-qGpq8inopfW4WLDBhw7-1WGe.QXwITO0wiM4kjNzEzW}`

To solve this challenge , I used my understanding of cat and made the absolute path of the file 'flag' as the argument for cat thus being able to retrieve it without using cd to navigate to that directory.

```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /lib/systemd/system-sleep/flag. Go cat it out **without** cding 
into that directory!
hacker@commands~more-catting-practice:~$ cat /lib/systemd/system-sleep/flag
pwn.college{0z-qGpq8inopfW4WLDBhw7-1WGe.QXwITO0wiM4kjNzEzW}
```

## What I learned
I learnt how to read a file using cat without using cd to navigate to that directory.

## References 
Did not use any references for this challenge.

# GREPPING FOR A NEEDLE IN THE HAYSTACK.
Using grep , search for  the flag (which begins with pwn.college) in the file /challenge/data.txt where thousands of lines of text are present.

## My solve
**Flag:** `pwn.college{4xKVwWO89Ej5PtgtSF7e8Aa0Sz1.QX3EDO0wiM4kjNzEzW}`

For this challenge , I first understood how to use grep to read big files that cannot be read out by cat . I used *grep SEARCH_STRING path/to/file* , in order to search for pwn.college in the big file /challenge/data.txt.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{4xKVwWO89Ej5PtgtSF7e8Aa0Sz1.QX3EDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new command called grep which is used to read out required sections of files that are so big that cat cannot be used. One of the ways to use grep is *grep SEARCH_STRING path/to/file* where grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

## References 
Did not use any references for this challenge.

# COMPARING FILES
There are two files in /challenge:

1./challenge/decoys_only.txt contains 100 fake flags.  

2./challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag.  

Use diff to find what's different between these files and get your flag.

## My solve
**Flag:** ` pwn.college{kb350L8jbCYKPJwp1P7pyQd94Yo.01MwMDOxwiM4kjNzEzW}`

Through my understanding of diff as shown in the example , I used diff followed by the two files as arguments such that the difference between them will be given as output in the terminal. This output would be the flag as it is the only element thats different between the two files full of fake flags .Thus , I was able to obtain the flag.

```
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
66a67
> pwn.college{kb350L8jbCYKPJwp1P7pyQd94Yo.01MwMDOxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about the usage of diff to compare two files line by line and how the difference between the files will be given as output in the form of numbers and letters which indicate which line is changed / replaced .

## References 
Did not use any references for this challenge.

# LISTING FILES
 /challenge/run  has been renamed with some random name. List the files in /challenge to find it.

## My solve
**Flag:** `pwn.college{gnNVC04-Wjj-WNO-ITGT4aLxtIf.QX4IDO0wiM4kjNzEzW}`

Firstly , I navigated to the '/challenge' directory and listed out the files present using 'ls'. Next, I found that '/challenge/run' has been renamed as '/challenge/593-renamed-run-21094'. This I ran /challenge/598-renamed-run-21094 to obtain the flag.

```
hacker@commands~listing-files:~$ cd /challenge
hacker@commands~listing-files:/challenge$ ls
593-renamed-run-21094  DESCRIPTION.md
hacker@commands~listing-files:/challenge$ /challenge/593-renamed-run-21094
Yahaha, you found me! Here is your flag:
pwn.college{gnNVC04-Wjj-WNO-ITGT4aLxtIf.QX4IDO0wiM4kjNzEzW}
```

## What I learned
I learnt about a new command called 'ls' used to list files present in directories and through this challenge , I was able to understand its use efficiently.

## References 
Did not use any references for this challenge.


# TOUCHING FILES
 To create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag.

## My solve
**Flag:** `pwn.college{Mj_doy3xeTcNUjxtasnZUNUX5hX.QXwMDO0wiM4kjNzEzW}`

I first navigated to the /tmp directory from ~ directory. Next, I understood the usage of command touch to create new files and thus used it to create the files given in the challenge. Then I ran /challenge/run in order to get the flag.

```
hacker@commands~touching-files:~$ pwd
/home/hacker
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{Mj_doy3xeTcNUjxtasnZUNUX5hX.QXwMDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new command called touch that is used to create new files in Linux.

## References 
Did not use any references for this challenge.


# REMOVING FILES
To remove the delete_me file created in the home directory by using rm command and then run /challenge/check which will check if you deleted the file and then give you the flag.

## My solve
**Flag:** `pwn.college{oAVOEM_HAfS3kiD4gSa0-YVlDU9.QX2kDM1wiM4kjNzEzW}`

I first understood  the usage of the rm command to remove a file in Linux by referring to the examples given . Next, I applied this in the terminal to delete the delete_me file created in the home directory , followed by running /challenge/check to obtain the flag.

```
hacker@commands~removing-files:~$ ls
Desktop  d  delete_me  x
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{oAVOEM_HAfS3kiD4gSa0-YVlDU9.QX2kDM1wiM4kjNzEzW}
```

## What I learned
I learnt the usage of the rm command in order to remove/delete files from a directory in Linux.

## References 
Did not use any references for this challenge .

# MOVING FILES
This challenge wants you to move the /flag file into /tmp/hack-the-planet and when you're done, run /challenge/check,to obtain the flag.

## My solve
**Flag:** `pwn.college{YwNUQbXpsY2MprdUWhN6Sk_MtFG.0VOxEzNxwiM4kjNzEzW}`

I first understood the usage of command mv in order to move one file into another within a directory . Next , I applied this to my solve and was able to obtain the flag.

```
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{YwNUQbXpsY2MprdUWhN6Sk_MtFG.0VOxEzNxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt about a new command called 'mv' used to move files , that is one file into another within a directory.

## References 
Did not use any references for this challenge.

# HIDDEN FILES
The flag is hidden as a dot-prepended file in / . We must obtain it.

## My solve
**Flag:** `pwn.college{g61rHXIOIR5VkSNwLMQiH8omTr1.QXwUDO0wiM4kjNzEzW}`

I first navigated to the '/' directory and listed out all unhidden files using ls.  
As explained in the example , ls does not list all the files within a directory . There are some files that are hidden and must be accessed using ls -a. Thus , I used ls -a to obtain the dot-prepended file containing the flag. Next , I used cat to read out its contents and obtained the flag.

```bash
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls
bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv             bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-316161129630811  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-316161129630811
pwn.college{g61rHXIOIR5VkSNwLMQiH8omTr1.QXwUDO0wiM4kjNzEzW}
```

## What I learned
I learnt about the concept of hidden files (files that start with .) and how they can be accessed using ls -a (where -a is a format of ls ) instead of just ls because Linux by default does not list those files.

## References 
Did not use any references for this challenge.

# AN EPIC FILESYSTEM QUEST
In this challenge, I have hidden the flag. Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:  


0.Your first clue is in /. Head on over there.
   
1.Look around with ls. There'll be a file named HINT or CLUE or something along those lines!  

2.cat that file to read the clue!  

3.Depending on what the clue says, head on over to the next directory (or don't!).  

4.Follow the clues to the flag!

## My solve
**Flag:** `pwn.college{wyYmt3PpgjXaGHXX5_MG_tDY6ya.QX5IDO0wiM4kjNzEzW}`  


1.I used cd to navigate to '/'.  

2.Used 'ls' to list files in '/'.  

3.As GIST is a suspicious file , I catted it out to find the first clue in */opt/linux/linux5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2*.  

4.Next , I navigated *to /opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2* and listed the files present in it using 'ls'.  

5.As TEASER was a suspicious file , I catted it out to obtain the next clue in */usr/share/racket/pkgs/mysterx*.  


6. As the clue is hidden , I navigated to the directory */usr/share/racket/pkgs/mysterx* and listed out all the files including hidden ones using 'ls -a'.


7.As .SECRET seemed like a suspicious file , I catted it out to obtain the next clue in */usr/share/help/it*.  


8.As the clue is delayed , I entered the directory */usr/share/help/it* using 'cd' and then listed out the files.


9.As BLUEPRINT seemed suspicious , I catted it out to obtain the next clue in  */usr/lib/python3.8/multiprocessing/__pycache__*.  


10. As the clue is delayed , I entered the directory */usr/lib/python3.8/multiprocessing/__pycache__* and then listed out the files in it.
    
    
11. As MEMO seemed suspicious , I catted it out to obtain the next clue in */usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled*.
    

12. As the clue is trapped , I listed the files in it directly by using its absolute path 'ls */usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled*'.
   

13. Since TRACE-TRAPPED looked suspicious , I catted it out by using its absolute path to obtain the next clue in */usr/share/racket/pkgs/draw-doc/scribblings/draw*.
    



```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
GIST  bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~an-epic-filesystem-quest:/$ cat GIST
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2$ ls
Kbuild  TEASER  base.c  gp102.c  priv.h  tu102.c
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2$ cat TEASER
Yahaha, you found me!
The next clue is in: /usr/share/racket/pkgs/mysterx

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/gpu/drm/nouveau/nvkm/engine/sec2$ cd /usr/share/racket/pkgs/mysterx
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/mysterx$ ls -a
.  ..  .SECRET  LICENSE.txt  compiled  info.rkt  main.rkt  mysterx.rkt  scribblings
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/mysterx$ cat .SECRET
Yahaha, you found me!
The next clue is in: /usr/share/help/it

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/mysterx$ cd /usr/share/help/it
hacker@commands~an-epic-filesystem-quest:/usr/share/help/it$ ls
BLUEPRINT  gedit
hacker@commands~an-epic-filesystem-quest:/usr/share/help/it$ cat BLUEPRINT
Tubular find!
The next clue is in: /usr/lib/python3.8/multiprocessing/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/help/it$ cd /usr/lib/python3.8/multiprocessing/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ ls
MEMO                       managers.cpython-38.pyc           process.cpython-38.pyc           sharedctypes.cpython-38.pyc
__init__.cpython-38.pyc    pool.cpython-38.pyc               queues.cpython-38.pyc            spawn.cpython-38.pyc
connection.cpython-38.pyc  popen_fork.cpython-38.pyc         reduction.cpython-38.pyc         synchronize.cpython-38.pyc
context.cpython-38.pyc     popen_forkserver.cpython-38.pyc   resource_sharer.cpython-38.pyc   util.cpython-38.pyc
forkserver.cpython-38.pyc  popen_spawn_posix.cpython-38.pyc  resource_tracker.cpython-38.pyc
heap.cpython-38.pyc        popen_spawn_win32.cpython-38.pyc  shared_memory.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cat MEMO
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cat /usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled
cat: /usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled: Is a directory
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ ls /usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled
TRACE-TRAPPED         beta-utils_rkt.zo        delta-dist_rkt.zo      gamma-random_rkt.zo     normal-pdf_rkt.zo      poisson-pdf_rkt.zo
beta-inv-cdf_rkt.dep  binomial-pdf_rkt.dep     gamma-inv-cdf_rkt.dep  normal-cdf_rkt.dep      normal-random_rkt.dep  poisson-random_rkt.dep
beta-inv-cdf_rkt.zo   binomial-pdf_rkt.zo      gamma-inv-cdf_rkt.zo   normal-cdf_rkt.zo       normal-random_rkt.zo   poisson-random_rkt.zo
beta-pdf_rkt.dep      binomial-random_rkt.dep  gamma-pdf_rkt.dep      normal-inv-cdf_rkt.dep  normal-utils_rkt.dep   walker-table_rkt.dep
beta-pdf_rkt.zo       binomial-random_rkt.zo   gamma-pdf_rkt.zo       normal-inv-cdf_rkt.zo   normal-utils_rkt.zo    walker-table_rkt.zo
beta-utils_rkt.dep    delta-dist_rkt.dep       gamma-random_rkt.dep   normal-pdf_rkt.dep      poisson-pdf_rkt.dep
```

14.As  the clue is trapped , I listed the files directly by using its absolute path 'ls */usr/share/racket/pkgs/draw-doc/scribblings/draw*.

15.As BRIEF-TRAPPED looked suspicious, I catted it out using its absolute path to find the next clue in */opt/linux/linux-5.4/tools/perf/arch/riscv*.

16.As the clue is delayed , I navigated to */opt/linux/linux-5.4/tools/perf/arch/riscv* and then listed the files.

17.As WHISPER looked suspicous , I catted it out to obtain the next clue in */usr/share/locale/so*.

18.As the clue is hidden , I navigated to */usr/share/locale/so* and listed out the files using 'ls -a'.

19.As .SNIPPET looked suspicious , I catted it out to finally obtain the flag.

20.The flag: pwn.college{wyYmt3PpgjXaGHXX5_MG_tDY6ya.QX5IDO0wiM4kjNzEzW}.

```
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cat TRACE-TRAPPED
cat: TRACE-TRAPPED: No such file or directory
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cat /usr/share/racket/pkgs/math-lib/math/private/distributions/impl/compiled/TRACE-TRAPPED
Great sleuthing!
The next clue is in: /usr/share/racket/pkgs/draw-doc/scribblings/draw

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ ls /usr/share/racket/pkgs/draw-doc/scribblings/draw
BRIEF-TRAPPED              common.rkt            draw.scrbl                      info.rkt                     ps-setup-class.scrbl
bitmap-class.scrbl         compiled              fire.png                        libs.scrbl                   radial-gradient-class.scrbl
bitmap-dc-class.scrbl      conveniences.scrbl    font-class.scrbl                linear-gradient-class.scrbl  record-dc-class.scrbl
blurbs.rkt                 dc-intf.scrbl         font-list-class.scrbl           pdf-dc-class.scrbl           region-class.scrbl
brush-class.scrbl          dc-path-class.scrbl   font-name-directory-intf.scrbl  pen-class.scrbl              svg-dc-class.scrbl
brush-list-class.scrbl     draw-contracts.scrbl  gl-config-class.scrbl           pen-list-class.scrbl         unsafe.scrbl
color-class.scrbl          draw-funcs.scrbl      gl-context-intf.scrbl           point-class.scrbl            water.png
color-database-intf.scrbl  draw-unit.scrbl       guide.scrbl                     post-script-dc-class.scrbl

hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cat /usr/share/racket/pkgs/draw-doc/scribblings/draw/BRIEF-TRAPPED
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/tools/perf/arch/riscv

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3.8/multiprocessing/__pycache__$ cd /opt/linux/linux-5.4/tools/perf/arch/riscv
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/arch/riscv$ ls
Build  Makefile  WHISPER  include  util
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/arch/riscv$ cat WHISPER
Lucky listing!
The next clue is in: /usr/share/locale/so

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/arch/riscv$ cd /usr/share/locale/so
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/so$ ls -a
.  ..  .SNIPPET  LC_MESSAGES
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/so$ cat .SNIPPET
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{wyYmt3PpgjXaGHXX5_MG_tDY6ya.QX5IDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt the cumulative use of ls, cat and cd to work in and around directories.

## References 
Did not use any references for this challenge.

# MAKING DIRECTORIES
To create a /tmp/pwn directory and make a college file in it. Then run /challenge/run, which will check your solution and give you the flag.

## My solve
**Flag:** `pwn.college{0O2h6nqyXxu8PRuT7w9kz2UZc5E.QXxMDO0wiM4kjNzEzW}`

Firstly I used 'cd' to navigate to the directory '/tmp' and in that directory , I used my understanding of the "mkdir' command in order to create a new directory called '/tmp/pwn' as stated in the challenge. Next , I used the 'touch' command to create a new file called college in the '/tmp/pwn' directory and  the 'ls' command to list the files . Finally , I ran /challenge/run in order to capture the flag.

```
hacker@commands~making-directories:~$ cd /tmp
hacker@commands~making-directories:/tmp$ mkdir pwn
hacker@commands~making-directories:/tmp$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ ls
college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{0O2h6nqyXxu8PRuT7w9kz2UZc5E.QXxMDO0wiM4kjNzEzW}
```

## What I learned
Through this challenge I learnt about a new command called 'mkdir' which is used for making directories.

## References 
Did not use any references for this challenge.















