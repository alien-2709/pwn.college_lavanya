# LAUNCHING SCREEN
Launch screen to obtain the flag.

## My solve
**Flag:** `pwn.college{cRjohCvQnGuLBSYvZwqQvg8h7fZ.0VN4IDOxwiM4kjNzEzW}`

Launched screen to obtain the flag.

```bash
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{cRjohCvQnGuLBSYvZwqQvg8h7fZ.0VN4IDOxwiM4kjNzEzW}
```

## What I learned
* screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

- Starting screen is super simple:

```hacker@dojo:~$ screen```
* you're working on something important over a remote connection, and your connection drops. With a normal terminal , everything's gone. With screen, your work keeps running, and you can reattach later.

## References 
No references.

# DETACHING AND ATTACHING
For this challenge, you'll need to:  

1. Launch screen
2. Detach from it.
3. Run /challenge/run (this will secretly send the flag to your detached session!)
4. Reattach to see your prize


## My solve
**Flag:** `pwn.college{YLGtgUq451Um4vUp0NN5glqnj_9.0lN4IDOxwiM4kjNzEzW}`

1. launched screen.
2. detached from it by using ctrl+a , followed by pressing d.
3. Next, ran /challenge/run to send flag.
4. reattach using screen -r.


```
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{YLGtgUq451Um4vUp0NN5glqnj_9.0lN4IDOxwiM4kjNzEzW}
Yes! Flag is: pwn.college{YLGtgUq451Um4vUp0NN5glqnj_9.0lN4IDOxwiM4kjNzEzW}
```

## What I learned
* You detach by pressing Ctrl-A, followed by d (for detach). This leaves your session running in the background while you return to your normal terminal.
```
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$
```
* To reattach, you can use the -r argument to screen:

```hacker@dojo:~$ screen -r```  
*  Ctrl-A is screen's activation key for all of its shortcuts in its default configuration. All screen functionality is activated by some command combination starting with Ctrl-A.

## References 
No references.

# FINDING SESSIONS
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys. 
You'll need to check each one until you find it. Don't forget to detach (Ctrl-A d) before trying the next session

## My solve
**Flag:** `pwn.college{k5ltmo9qd6bDE-idZyX9i9eySpe.01N4IDOxwiM4kjNzEzW}`

1.Used screen -r to see the sessions that are attached/detached .  
2.Then , I checked each session by reattaching to the using screen -r [name/pid].  
3.Found the flag in session 147 .

```

hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{k5ltmo9qd6bDE-idZyX9i9eySpe.01N4IDOxwiM4kjNzEzW}
pwn.college{k5ltmo9qd6bDE-idZyX9i9eySpe.01N4IDOxwiM4kjNzEzW}
```

## What I learned
* to find the right session to reattach to , we can list them:
```
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```
* The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to screen -r.

```hacker@dojo:~$ screen -r goodwork```

## References 
No references.

# SWITCHING WINDOWS
For this challenge, we've set up a screen session with two windows:  


* Window 0 has... well, you'll have to switch there to find out!
* Window 1 has a welcome message
* Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag.

## My solve
**Flag:** ` pwn.college{QJ1ZXrFoiUosAgAVAg88SWg-1ts.0FO4IDOxwiM4kjNzEzW}`

1.Used screen -r to attach to session .
2.Then,used ctrlA followed by 0 to switch to window 0 and obtained the flag.

```
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{QJ1ZXrFoiUosAgAVAg88SWg-1ts.0FO4IDOxwiM4kjNzEzW}
```

## What I learned
* Inside a single screen session, you can have multiple windows, like your browser has multiple tabs.
* These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

- Ctrl-A c - Create a new window
- Ctrl-A n - Next window
- Ctrl-A p - Previous window
- Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
- Ctrl-A " - bring up a selection menu of all of the windows

## References 
No references.

# DETACHING AND ATTACHING (tmux)
For this challenge:  

1. Launch tmux
2. Detach from it.
3. Run /challenge/run (this will send the flag to your detached session!)
4. Reattach to see your prize

## My solve
**Flag:** ` pwn.college{8mpuldqUxhQ_UiB0-9hodv3-qzx.0VO4IDOxwiM4kjNzEzW}`

1. Used tmux to launch it.
2. Used ctrlB+d to detach .
3. Ran /challenge/run to send flag to detached session.
4. Used tmux a to reattach and obtain flag.

```
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{8mpuldqUxhQ_UiB0-9hodv3-qzx.0VO4IDOxwiM4kjNzEzW}
Congratulations, here is your flag: pwn.college{8mpuldqUxhQ_UiB0-9hodv3-qzx.0VO4IDOxwiM4kjNzEzW}
```

## What I learned
* tmux (terminal multiplexer) It does all the same things but with some different key bindings. The biggest difference is that instead of Ctrl-A, tmux uses Ctrl-B as its command prefix.

* So to detach from tmux, you press Ctrl-B followed by d.
```
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$
```
* The commands also differ:
```
tmux ls - List sessions
tmux attach or tmux a - Reattach to session
```

## References 
No references.

# SWITCHING WINDOWS(tmux)
We've created a tmux session with two windows:  

* Window 0 has the flag!
* Window 1 has your warm welcome.
* Go get that flag

## My solve
**Flag:** `pwn.college{wBxs0Jv7UJMLJZMMzgebdQbEVtI.0FM5IDOxwiM4kjNzEzW}`

Explain how you arrived at the solution and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for bash.

```bash
(0)   - challenge_session: 2 windows
(1)   ├─> 0: bash-
(2)   └─> 1: bash*
(3)   - 1: 1 windows
(4)   └─> 0: bash*
(5)   - 2: 1 windows (attached)
(6)   └─> 0: bash*
(7)   - 3: 1 windows
(8)   └─> 0: bash*
(9)   - 4: 1 windows
(M-a) └─> 0: bash*
(M-b) - 5: 1 windows (attached)
(M-c) └─> 0: [tmux]*



┌ challenge_session (sort: index) ──────────────────────────────────────────────────────────────────────────────────────────────────┐│                                                                │to switch to window 0!                                            ││                                                                │                                                                  ││ ou found window 0!                                             │tmux window switching challenge!                                  ││ : pwn.college{wBxs0Jv7UJMLJZMMzgebdQbEVtI.0FM5IDOxwiM4kjNzEzW} │ly in window 1.                                                   ││ ultiplexing~switching-windows-tmux:~$ 
```

## What I learned
* Just like screen, tmux has windows. The key combos are different, but the concept is the same:

- Ctrl-B c - Create a new window
- Ctrl-B n - Next window
- Ctrl-B p - Previous window
- Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
- Ctrl-B w - See a nice window picker
* Tmux shows your windows at the bottom in a status bar that looks like:

```[0] 0:bash* 1:bash```
- The * shows your current window, and each entry also shows the process that the window was created to run.

## References 
No references.

