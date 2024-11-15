## CTF Semana #5 (Buffer Overflow)

First, we verified that the program's security features were as expected by running the following command:
> $ checksec program

After analyzing the source code of the program, we were able to answer the questions.

#### Is there any file that is opened and read by the program?
Yes, the program tries to open and read the file ```rules.txt```. This happens in the ```readtxt``` function, where the command ```cat rules.txt``` is constructed and executed using the system function.

#### Is there a way to control the file that is opened?
Yes, there is an indirect way to control the file that is opened. In the main function, there is a buffer overflow vulnerability in ```scanf```, which allows overwriting the ```fun``` pointer. By redirecting ```fun``` to ```readtxt``` and modifying the string in buffer to ```"flag"```, the program will attempt to open ```flag.txt``` instead of ```rules.txt```.

#### Is there a buffer overflow? If yes, what can you do?

Yes, there is a buffer overflow. The array buffer has only 32 bytes, but ```scanf("%45s", &buffer)```; allows reading up to 45 bytes, causing an overflow and enabling the overwriting of fun. 
With this vulnerability, we can overwrite the fun pointer to redirect the function call back to readtxt, and modify the value in buffer to ```"flag"```, so that ```readtxt``` will attempt to open ```flag.txt``` instead of ```rules.txt```.