## Public Key Infrastructures

### Task 1

We set up the certificate and ran the commands: 

> openssl x509 -in ca.crt -text -noout
> openssl rsa -in ca.key -text -noout

From the output, we answered to the questions:

- **What part of the certificate indicates this is a CA’s certificate?**

We can identify that is a CA certificate in the Basic Constraints field, whith ```CA: TRUE```.

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK11_1.png)

- **What part of the certificate indicates this is a self-signed certificate?**

The certificate is self-signed because the Issuer and Subject fields are identical. 

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK11_2.png)


- **In the RSA algorithm, we have a public exponent e, a private exponent d, a modulus n, and two secret
numbers p and q, such that n = pq. Please identify the values for these elements in your certificate
and key files.**

Public exponent: 
```
65537 (0x10001)
```

Private exponent:
```
36:3e:c0:42:33:7e:31:8f:91:3d:13:40:85:f1:b2:
ff:3c:41:2f:fb:b5:f6:77:59:a8:a3:a8:e4:47:0f:
ff:d9:41:aa:7b:58:15:0c:b4:c5:fd:90:a4:99:f5:
1d:09:b7:53:ed:66:8b:d6:80:55:0d:f3:6e:6a:47:
ac:6c:c6:de:15:a8:66:49:3a:ed:02:f6:ed:81:df:
c1:44:1b:80:d0:42:1b:8f:9b:18:92:2e:a7:d5:73:
c1:1a:65:71:fe:78:74:06:cb:08:3b:dc:5d:c3:2e:
fe:20:3b:4f:ab:cd:1b:38:ab:4f:cf:58:aa:e8:da:
76:26:f2:2e:46:3e:f4:90:51:51:be:2a:b7:3b:3a:
f3:ef:d8:bd:d4:ed:e1:9f:72:0b:2b:f9:b9:64:da:
e4:12:f9:7e:b4:fb:7b:c9:15:fa:a7:08:72:34:02:
7d:9e:d8:ed:f9:e6:96:78:b1:ae:17:dd:cd:d7:cd:
30:93:d4:41:a7:43:ac:e2:a5:6a:da:5d:28:ae:e2:
e8:2d:85:4e:63:b2:72:6c:6a:dc:6a:79:b1:2a:7b:
44:5a:48:ac:e6:6e:97:37:33:46:15:19:a0:69:55:
ef:ff:76:fe:4c:6e:56:d5:be:2d:c5:24:45:48:42:
d4:12:f9:e3:71:80:2b:7b:fd:1d:d4:7e:66:b0:3c:
69:41:77:0b:ec:7c:83:c1:9c:0f:c9:ae:27:97:5b:
f0:00:3c:a7:a5:bd:d2:9f:2f:15:83:fb:f5:69:b1:
d2:82:f6:ec:0a:e9:6c:e3:17:d9:85:8a:38:88:99:
32:c0:2c:4d:67:7e:9a:57:8b:0c:64:35:98:23:8a:
bd:3e:4e:8b:18:ce:31:9b:72:41:29:a3:e3:09:a6:
74:52:5b:2d:fe:b1:63:cb:0c:fb:15:6c:13:c9:aa:
77:14:6b:84:c5:ec:a8:95:c2:73:b6:6f:be:3b:12:
25:3e:b2:51:2d:81:e2:3f:55:e1:71:a7:6e:0e:2a:
c0:5d:06:6d:2a:0f:82:a9:bb:e7:78:00:8c:2e:fa:
3d:8a:e0:1c:f3:6e:d0:b7:b7:37:54:7d:15:6e:fe:
0c:07:a1:fa:9f:cc:42:7b:95:e6:7c:db:3e:b0:36:
46:56:70:c4:21:18:38:17:0c:58:dc:eb:cb:11:2a:
02:15:bd:28:32:33:fc:15:9b:c5:f6:fc:9f:5f:1e:
c8:cb:48:00:27:e7:6e:51:14:1c:d8:f3:b7:d7:f4:
3b:28:22:42:ef:69:80:32:7b:a7:e1:40:a2:6b:f3:
19:59:99:e9:71:47:f7:32:e0:7a:0c:90:b8:13:96:
e2:57:da:2b:32:b3:e3:77:c5:a3:d9:2c:a1:da:cb:
a5:e9
```

Modulus: 
```
00:b9:ce:d2:5f:9c:3e:6b:24:df:66:c7:4d:af:e2:
25:fc:29:ce:0a:cb:db:79:93:38:da:01:47:38:95:
60:d7:ea:b8:21:e4:48:bd:34:3f:22:e2:e1:52:63:
8b:26:f5:d9:75:f4:64:79:4a:61:bf:9e:7e:2d:b3:
c9:df:b4:e6:de:d6:83:d8:93:d6:b6:65:20:1a:e0:
b8:94:4d:66:7d:6b:d0:af:91:9f:a3:b1:e7:61:87:
47:a8:4f:30:b8:cd:c3:95:1c:3b:8e:0a:78:a1:16:
e7:40:47:d7:db:ce:fc:6a:19:c0:13:9f:b9:46:d0:
66:1a:60:a2:8e:8e:75:ce:fe:1c:a2:51:cf:c5:35:
1b:97:83:40:f4:a9:a7:a5:4d:1a:c8:1c:a5:2e:6c:
4d:3d:ef:30:5d:51:94:9f:48:8e:85:40:77:5d:c9:
64:5b:ce:0b:dd:9f:db:d3:4d:15:97:ae:ea:6a:04:
9d:d5:f9:3d:a9:5f:0e:5b:d8:43:ef:e3:34:d3:30:
df:2a:91:4c:d7:1c:56:32:1b:3b:6e:8c:dd:c8:50:
8d:b4:a3:40:03:33:02:df:3a:c2:1b:98:38:7b:e2:
98:6a:93:c8:41:72:87:35:6d:72:e3:43:95:42:84:
eb:2b:fa:3e:ff:af:20:3e:e3:63:5e:fa:c5:81:45:
df:31:2a:33:4e:b7:2b:c4:3d:6c:76:54:d6:02:d2:
b9:69:25:be:2f:75:f3:58:4b:1d:c2:11:c7:9d:07:
f3:3f:9e:11:38:95:99:87:42:74:fd:5c:64:08:32:
05:ee:64:fd:ff:7f:66:10:0a:99:0e:50:27:df:f7:
09:78:4e:fa:a7:6c:e6:41:90:69:f8:11:72:aa:e6:
97:40:ff:de:17:6d:df:9b:bd:a6:e2:51:81:0b:b4:
a6:eb:81:2f:a5:69:11:89:34:71:1a:09:a9:ef:ee:
d2:a9:38:54:18:3c:80:61:41:85:bd:00:ba:83:31:
78:00:52:c7:ad:13:4f:ef:d1:be:88:d7:6e:9a:28:
39:66:17:cd:13:76:fa:e4:20:3c:04:76:86:4e:85:
b7:84:40:1e:54:c2:21:d1:19:1d:0d:09:c5:40:2f:
2f:de:5e:a7:cb:e6:47:5c:48:b2:ac:cb:a6:f2:6a:
d6:3b:5e:f8:ef:30:08:d5:52:31:23:9c:46:49:1d:
27:b4:77:f0:22:f1:3a:91:3f:51:a5:2d:fc:91:57:
81:59:d3:6c:fb:45:12:e1:46:ef:a5:31:e0:b6:72:
73:1d:0a:76:a3:a4:59:9d:ff:df:0d:ca:59:99:26:
73:e7:ac:9b:ae:aa:77:a2:be:ea:14:0a:52:17:61:
43:8a:ef
```

Secret numbers (such that **modulus=number1*number2**):


