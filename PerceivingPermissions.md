# Percieving Permissions
## Overview:
let's look at the output above at a high level:

The File Type
The first character of each line represents the file type. In pwn_directory's case, the d indicates that it's a directory, and in college_file's case, the - represents that it's a normal file. There are other types as well, and you will encounter some of them later in your pwn.college journey.

The Permissions
The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting the permissions that the user who owns the file (termed the "owner") has to the file, 3 characters denoting the permissions that the group that owns the file (termed the "group") has to the file, and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file. We will learn all about these later in the module.

Ownership Information
There are two columns showing the user that owns the file (in this case, user hacker) and then the group that owns the file (in this case, also group hacker). You'll mess around with that here!

## 1. Changing File Ownership
### Question statement:
In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use chown to your heart's content as the hacker user (again, typically, this requires you to be root). Use this power wisely and chown away!

### Solution:
![Screenshot from 2025-06-02 08-42-36](https://github.com/user-attachments/assets/3b52bfc9-69b5-4728-a6ec-e73b0ba0384b)
1. chown is used to change the ownership of /flag to hacker.
2. Upon invoking cat /flag, we get the flag.

## 2. Groups and files
### Question statement:
In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user! Change the group ownership of the flag file, and read the flag!

### Solution:
![Screenshot from 2025-06-02 09-07-04](https://github.com/user-attachments/assets/7ee9364e-1cff-49c0-993e-9edd29dcaa19)
1. We use ```id``` command first.
2. Then we use ls -l /flag to check who has access to the file.
3. We change the group using ```chgrp```.
4. Now we access /flag using ```cat```.
5. The flag is obtained.

## 3. Fun with group files
### Question statement:
You've used hacker for the group before, but in this level, that is not going to work. I'll still allow you to use chgrp, but I have randomized the name of the group that your user is in. You will need to use the id command to figure that name out, then chgrp to victory!

## Solution:
![Screenshot from 2025-06-02 09-08-24](https://github.com/user-attachments/assets/cfbd726a-55ab-4535-8bee-04766beabde7)
1. We change the group of /flag, but to obtain the group, we need to get the group id first, which we get by using ```id``` command.
2. Once we get group id we write it in the ```chgrp``` command.
3. Then we run the ```cat /flag```.
4. This gives the flag.

## 4. Changing Permissions
### Question statement:
In this level, we will cover the former: modifying an existing mode. chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute. For example, to add read access for the owning user, you would specify a mode of u+r. write and execute access for the group and the other (or all the modes) are specified the same way. More examples:

u+r, as above, adds read access to the user's permissions
g+wx adds write and execute access to the group's permissions
o-w removes write access for other users
a-rwx removes all permissions for the user, group, and world

### Solution:
![Screenshot from 2025-06-02 09-13-42](https://github.com/user-attachments/assets/21234d76-5a98-4889-aaad-e54ad35f9b9a)
1. We first look up the permissions given to /flag.
2. We use ```chmod``` to change the permissions and give read permissions to others.
3. We use cat /flag to get the flag.

## 5. Executable files
### Question statement:
In this challenge, the /challenge/run program will give you the flag, but you must first make it executable! Remember your chmod, and get /challenge/run to tell you the flag!

### Solution:
![Screenshot from 2025-06-02 10-11-05](https://github.com/user-attachments/assets/392d8996-8320-4e41-a285-b978f3080b85)
1. We look up the permissions available to ```/challenge/run```.
2. We give it the required permissions.
3. We run the above code, giving us the flag.

## 6. Permission tweaking practice
### Question statement:
This challenge will ask you to change the permissions of the /challenge/pwn file in specific ways a few times in a row. If you get the permissions wrong, the game will reset and you can try again. If you get the permissions right eight times in a row, the challenge will let you chmod /flag to make it readable for yourself :-) Launch /challenge/run to get started!

### Solution:
![Screenshot from 2025-06-02 11-57-31](https://github.com/user-attachments/assets/29f97c71-2303-4609-81c8-fbaa5e5ad498)
![Screenshot from 2025-06-02 12-07-11](https://github.com/user-attachments/assets/9d78b285-5c29-43c0-b47e-ef34c4e2cbeb)
![Screenshot from 2025-06-02 12-07-48](https://github.com/user-attachments/assets/0977bb51-bb8d-4d83-a539-f3169c8f1dfe)
![Screenshot from 2025-06-02 12-08-07](https://github.com/user-attachments/assets/6bd7b821-90de-4da8-951e-f128ec0c19d7)


## 7. Permissions setting practice
### Question statement:
This level extends the previous level by requesting more radical permission changes, which you will need = and ,-chaining to achieve. Good luck!

### Solution:
![Screenshot from 2025-06-04 00-44-00](https://github.com/user-attachments/assets/5c1f0476-03cb-4264-aab3-c8f10b4db3b9)
![Screenshot from 2025-06-04 00-44-24](https://github.com/user-attachments/assets/0a410c2f-828f-4197-bd5f-5c1a45c48c88)
It is the same as the previous level but here we give permissions to group, user and others as u=,g=, and o=.

## 8. The SUID bit
### Question statement:
Now, we are going to let you add the SUID bit to the /challenge/getroot program in order to spawn a root shell for you to cat the flag yourself!

### Solution:
![Screenshot from 2025-06-04 00-50-54](https://github.com/user-attachments/assets/32137998-26aa-4642-ae8f-fe5d94c09361)
1. I first tried running `/challenge/pwn` but it didn’t exist, so I ran `/challenge/run` and learned about the SUID bit.
2. I checked `/usr/bin/sudo` with `ls -l` and confirmed it had the SUID bit set.
3. I viewed the `/challenge/getroot` script, which spawns a root shell.
4. I set the SUID bit on `/challenge/getroot` using `chmod u+s`.
5. I ran the script and successfully got a root shell.
6. Initially, `cat /flag` failed due to permission denial, but once in the root shell, I ran it again and retrieved the flag.
