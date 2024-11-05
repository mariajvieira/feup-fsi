# Format-String Vulnerability Lab

## Environment Setup

First, we turned off the address randomization:

>  $ sudo sysctl -w kernel.randomize_va_space=0

Then, we compiled and installed the program.


## Task 1

After running the containers, we ran the following command:
> $ echo hello | nc 10.9.0.5 9090

We successfuly printed out ```hello```.
![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK6.png)

![Image 2.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/using%25d.png)
![Image 3.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Using%25d.png)

After some tries, we noticed only %n and %s crash the program:

![Image 4.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/using%25n.png)
![Image 5.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Using%25n.png)


![Image 6.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/using%25s.png)
![Image 7.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Using%25s.png)


## Task 2

### Task 2.A
To print out the data on the stack, we use the values ´´´ABCD´´´ which the ascii code is ´´´41424344´´´. 

![Image 8.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2_LOGBOOK6.png)

Considering the values are reversed, we can see the value ´´´44434241´´´ that represents the adress of ABCD.
After testing, we concluded that we needed 63 %x format specifiers so that the server program could print out the first four bytes of the input.

### Task 2.B

After finding the adress of the secret message on the server printout ´´´0x080b4008´´´, we converted it to little endian format: ´´´0x08400b08´´´.

![Image 9.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2_LOGBOOK6_img3.png)

We exploited the format string vulnerability, so we could access arbitrary memory data. We used printf followed by the converted adress, 63 %x specifiers until we reached the correct position of the adress and %s to print the content(secret message). The result was the following:

![Image 10.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2_LOGBOOK6_img2.png)