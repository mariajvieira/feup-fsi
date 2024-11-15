## CTF Week #4 (Environment Variables)

After analyzing all installed software in the server, we noticed the following packages:
- bash ("bash/trusty-updates,trusty-security,now 4.3-7ubuntu1.7 amd64 [installed]")
- apache2 ("apache2/trusty-updates,trusty-security,now 2.4.7-1ubuntu4.22 amd64 [installed]")

### CVE-2014-6271
- While searching for the CVEs, we found many vulnerabilities related to the Apache web server and other components of Linux systems. However, CVE-2014-6271, commonly known as Shellshock, stood out due to its widespread impact and significant security implications. This vulnerability affects the Bash shell, which is a critical component of many Linux distributions.

- Shellshock exploits how Bash handles environment variables, allowing attackers to execute arbitrary code by manipulating these variables.
This vulnerability illustrates the critical interaction between environment variables and program execution in Linux systems.


In summary, we can see how a misconfiguration or vulnerability in a widely used shell can lead to severe security breaches, not just in Bash itself but also in any service that relies on it, such as web servers like Apache.

### Searching and Accessing the Flag

#### 1. Searching for the Flag
After some search on the server, we noticed that there was a file named ```flag.txt```:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Image1CTF4.png)

*Image 1 - Results of ```/var/```  command on the server.*

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Image2CTF4.png)

*Image 2 - Results of ```/var/flag```  command on the server.*

The flag.txt file has restricted permissions, meaning we cannot read the file directly.

#### 2. Crafting the Exploit

We created a command to exploit the Shellshock vulnerability:

> env 'VAR=() { :;}; cat /var/flag/flag.txt'

This command uses env to set the variable VAR with a payload that includes a function definition followed by the cat command to read the flag.txt file.

#### 3. Executing the Command

We ran the crafted command, which, due to the vulnerability in Bash, executed the cat /var/flag/flag.txt command and displayed the contents of the file:
>flag{13PaSnJE3HerDbmZOsvXMxqKgXOxX2}

This exercise showed how the Shellshock vulnerability (CVE-2014-6271) in Bash can be used to exploit environment variables and access the restricted files (like flag.txt). By changing these variables, we got around permission restrictions. This highlights the importance of managing environment variables properly to avoid unauthorized access and protect sensitive information.
