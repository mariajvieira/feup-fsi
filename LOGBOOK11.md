## Public Key Infrastructures

## Question 1

### Task 1: Becoming a Certificate Authority (CA)

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
00:86:24:08:30:32:9d:13:70:6b:f2:b7:42:c7:92:
9e:d7:d6:1b:58:02:50:d2:e8:27:3d:19:5d:46:e7:
e9:ed:7f:72:62:a4:04:5f:6a:aa:fe:64:e3:c9:5d:
84:97:65:ff:5e:30:d1:dd:78:f8:ae:53:a7:e3:8b:
a0:b1:98:98:fa:42:0a:40:59:d2:30:87:5a:8c:3e:
10:be:6a:bf:67:83:ed:7a:c2:de:2b:db:4a:c2:94:
e2:ee:b6:cb:ca:a6:58:f0:e1:90:98:6e:79:4c:00:
57:be:cb:04:f9:e7:1e:da:58:a1:8f:fa:89:11:73:
c7:22:e7:be:ed:ae:ba:25:80:b9:30:5d:ce:67:b6:
c6:78:11:50:89:af:3f:b1:09:c9:a3:24:b8:fb:e1:
a9:e0:b1:c0:75:31:ba:3e:95:89:89:cf:8d:e0:d0:
96:47:75:12:b7:29:ca:f3:1c:4f:97:76:70:5a:4b:
70:2d:f4:5a:f8:e1:8a:03:f3:37:6e:14:eb:9d:e1:
3d:be:31:9b:fc:0c:ff:4b:c7:f8:a2:75:74:5e:e5:
5f:7f:86:94:d7:c4:6a:5e:00:7c:cd:41:63:79:cf:
e0:72:cf:7a:ef:0c:56:c1:9c:f6:9b:e8:62:1a:70:
0d:d8:d9:1d:d9:d4:6d:fc:5f:23:f6:74:3f:d7:44:
74:9b:70:cc:83:5a:5c:3f:19:6f:2b:c2:2f:df:bd:
84:01:39:4e:45:a0:71:e9:41:1f:9d:24:57:94:9c:
be:22:ad:fc:ee:eb:e4:b0:22:56:36:25:22:bf:fd:
6d:7f:30:bd:ab:8c:2b:30:56:ff:6a:ca:59:7f:af:
d4:0e:62:0a:14:27:1b:f0:99:89:8d:4a:51:79:a7:
48:7b:1f:69:51:a3:1d:f2:45:b8:8f:47:25:e0:21:
0a:4a:35:96:c1:0b:5c:ab:6b:e6:42:0d:03:1a:c4:
0d:b8:b8:c7:6a:73:30:a9:f3:69:b9:49:2c:6d:70:
23:b4:8d:01:f7:53:65:62:94:0b:8b:d9:ce:59:44:
b5:92:07:da:f1:be:30:82:73:3f:17:98:f7:4c:c9:
a9:36:00:f4:95:09:31:08:d5:46:d8:af:a7:1e:ee:
04:05:81:91:14:43:c6:f3:35:3a:f2:21:6a:ca:12:
91:61:42:e1:36:c0:37:81:35:68:e1:a7:08:19:d7:
f4:ed:c1:bf:b0:dc:ab:94:d4:1a:20:58:df:94:fa:
4b:79:d4:5c:83:bb:59:dd:13:92:c8:0a:97:d1:0a:
93:f1:3c:82:8a:10:1a:ac:ba:00:b8:e2:29:ce:f3:
b4:21:d8:6b:b0:6f:35:93:f3:2a:92:c5:39:67:e8:
9c:9a:b1
```

Modulus: 
```
00:af:f1:7b:52:cc:b3:30:62:34:2c:53:07:52:13:
3c:56:24:10:ac:23:17:02:bd:ae:af:bd:14:37:f9:
9c:33:a6:d9:cc:bc:8a:06:14:ef:c8:d4:69:0b:00:
6e:1e:5d:62:71:8e:cf:f1:76:be:1e:5f:ad:52:c8:
64:14:02:39:fd:f2:11:15:6d:41:85:5a:09:0e:66:
6f:09:e2:be:76:34:a2:2e:aa:9d:e6:34:a4:4f:3a:
4d:81:8a:70:6a:a9:51:9c:f7:34:96:61:36:2a:fb:
f3:7e:88:92:06:26:0f:a4:f6:9a:62:4a:17:47:f2:
c3:91:1f:40:9d:4c:a8:1c:e9:41:59:ba:40:ba:46:
82:a4:95:ef:cd:fe:63:55:e8:6c:d9:1a:b6:e9:56:
47:3a:7f:7f:a9:5c:e2:c9:99:04:c2:f1:a4:74:9a:
46:11:a9:96:94:95:69:5f:cb:8c:a3:73:15:2f:2a:
6c:c4:b9:5a:16:61:ca:99:b5:f9:04:aa:06:c1:c1:
0a:6b:13:d6:cb:92:40:6a:9b:0f:2a:ef:6c:b6:3d:
b2:f2:89:30:34:1a:1e:c6:16:a9:00:7e:2a:17:27:
a2:f8:a7:0e:15:00:a7:a1:41:4e:18:bb:23:f3:58:
86:67:62:f8:03:20:73:82:07:90:60:b1:04:93:f2:
7e:6e:dd:21:11:e2:e3:8a:18:5c:9d:9f:ff:aa:8a:
65:16:99:dc:17:30:5b:d2:1d:66:b1:8d:e6:62:cf:
c8:3b:f4:2c:24:7c:c2:cf:9a:ee:8f:2f:30:19:37:
ec:12:96:9a:46:32:62:37:16:46:4a:80:c7:9a:4b:
46:61:6f:aa:cf:69:47:84:f8:63:05:25:30:8b:7a:
66:1d:57:38:dc:66:d5:31:81:ed:6f:88:bf:48:b1:
92:4b:d2:d2:9b:1f:dc:9e:9c:e6:b5:11:cf:e3:cb:
99:b3:ff:ff:9f:5f:d9:74:2a:2a:c9:64:64:3a:52:
16:0c:ed:c1:ff:b7:ac:aa:3c:ee:c2:9c:27:3f:c0:
3c:12:48:05:15:09:2b:8b:94:78:90:26:47:f0:6d:
ce:1e:57:20:e6:9e:9d:9c:f5:a1:71:55:d7:e5:1c:
f4:0d:fb:2b:3d:bc:f0:d9:f2:be:92:f7:11:33:95:
95:d1:68:38:9e:eb:8b:3d:9e:87:3f:47:e6:d4:0f:
a3:b6:61:71:c8:5a:85:a9:91:25:04:43:70:2f:46:
29:ca:14:22:15:bc:c3:47:9f:73:2f:e4:95:9c:8b:
f2:e9:66:94:2b:20:26:2e:c4:51:77:8d:12:23:64:
3f:83:ab:fb:63:06:2c:e4:58:cd:2a:a4:66:05:80:
20:45:df
```

Secret numbers (such that **modulus=number1*number2**):
```
prime1:
    00:e8:69:97:43:8e:b4:4d:e1:5d:b3:21:ae:42:99:
    fb:7c:9a:75:3e:be:ec:18:8f:bf:e7:22:9b:03:0d:
    bc:3d:b6:61:cc:ac:d9:03:83:70:14:a3:6e:c8:03:
    40:d2:7b:7b:d6:1b:35:4b:65:8b:eb:7a:61:49:82:
    7a:89:24:cb:ad:97:b4:9a:6d:72:40:87:11:91:1a:
    4e:01:25:ae:95:9a:c9:de:ff:5b:03:86:3e:61:ba:
    40:a7:ac:e8:49:d7:62:65:74:b2:5c:e3:c1:c6:39:
    05:47:5f:b2:9f:26:9e:3a:f0:e5:1b:96:07:86:80:
    5a:46:8b:e9:6e:3a:fe:12:f6:87:d5:fe:b2:a1:a3:
    7d:ce:33:b2:ec:7a:05:a8:12:a0:51:bd:e8:93:73:
    fc:5d:db:6d:8f:d8:a6:f2:14:23:12:ed:e0:b9:b0:
    f1:8e:60:19:e5:07:e0:d1:12:03:17:a3:7c:7c:8f:
    f9:34:f6:c2:f7:3c:7e:54:c0:40:7a:52:bd:b4:ec:
    78:7b:a7:98:37:47:63:e6:74:2e:8e:14:ad:c2:63:
    79:39:cf:54:e7:d6:da:fc:9e:d2:b3:6b:40:4a:5c:
    ba:0f:db:d5:fe:c2:64:62:ec:c4:b6:74:1b:3d:f0:
    55:85:06:7c:d1:bd:af:1e:fd:58:06:94:68:cc:df:
    b0:b5
prime2:
    00:c1:cc:bd:9c:d2:ab:b0:12:d8:f4:ee:f1:cf:a8:
    c3:b8:af:5a:33:7b:96:50:0c:44:8f:53:85:21:9c:
    4d:d4:71:d2:2d:50:e4:b7:2c:09:e7:f4:a2:cf:ff:
    76:47:aa:9b:de:ec:25:00:07:b9:9a:b8:87:5b:d1:
    21:34:8a:a2:8e:18:f8:45:7a:7e:44:48:65:86:b5:
    98:f7:64:03:0d:f1:8d:50:f5:d2:5e:12:d0:03:1f:
    6a:e8:16:0e:f7:45:f8:b7:86:1a:e9:ef:2d:68:e2:
    2b:62:1b:dd:a7:e5:2c:56:25:fa:71:a9:5e:20:74:
    5c:66:99:fb:a8:85:a2:3c:d0:2c:ba:91:6c:67:e0:
    c6:bd:7b:df:d6:29:8a:e7:9a:de:4c:20:7f:98:15:
    bf:04:94:be:54:0f:1b:a0:ff:8f:41:5e:29:dd:86:
    2b:6d:bb:b5:7d:4a:36:3b:b8:98:60:3a:6e:88:31:
    ea:e8:ec:5e:e1:fc:16:7e:d5:ee:11:f7:ce:6b:9b:
    ec:c2:37:14:55:f6:a5:fd:68:de:37:f1:f6:81:48:
    47:09:7d:00:42:da:e6:5c:d7:ee:94:48:fd:8d:3c:
    27:f0:28:c7:a3:12:57:e8:78:c1:f2:b6:01:07:cf:
    0b:54:84:5c:d6:f0:e5:d9:58:1b:93:70:0e:1f:b1:
    7c:c3
```



### Task 2: Generating a Certificate Request for Your Web Server

We generated the key for ```www.vieira2024.com```:

```
openssl req -newkey rsa:2048 -sha256 \
-keyout server.key -out server.csr \
-subj "/CN=www.vieira2024.com/O=Vieira 2024 LTD./C=PT" \
-passout pass:logbook \
-addext "subjectAltName = DNS:www.vieira2024.com, DNS:www.maria2024.com, DNS:www.mariavieira2024.com"
```

Two files were generated: ```server.csr```and ```server.crt```.

### Task 3: Generating a Certificate for your server


```
openssl ca -config myCA_openssl.cnf -policy policy_anything -md sha256 -days 3650 -in server.csr -out server.crt -batch -cert ca.crt -keyfile ca.key
```
Then, we uncommented the line ```copy_extensions = copy``` in the ```myCA_openssl.cnf``` file.

After this, by running ```openssl x509 -in server.crt -text -noout```we verified that the alternative names were there.

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task3_LOGBOOK11.png)


### Task 4: Deploying Certificate in an Apache-Based HTTPS Website

We started by configuring the Apache server, creating the file vieira2024_apache_ssl.conf inside the shared volumes folder.

Following the example of bank32, our configuration file turned out as follows:
```
<VirtualHost *:443> 
    DocumentRoot /var/www/bank32
    ServerName www.vieira2024.com
    ServerAlias www.maria2024.com
    ServerAlias www.mariavieira2024.com
    DirectoryIndex index.html
    SSLEngine On 
    SSLCertificateFile /volumes/server.crt
    SSLCertificateKeyFile /volumes/server.key
</VirtualHost>

<VirtualHost *:80> 
    DocumentRoot /var/www/bank32
    ServerName www.vieira2024.com
    DirectoryIndex index_red.html
</VirtualHost>

# Set the following gloal entry to suppress an annoying warning message
ServerName localhost
```

We also moved the server.crt and server.key files to the shared volumes folder.

In the container's shell, we copied the previously created configuration file to the /etc/apache2/sites-available folder with the command:
```
$ volumes/vieira2024_apache_ssl.conf /etc/apache2/sites-available
```
Then we enabled the site described in it and started the Apache server:
```
$ a2ensite vieira2024_apache_ssl 
$ service apache2 reload
$ service apache start 
```

We accessed the site at https://www.vieira2024.com, but noticed that the connection was insecure.


To solve this, we imported the ```ca.crt``` file to the certificates of the browser:

![Image 4](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task4_LOGBOOK11_2.png)





## Question 2

**Provide a mechanism to respond to this occurrence and prevent attacks, and describe the measures an adversary might take to avoid being prevented by this mechanism while exploiting a compromised certification authority.**

One effective mechanism to respond to the compromise of a certification authority (CA) is Certificate Revocation. This involves maintaining and consulting Certificate Revocation Lists (CRLs) or using the Online Certificate Status Protocol (OCSP) to validate certificates in real-time.

Measures Adversaries Might Take to Evade the Mechanism:
- Manipulating CRLs or OCSP Responses: Intercepting and forging responses to falsely mark revoked certificates as valid.
- Timing of Exploits: Utilizing malicious certificates issued by the compromised CA before detection and revocation.
- Targeting Systems Without Revocation Checks: Exploiting environments where revocation checks are not enforced.
- Abusing Intermediate CAs: Using intermediate certificates signed by the compromised CA to issue harder-to-detect malicious certificates.
- Proactive monitoring, strict enforcement of revocation checks, and adherence to best practices for certificate validation can mitigate these strategies.




