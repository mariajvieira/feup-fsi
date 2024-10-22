## Buffer-Overflow Attack Lab - Set-UID Version



Setup of the system:

Disabling the address randomization:

> $ sudo sysctl -w kernel.randomize_va_space=0

Changing shell create a symbolic link from /bin/sh to /bin/zsh, making our future attack easier:

> $ sudo ln -sf /bin/zsh /bin/sh


### Task 1

We compiled the ```call_shellcode.c```file and ran the -m32 and 64 versions:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1LOGBOOK5_32.png)

*Image 1 - m32 shell.*


![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1LOGBOOK5_64.png)
-
*Image 2 - 64 shell.*

The shell opened successfully in both.

### Task 2




