## Hash Length Extension

#### Task 1

First we picked a uid number from the ```key.txt```file: **1001:123456**.

We built the R message: ***123456:myname=MariaVieira&uid=1001&lstcmd=1***.

To calculate the MAC, we ran the command:
> $ echo -n "123456:myname=MariaVieira&uid=1001&lstcmd=1" | sha256sum
> **1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e  -**

Then, we built the request and sent it using the browser: 
http://www.seedlab-hashlen.com/?myname=MariaVieira&uid=1001&lstcmd=1&mac=1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e


#### Task 2

#### Task 3