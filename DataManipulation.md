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
I learnt about the command 'tr' which is used to translate basically 

## References 
Add an references or videos you used while solving the challenge.
