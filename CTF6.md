### CTF Week #6 (Format Strings)


After running the ```checksec``` command, we obtained the following output:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF6_1.png)

We concluded that the only protection enabled in the binary is the stack canary, which helps prevent basic stack-based buffer overflow attacks by detecting stack corruption before the function returns. However, the binary lacks other critical protections like RELRO, PIE, and NX, making it vulnerable to several types of exploits.

Possible attacks include format string vulnerabilities, which can be used to read or write arbitrary memory addresses, potentially leading to control flow hijacking. Additionally, due to the absence of RELRO, attackers can perform GOT overwrite attacks, redirecting function calls to malicious code. The lack of PIE allows for predictable addresses, enabling Return-to-libc attacks. Finally, since the stack is executable, shellcode injection is also feasible.

After analyzing the source code, we were able to answer the questions:

#### Is there any file that is opened and read by the program?
   Yes, the program reads a file using the ```readtxt``` function. Specifically, it constructs a command using ```sprintf``` to read a file with the ```.txt``` extension. By default, the program reads a file called ```rules.txt```.

#### Is there any way to control the file that is opened?
   Yes, the filename can be controlled indirectly. The function pointer ```fun``` is initially set to point to ```readtxt``` and it is used to read ```rules.txt```. However, by exploiting the format string vulnerability present in the ```printf(buffer)``` statement, it may be possible to overwrite the function pointer ```fun``` to change its behavior. This means you could potentially alter the filename being read by pointing ```fun``` to read a different file like ```flag.txt```.

#### Is there a format string vulnerability? If so, what is it vulnerable to and what can you do with it?
   Yes, there is a format string vulnerability in this line:```printf(buffer);```
   This line uses user input directly in ```printf``` without specifying a format. This can be exploited to:
   - Leak memory addresses: Using format specifiers like ```%x``` or `%s`, an attacker can read values from the stack, potentially revealing addresses of variables or functions.
   - Arbitrary Memory Write: By using format specifiers like ```%n```, the attacker can write arbitrary values to specific memory addresses. This can be used to overwrite the function pointer ```fun``` to point to ```readtxt``` with a custom filename (e.g., ```flag```) instead of ```rules```, thereby making the program read ```flag.txt``` to reveal the flag.

### Attack

To exploit the vulnerability, we started by analizing the source code.

The program provided a hint by printing the address of a function pointer named ```fun```. We extracted this hint using string manipulation techniques to obtain the exact memory address. This address was critical because it pointed to the function we intended to overwrite.
We discovered the address of the ```readtxt``` funcion using gdb:
![Image 2.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF6_2.png)

The address of readtxt was found to be ```0x80497a5```.

Our goal was to overwrite the existing function pointer ```fun``` with this address so that we could force the program to read from ```flag.txt``` instead of ```rules.txt``` file.

Next, we tried to overwrite the function pointer ```fun``` with the address of the ```readtxt``` function, to cause the program to execute our desired command.

To craft our exploit, we prepared a prefix that would replace the default filename (using something like "flagnn" to hint at ```flag.txt```). We then used an automated technique to generate a format string payload. This payload was carefully constructed to write the address of ```readtxt``` into the location pointed to by the `fun` address. The exploit took into account the stack offset to ensure our input aligned correctly.

Once our payload was ready, we sent it to the program. If the exploit was successful, it would change the function pointer to point to ```readtxt```, with "flag" as the argument. This would make the program execute a command equivalent to reading `flag.txt`, ultimately revealing the hidden flag in the program’s output.

In summary, the exploit process involved extracting the function pointer address, finding the address of ```readtxt```, crafting a payload to exploit the format string vulnerability, and sending this payload to change the program’s behavior, thus obtaining the flag.

![Image 3.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF6_3.png)

![Image 4.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF6_4.png)


