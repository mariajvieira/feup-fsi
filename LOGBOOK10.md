## Hash Length Extension

#### Task 1

First we picked a uid number from the ```key.txt```file: **1001:123456**.

We built the R message: ***123456:myname=MariaVieira&uid=1001&lstcmd=1***.

To calculate the MAC, we ran the command:
> $ echo -n "123456:myname=MariaVieira&uid=1001&lstcmd=1" | sha256sum

> **1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e  -**

Then, we built the request and sent it using the browser: 

http://www.seedlab-hashlen.com/?myname=MariaVieira&uid=1001&lstcmd=1mac=1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e

This didn´t work, so we tried to use 10.9.0.80 in the url:

http://10.9.0.80/?myname=MariaVieira&uid=1001&lstcmd=1&mac=1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e&subid1=20241206-1030-1288-97a0-15adcfd528ba

This time, it worked, showing the files successfully:


![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK10_2.png)


Then, we did the download request:
- We had to calculate the MAC again with ```echo -n "123456:myname=MariaVieira&uid=1001&lstcmd=1&download=secret.txt" | sha256sum```
- Sent the updated url: 
> http://10.9.0.80/?myname=MariaVieira&uid=1001&lstcmd=1&download=secret.txt&mac=289e9016b7caf160b0b116505c9452ac870b83598d95df94c221c47393d264d5

The request was successful, showing the content of ```secret.txt```!

![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK10_3.png)

#### Task 2

#### Task 3