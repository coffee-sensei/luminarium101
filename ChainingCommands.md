# Chaining Commands
## Overview:
In the piping module, you've explored the concept of using several commands, with data flowing between them via pipes, to accomplish something slightly more complex than the individual commands can do. Of course, this concept also applies independent of the data transfer: sometimes, you might want to run several commands in quick succession to achieve up some cumulative effect.

This module will cover a few ways, aside from piping, that commands can be chained. By the end, you'll be on your way to writing shell scripts!

## 1. Chaining with Semicolons
### Question statement:
In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.

### Solution:

![Screenshot from 2025-06-04 11-39-17](https://github.com/user-attachments/assets/5cba2109-fab2-434f-92eb-5d82d1cb01ed)
1. As implied in the question, ```/challenge/pwn``` and ```/challenge/college``` is written together as ```/challenge/pwn ; /challenge/college```.
2. This gives the flag.

## 2. Your first Shell Script
### Question statement:
Same as last level, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash!

### Solution:
![Screenshot from 2025-06-04 11-46-51](https://github.com/user-attachments/assets/c8247381-904c-47e8-bd12-1316fb43a464)
1. A script x.sh is created with the following commands:
   ```bash
   /challenge/pwn
   /challenge/college
   ```
2. This script is run with the command ```bash x.sh```
3. This will invoke the flag.

## 3. Redirecting Script Output
### Question statement:
In this level, we will practice piping (|) from your script to another program. Like before, you need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command!
### Solution:

![Screenshot from 2025-06-04 11-50-44](https://github.com/user-attachments/assets/857b019f-c2d8-4f88-85ae-d6dcc7d43309)

1. x.sh is created.
2. bash x.sh is piped with /challenge/solve using ``` | ```
3. This gives the flag.

## 4. Executable Shell Scripts
### Question statement:
Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash!

### Solution

![Screenshot from 2025-06-04 11-54-53](https://github.com/user-attachments/assets/bf3668b7-dfca-47f5-b887-097517a0c382)

1. A script sc.sh is created with   ```/challenge/solve``` in it.
2. First I have tried running it, when it gave me an error.
3. So I looked up its permissions -> which had only read permissions and no execution permissions
4. Execution permissions were added.
5. The shell is executed upon running, giving the flag.
