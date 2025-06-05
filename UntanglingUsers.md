# Untangling Users
## Overview:
In this module, we'll explore various user shenanigans, learn the intended ways to switch users to administer the system, and have fun along the way!

## 1. Becoming root with su
### Question statement:
In this challenge, we will cover the older one, su (the switch user command). This is not typically used to elevate to root access anymore, but it is an elegant utility from a more civilized time, and we'll cover it first.
Because it has the SUID bit set, su runs as root. Running as root, it can start a root shell! Of course, su is discerning: before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password.
This check against the root password is what obsoletes su. Modern systems very rarely have root passwords, and different mechanisms (that we will learn later) are used to grant administrative access.
But THIS challenge (and only this challenge) does have a root password. That password is hack-the-planet, and you must provide it to su to become root! Go do that, and read the flag!

### Solution:
![Screenshot from 2025-06-04 11-23-01](https://github.com/user-attachments/assets/823dd876-3f65-4c13-8757-ec265daab807)
1. su is entered, and password, as given is entered, giving root access.
2. /flag is invoked, giving the flag.

## 2. Other users with su
### Question statement:
In this level, you must switch to the zardus user and then run /challenge/run. Zardus' password is dont-hack-me. Good luck!

### Solution:
![Screenshot from 2025-06-04 11-24-36](https://github.com/user-attachments/assets/0dae5bb6-61f5-4a52-97ee-d2838ef8d70a)

1. su is provided to zardus, with the command ```su zardus```.
2. Now, ```/challenge/run``` is invoked, giving the flag.

## 3. Cracking passwords
### Question statement:
John the Ripper cracked Zardus' leaked password hash to find the real value of password1337. Poor Zardus!

This level simulates this story, giving you a leak of /etc/shadow (in /challenge/shadow-leak). Crack it (this could take a few minutes), su to zardus, and run /challenge/run to get the flag!

### Solution:
![Screenshot from 2025-06-04 11-32-02](https://github.com/user-attachments/assets/dcb2a87e-d676-46e0-af85-666eeff9b8d5)

1. I run```john /challenge/shadow-leak```
2. This creates a new directory ```/home/hacker/.john```
3. Password is cracked, it is ```aardvark```
4. This is used to login to zardus.
5. Now /challenge/run is ran, giving out the flag.

## 4. Using sudo
### Question statement:
Unlike su, which relies on password authentication, sudo checks policies to determine whether the user is authorized to run commands as root. These policies are defined in /etc/sudoers, and though it's mostly out of scale for our purposes, there are plenty of resources for learning about this!

So, the world has moved to sudo and has (for the purposes of system administration) left su behind. In fact, even pwn.college's Practice Mode works by giving you sudo access to elevate privileges!

In this level, we will give you sudo access, and you will use it to read the flag. Nice and easy!

### Solution:
![Screenshot from 2025-06-04 11-36-46](https://github.com/user-attachments/assets/51665b7b-ca53-45a1-b7cc-ebf165f60711)
1. We check if /flag exists using grep.
2. Using sudo, we invoke /flag file with cat.
3. This gives us the flag.
