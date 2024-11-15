## CTF Semana #5 (Buffer Overflow)

First, we verified that the program's security features were as expected by running the following command:
> $ checksec program

After analyzing the source code of the program, we were able to answer the questions.

#### Is there any file that is opened and read by the program?
Yes, the program tries to open and read the file ```rules.txt```. This happens in the ```readtxt``` function, where the command ```cat rules.txt``` is constructed and executed using the system function.

#### Is there a way to control the file that is opened?
Yes, there is an indirect way to control the file that will be opened. This can be achieved by exploiting the buffer overflow vulnerability present in the program.
In the main function, the function pointer ```fun``` initially points to ```readtxt```, but it is later overwritten to point to ```echo```.
The buffer overflow vulnerability allows overwriting the fun pointer to redirect it back to ```readtxt``` and pass a controlled string argument. This causes the program to construct the command ```cat flag.txt```, opening the ```flag.txt``` file instead.

#### Is there a buffer overflow? If yes, what can you do?

Yes, there is a buffer overflow. The array buffer has only 32 bytes, but ```scanf("%45s", &buffer)```; allows reading up to 45 bytes, causing an overflow and enabling the overwriting of fun. 
With this vulnerability, we can overwrite the fun pointer to redirect the function call back to readtxt, and modify the value in buffer to ```"flag"```, so that ```readtxt``` will attempt to open ```flag.txt``` instead of ```rules.txt```.