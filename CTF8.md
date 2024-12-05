# CTF Week #8 (SQL Injection)

By exploring the website, using the developer tools, we obtained:

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img1.png)

We discovered that the website has the following plugins:
- Wordpress version 6.7.1.
- NotificationX version 2.8.1.
- FontAwesome version 4.7.0.

After that, we did some research to find any vulnerabilities in that plugins related to SQLinjection.
We found **CVE-2024-1698** on **WordPress NotificationX** .


After some research in the website, we found the comment: 

![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img2.png)

We now know that the website uses WordPress Password Hashing (using phppass).