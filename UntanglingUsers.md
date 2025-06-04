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
