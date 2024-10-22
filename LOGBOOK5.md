## Buffer-Overflow Attack Lab - Set-UID Version


- Setup of the system:

> $ sudo sysctl -w kernel.randomize_va_space=0

> $ sudo ln -sf /bin/zsh /bin/sh


### Task 1

 - We compiled the ```call_shellcode.c```file and ran the -m32 version:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1LOGBOOK5_32.png)
-
*Image 1 - m32 shell.*

- As we can see, the shell was opened successfully.

- Then, we ran the 64 version:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1LOGBOOK5_64.png)
-
*Image 2 - 64 shell.*

- The shell opened successfully as well.

### Task 2