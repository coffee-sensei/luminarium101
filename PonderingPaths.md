# Pondering Paths
## Overview:
Thus far, you have invoked commands in several ways:

Through an absolute path (e.g., /challenge/run).
Through a relative path (e.g., ./run).
Through a bare command name (e.g., ls).
The first two cases, the absolute and the relative path case, are straightforward: the run file lives in the /challenge directory, and both cases refer to it (provided, of course, that the relative path is invoked with a current working directory of /challenge). But what about the last one? Where is the ls program located? How does the shell know to search for it there?

In this module, we will pull back the veil and answer this question! Stay with us.

## 1. The PATH variable
### Question: 
In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command!

### Method to solve: 
![Screenshot from 2025-06-04 11-58-43](https://github.com/user-attachments/assets/247e1d2c-cb49-4dbe-98ea-ff411f879248)

1. The rm command doesn't exist when the PATH is checked.
2. Run /challenge/run
3. You will get the flag.

## 2. Setting PATH
### Question: 
This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. Good luck!

### Method to solve:
![Screenshot from 2025-06-04 12-02-57](https://github.com/user-attachments/assets/c8f674ad-355d-4fe2-a7e8-cfea58ae4700)
1. Path is changed to /challenge/more_commands
2. /challenge/run is invoked.
3. Since win is present in the given PATH, the flag is displayed.

## 3. Adding Commands
### Question:
Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

### Method to solve:
![Screenshot from 2025-06-04 15-24-40](https://github.com/user-attachments/assets/66d9e45b-017a-4400-a9ac-677b880958e4)
1. A script called win is created with the given code:
``` bash
read flag < /flag 
echo "$flag"
```
2. The permissions are checked using ls -l win and changed to execution using octal values.
3. Path is set to where the script lies, i.e., ``` /home/hacker ```
4. /challenge/run is invoked in turn gives the flag.

## 4. Hijacking Commands
### Question:
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

### Method to solve: 

![Screenshot from 2025-06-04 15-29-32](https://github.com/user-attachments/assets/2cf75e2f-1f89-43b6-b69b-ba0cd2341678)
1. Just like how we created a script for win, we create a script for rm
2. The code is the same:
``` bash
read flag < /flag 
echo "$flag"
```
3. Permissions to rm is looked upon, and changed using ```chmod 777 rm```
4. Path is changed to ``` /home/hacker ```
5. /challenge/run is invoked, which gives the flag.
