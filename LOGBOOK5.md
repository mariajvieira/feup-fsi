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

Before compiling the vulnerable program, we disabled the StackGuard and the
non-executable stack protections and made it a root-owned Set-UID program.

> $ gcc -DBUF_SIZE=100 -m32 -o stack -z execstack -fno-stack-protector stack.c

> $ sudo chown root stack 

> $ sudo chmod 4755 stack 



Next, we changed the value of the L1 variable acoording to our group number:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2LOGBOOK5.png)

*Image 3 - L1 variable.*

And ran ```make stack-L1``` successfully.


### Task 3

