## CTF Semana #4 (Environment Variables)

After analyzing all installed software in the server, we noticed the following packages:
- bash ("bash/trusty-updates,trusty-security,now 4.3-7ubuntu1.7 amd64 [installed]")
- apache2 ("apache2/trusty-updates,trusty-security,now 2.4.7-1ubuntu4.22 amd64 [installed]")

### CVE-2014-6271
- While searching for the CVEs, we found many vulnerabilities related to the Apache web server and other components of Linux systems. However, CVE-2014-6271, commonly known as Shellshock, stood out due to its widespread impact and significant security implications. This vulnerability affects the Bash shell, which is a critical component of many Linux distributions.

- Shellshock exploits how Bash handles environment variables, allowing attackers to execute arbitrary code by manipulating these variables.
This vulnerability illustrates the critical interaction between environment variables and program execution in Linux systems.


In summary, we can see how a misconfiguration or vulnerability in a widely used shell can lead to severe security breaches, not just in Bash itself but also in any service that relies on it, such as web servers like Apache.


After some search on the server, we noticed that there was a file named ```flag.txt```:

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Image1CTF4.png)

*Image 1 - Results of ```/var/```  command on the server.*

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Image2CTF4.png)

*Image 1 - Results of ```/var/flag```  command on the server.*




