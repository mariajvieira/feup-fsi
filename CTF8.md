# CTF Week #8 (SQL Injection)

By exploring the website, using the developer tools, we obtained:

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img1.png)

We discovered that the website has the wordpress version 6.7.1.

After that, we did some research to find any vulnerabilities in that version and found ```CVE-2023-4239```.
-- NOT SQL INJECTION ATTACK


After some research in the website, we founf the comment: 

![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img2.png)

We now know that the website uses WordPress Password Hashing (using phppass).