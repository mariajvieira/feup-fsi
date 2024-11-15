## CTF Week #5 (Buffer Overflow)

First, we verified that the program's security features were as expected by running the following command:
> $ checksec program

After analyzing the source code of the program, we were able to answer the questions.

#### Is there any file that is opened and read by the program?
Yes, the program tries to open and read the file ```rules.txt```. This happens in the ```readtxt``` function, where the command ```cat rules.txt``` is constructed and executed using the system function.

#### Is there a way to control the file that is opened?
Yes, there is an indirect way to control the file that will be opened. This can be achieved by exploiting the buffer overflow vulnerability present in the program.
In the main function, the function pointer ```fun``` initially points to ```readtxt```, but it is later overwritten to point to ```echo```.
The buffer overflow vulnerability allows overwriting the fun pointer to redirect it back to ```readtxt``` and pass a controlled string argument to open another file.

#### Is there a buffer overflow? If yes, what can you do?
Yes, there is a buffer overflow. The array buffer is only 32 bytes long, but the program uses the function call ```scanf("%45s", buffer)```, which allows up to 45 bytes to be written into the buffer. This causes a stack overflow, enabling us to overwrite the fun pointer.

### Attack
To exploit the vulnerability, we modified the ```exploit-template.py``` payload.

In order to do that, we overwrote the function pointer ```fun``` to point back to the ```readtxt``` function and provide the argument "flag" to readtxt, so it constructs the command ```cat flag.txt```.

First, we discovered the address of the ```readtxt```funcion using gdb:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF5_img1.png)

The address of readtxt was found to be 0x80497a5.

Then we started constructing the payload, by adding "flag" and a specific number of characters 'A' and the readtxt adddress.
After many tries and errors, we realized we needed to put the null terminator after "flag" (\x00) and 27 'A' characters.

#### Why 27 'A's?
The buffer in the program has a size of 32 bytes, but the scanf function allows up to 45 bytes to be read into it, causing a buffer overflow. To exploit this, we need to overwrite the function pointer (fun), which is located right after the buffer in memory. To do this, we first send the controlled string "flag\x00", which occupies 5 bytes (4 for "flag" and 1 for the null terminator). After this string, we need to fill the remaining space in the buffer with 27 'A' characters, ensuring that the overflow will reach the function pointer and overwrite it correctly. 

![Image 2.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF5_img2.png)

After sending the crafted payload to the remote server, the exploit worked as expected, and the flag was revealed:

![Image 3.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF5_flag.png)