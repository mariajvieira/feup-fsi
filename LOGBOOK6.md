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



