# TRANSLATING CHARACTERS
In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Undo it with tr and get the flag.

## My solve
**Flag:** `pwn.college{ANGEmY5swSD6xPreMlFKuUKCbZd.01MxEzNxwiM4kjNzEzW}`

Using my understanding of the 'tr' command which translates the characters provided in the first argument with characters provided in the second argument , I was able to obtain the flag.

```
hacker@data~translating-characters:~$ /challenge/run | tr abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
yOUR CASE-SWAPPED FLAG:
pwn.college{ANGEmY5swSD6xPreMlFKuUKCbZd.01MxEzNxwiM4kjNzEzW}
```

## What I learned
I learnt about the command 'tr' , which translates characters it receives over standard input and prints them to standard output.

## References 
Did not use any references for this challenge.  


# DELETING CHARACTERS
Use tr -d to remove special characters like '^' and '%' from the flag and thus obtain it.

## My solve
**Flag:** `pwn.college{Av9BmvGxzwGYkdPzXFmMszavBbM.0FNxEzNxwiM4kjNzEzW}`

I first ran the command '/challenge/run ' and piped it into the 'tr -d' command which deleted the characters '^' and '%' by translating them into nothing .


```
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{Av9BmvGxzwGYkdPzXFmMszavBbM.0FNxEzNxwiM4kjNzEzW}
```

# What I learned
Through this challenge , I learnt about how we can use 'tr' command to delete characters by translating them into nothing . To do this , we must use 'tr -d' .

## References 
Did not use any references for this challenge.

# DELETING NEWLINES
There are a bunch of injected newlines in the flag. Delete them with tr's -d flag and the escaped newline specification.

## My solve
**Flag:** `pwn.college{U6BLRCfeYrXRJfnqxNEK3OGJO0k.0VNxEzNxwiM4kjNzEzW}`

I ran the command '/challenge/run' and piped it into the command 'tr -d' followed by the escaped newline specification i.e. "\n" in order to delete all the newlines.

```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{U6BLRCfeYrXRJfnqxNEK3OGJO0k.0VNxEzNxwiM4kjNzEzW}
```

## What I learned
I learnt how using 'tr' , we can translate "\n" new line characters as well as delete them . 

## References 
Did not use any references for this challenge.   '


# EXTRACTING THE FIRST LINES WITH HEAD
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag.

## My solve
**Flag:** `pwn.college{wiWitO9EFHjNvtfyzcOPXHCTWGc.0lNxEzNxwiM4kjNzEzW}`

I first ran '/challenge/pwn' and piped it into 'head -n 7' which will print the first 7 lines of the output of '/challenge/pwn'. Next I piped it onwards into '/challenge/college'.Thus the flag is obtained.

```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{wiWitO9EFHjNvtfyzcOPXHCTWGc.0lNxEzNxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that the 'head' command is used to display the first few lines of its input.By default, it shows the first 10 lines, but you can control this with the -n option.

## References 
Did not use any references for this challenge.  


# EXTRACTING SPECIFIC SECTIONS OF TEXT
In this challenge ,the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

## My solve
**Flag:** `pwn.college{8A-AVyaVdLCt8aWCjVpAhnCsfDb.01NxEzNxwiM4kjNzEzW}`

1.Run '/challenge/run' .  
2.Pipe it into 'cut -d " " -f 2' as the delimiter is the space character and the field number is 2 as the first field would be random numbers and the second would be the flag characters.  
3.Pipe the output further into 'tr -d "\n"' in order to delete the newline characters and obtain the flag.


```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2|tr -d "\n"
pwn.college{8A-AVyaVdLCt8aWCjVpAhnCsfDb.01NxEzNxwiM4kjNzEzW}
```

## What I learned
The 'cut' command used to extract specific columns.   
For example, imagine that you have the following data file:  
```
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```

```
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```
The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

## References 
Did not use any references for this challenge.  

# SORTING DATA
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end.

## My solve
**Flag:** `pwn.college{snxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}`

Through my understanding of the 'sort' command that sorts file content alphabetically , I used 'sort /challenge/flags.txt' to find the flag.

```
hacker@data~sorting-data:~$ sort /challenge/flags.txt
ovm.bolkege{snxEk3jauJVTtlcdWX8P1VLVMfS.0FM0MCOxwiM4kjMzEzV}
ovn.cnllege{smwEj3iauIVUsmcdXY7P0UKVLfT.0FL0MDNwwiL4kjNzEyW}
ovn.cokkege{smwDk4jauJVTtmcdXX8P1VKWMfT.0EM0LDOxwiL4jiNzDyW}
ovn.collegd{snxDk3iatJUUslccXY8P1UKWMeT.0FM0MDOwwiL3kjNyDzW}
owm.bnlkefe{smwDj4jauJVTtmcdWY8O1ULWMfT.0FM0LDOwviL4kjNyEyW}
owm.bolkdge{snxEk4iauJVUsmcdXY8P1VLWLeT.0FM0MDOxwiM4kjNyDzW}
owm.bollefe{rnxDk3jatIVUtlcdXX8P1ULWLfS.0FM0MDOwwiM4jjNzDzW}
owm.colkefe{snxDj4jauJVUsmbcXY8O1VKWLfT.0EM0LDNwwhM4kiMzEzW}
own.bnkldge{snxDj4jatJVUtmcdWX8O1VLVMfS.0FM0MDOxviM3kjNzEyW}
own.bokkefe{rnxEk4jatIVTsmccXX8P1ULWMfS.0FM0LDOwviM4kjNzEzV}
own.bollege{snxEj4jauIVUtmcdXY8P1VKVMeT.0FL0LDOwwiM3jiNzEzW}
own.cnllegd{snwDj4jauJVUtmcdXY7P1VKWLfS.0EL0MDNxwiL4kjNzEyW}
own.coklege{smxEk4jauIVUtmbdXY8P1ULWMeT.0FM0MDOxwiM4kjNzEzW}
own.colkefd{smxDk3jatJVUtlccXY8P1VLWLfT.0FM0LDOxwiM4kiMzEyV}
own.colldge{smwEj4jauJVTtlcdWY8P1VLWLeS.0FM0MDOxwiM3kjNzEzW}
own.college{snxEk3jatJUTsmcdXY8P1VLVMfT.0FM0LCOxwiM4kjNzEzW}
own.college{snxEk4jauJVTtlbdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pvm.colkege{smxDk3jauJUUtmccXX8P0VLWMfT.0FM0MDOxwiM4kjNzDzW}
pvm.collefe{rnxEk4jatJVTtmcdWX8P1VLWLeS.0FM0LDNxwhL3kjMzEyW}
pvm.college{snxDk4iauJVUslcdXY8P1ULWLeS.0FM0MDOwvhM4jiNzDyW}
pvn.bnklege{snxEj4jauJVTtlccWY8P1VLWMfT.0EM0MDOwwiM3kjNzEyW}
pvn.bollefe{rnwEk4iauJUUtmbdXX8P1VLVMfT.0EM0MDOxwiL4kjNzEzW}
pvn.bollefe{snwEk4jauJUUsmcdXX7P0VLVMfT.0FM0MDOwwiM4kjNzEyW}
pvn.cnkkefd{smxDj3jauJUTtmbcXX7P1VLWMfS.0EM0MDOxwiM4kjMyEzW}
pvn.cnklege{snxEk4jauIVUtmcdXY8O0ULWMfT.0FM0MDOwwiM3kiNzDzW}
pvn.cnlkege{smxEk4iatJVUtlccXY8P0VLWLfS.0FM0LDOwviL4kiMzEzW}
pvn.cnllege{smxEk3jauJVUtlcdXY8P1ULVMfS.0FL0MDNxwiL3jjMyEzW}
pvn.cnllege{snxEk4iatJVUsmcdXY8O0VLWMfT.0FM0LCOxwiM3kjNzEyW}
pvn.coklegd{rmxEj4jauJUUtlcdXY8O1VLWMfS.0FM0MDOxviL4kjMzEzV}
pvn.colkefe{smxDk4jauJUTtmcdWY7O1VLVMfS.0EL0LCOxviM4jiMyEzW}
pvn.colldge{smxDk3iauJVTtmbdXY7O1VKVMfT.0FL0MDNxwiM4kjMzEzW}
pvn.college{smxEk4jauJVUtmbdXY8O1VLWMfT.0FL0LDOxwiL4kiMzEzW}
pvn.college{snxEj4jauJVUtmcdXX8P0VLWMfT.0FM0MDOxwiM4kjNzEzW}
pvn.college{snxEk4jatJVUtmcdXY8P1VLWMeT.0FM0MDOxwiM4kjNzEzW}
pwm.bnllegd{smxDj3jatJUUtmbdXX8P0VLVLfT.0EL0MCNxwiM4jjNyDyV}
pwm.cnlkdgd{smwEk4jauJVUtmbdWY8P0VLWMfT.0EM0MDNxwiM4jjNzEzW}
pwm.cnlkege{snwEk3jauJVUtlccXX7P1VLVMfT.0EL0MDOxwiM4kiNyEzW}
pwm.cnlldgd{snxEj4jauJVUtmccXY8P1VLWMfT.0FM0LDOxwiM4kjNzEzW}
pwm.cnllege{rnxEj3iauJVTtlcdXY8O1VLWMfT.0FM0MCNwwiM4jjNzDyW}
pwm.cokkege{rnxDk4jatJVUtmcdXY7P1VLWMeT.0EM0LDNwwiM4kiNzDzW}
pwm.cokkege{snxEk3jauIVTtmcdXX8P1ULVMfS.0FL0MCOxwhM4kiMzEyW}
pwm.colkefe{snxDk4jauIVUslcdXY8P1VLWLeS.0FM0MDNxwiL3jiMyEzW}
pwm.colldge{snxEj3jatJVUtmccXX8P0VLWLfT.0FL0MDOxwhM4kiNzDyW}
pwm.college{rnxEk4jauJVUtmcdXY7P1VLWMfT.0EM0MCOxwiM3kjNyDzV}
pwm.college{snxEk4jauJVTtmcdXX8P1VLWMeT.0FM0LCOxwiL4kjNyEzW}
pwn.bnlkege{smwEj4iauJUUtlccXY8P1VKVLfT.0FM0MCNxwhM4kjNzEzW}
pwn.boklege{snxEj4jauJVTtmbdXY8P1VLWMfT.0FM0MDOxwhM4kiMzEzW}
pwn.bolkefe{rnxEj4jauJVUtlcdXY7P1ULWMfT.0FM0MDOxwiM4kjNzEzV}
pwn.bolldge{rmwEk4jauJUUsmcdWY8P1VLWLeS.0FM0MDOxwiM4kjMzEyW}
pwn.bollegd{snxEj3jauIVTtmbdWX8O1ULVMfT.0FM0MDOxwhM3jjMyDzW}
pwn.bollegd{snxEk3iauJVUtmcdXY8P1VKWMfT.0FM0MCNxwiM3jjNyEzW}
pwn.bollege{snxEk4jauJVUtlbcXY8P1UKWMfS.0FM0LDNxwiM4kjNzEzW}
pwn.bollege{snxEk4jauJVUtmccXY7P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pwn.cnkkefe{snwEk4jauJUUsmcdXY7P1VKVMeS.0FL0LDNxwhM3kjNzEyW}
pwn.cnklefe{smwDj4jauIVUtmcdXY8P1VLWLfS.0FM0MDNwwiL4jjNzEzW}
pwn.cnklege{snxEj4jatJVUtmcdWX8P1VKVMfT.0FM0MCOxwiM4kjNzEzW}
pwn.cnllefd{smwDk4jatJVUtmccXX8P1VKVLfS.0FM0MCOwwiM3kjMzEyV}
pwn.cnllefe{rnxEk3jauJUUsmccXY7P1VLWLeS.0FM0MDOxwhM4kjMzDzW}
pwn.cnllefe{snxEk3iauIVUtmccWX8P1ULVLfT.0EM0LDNxwiL4kjNzEzW}
pwn.cnllegd{snxEj4jauJVUtmcdXX8P1VLWMfS.0FM0MCOxwiM4kjNzEzW}
pwn.cnllege{snxDk3iauIVUslbcWY7P0VLVMfS.0EM0MDOxviL4jjNzEzW}
pwn.cokkdge{rnxEj4jatJVUslccWX7O1VLWLfT.0EL0LDOxviL4kjNzEzW}
pwn.cokkegd{rnxEj4jatJVUtmbcXX8P0VLWLeT.0FL0LDNxviM4kjMzDzW}
pwn.cokldfd{snxDj4jauJUUslccXX8P1VLWMeT.0EM0MCOxwhL4kjNzEzW}
pwn.cokldge{snxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzDzW}
pwn.coklege{snxEk4jauIVTtmcdXY8P1VLWMfT.0FM0MDOxwhL4kjNzEyV}
pwn.colkegd{snxEk4jauJVUtmbdXY8P1VLWMfT.0FM0MDNxwiM4kjNzEzW}
pwn.colkege{rnxEj4jauJVUtlccXY8P1VLWMfT.0FM0MDOwwiM4kjNzEzW}
pwn.colkege{snwEk4jauIUUtmccXY8O0VLWMfT.0FM0MDOxwiM4kiNzEzW}
pwn.colkege{snxEj3jauJVUtmcdXX7P1VLWMeT.0FM0MDOwwiM4kiMzEyW}
pwn.colkege{snxEj4jatJVUsmbdXX8P1VKVLeT.0FM0LDNxwiM3kjMzDzW}
pwn.colldfd{rnxEk4jauIVUtmcdXX7P1VLVLfS.0FM0LCOwviL4kiMyEzV}
pwn.colldfe{rmxDk4jauJUUtmbdXX7P0VLVMeT.0EM0MCOxwiL4kiNzEyW}
pwn.colldgd{snxEk4iatIVUtmcdXY8O1VLWMfT.0FM0MDNwwiL4kjNzEzW}
pwn.colldge{rnwEk4jatJVUtmcdXY8P1VLWLfT.0FM0LDOxwiM4kjNzEzW}
pwn.colldge{smxEk4jauJVUtmcdXY8P1VLVMfS.0FL0MDOxwiM4kjNzEzW}
pwn.colldge{snxEj4iauJVUsmcdXY8P1VLWMfT.0FM0MCNxwiM3kjMzEyW}
pwn.colldge{snxEk3jauIVTtmcdXY8P1VLWMfT.0FM0LDOwwiM4kjNyEzW}
pwn.colldge{snxEk4jauJUUtmcdXX8P0ULVMeT.0FM0MDOxwhL3kiNzEzV}
pwn.colldge{snxEk4jauJVUtmccWY8P1VLWMfT.0FM0MDOxwiM4kjNzEyW}
pwn.colldge{snxEk4jauJVUtmccXY8P1VLWMeT.0FM0MDOxwiM4kjNzEzW}
pwn.colldge{snxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzDzW}
pwn.collefd{snwEk4jauIVUtmcdXY8P1UKWMfT.0FL0MDOxwiM4kjNzDzW}
pwn.collefe{smxEk4iauJVUtlcdXY8P1VLWMfT.0FM0MDOxwiM4kjNyEzW}
pwn.collefe{snxEk4jauIVUtmcdXY8P1VLWMfT.0FM0MDOxwiL4kjNzEzW}
pwn.collegd{smxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzDzW}
pwn.collegd{snxEk4jauJVUtlccWY8P1VLWMfS.0FL0LDOxwiM4kjNzEzW}
pwn.collegd{snxEk4jauJVUtmcdXY8P1VKWMfT.0FM0MDOxwiM3kjNzEzW}
pwn.college{rmwEk4jatIVUtmccWY7P0UKWMfT.0FM0MCOwviM4jjNyEzW}
pwn.college{smxEk3iauIVTtmcdXY8O1VLWMfT.0FM0LDOxwiM4kjNzEzV}
pwn.college{smxEk4jauJVUtmcdXY7P1VLWMfT.0FM0MDOxwiM4kjNyEzW}
pwn.college{smxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxviM4kjNzEzW}
pwn.college{snxEj4jauJVUslcdXY8P1VLWMfT.0FM0MDNxwhM4kjNzEzV}
pwn.college{snxEk3jauJVUtmcdXY8P1ULWMfT.0FM0MDOxwiM3jjNzEzW}
pwn.college{snxEk4iauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pwn.college{snxEk4jauJUUsmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pwn.college{snxEk4jauJVUsmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pwn.college{snxEk4jauJVUtlcdWY8P0VLVMfT.0FM0MDOxviM4kjNyDzW}
pwn.college{snxEk4jauJVUtmccXX8P1VLWMfT.0FM0LDOxwiM4kjNzEzW}
pwn.college{snxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
pwn.college{snxEk4jauJVUtmcdXY8P1VLWMfT.0FM0MDOxwiM4kjNzEzW}
```

## What I learned
Through this challenge , I learnt that files (or output lines of commands) aren't always in the order you need them. The 'sort' command helps you organize data. It reads lines from input (or files) and outputs them in sorted order.  
By default, sort orders lines alphabetically. Arguments can change this:  

1.-r: reverse order (Z to A)  

2.-n: numeric sort (for numbers)  

3.-u: unique lines only (remove duplicates)  

4.-R: random order.  


## References 
Did not use any references for this challenge.

