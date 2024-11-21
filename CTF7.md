## CTF Week #7 (XSS)


##### Find the file related to the flag on the server. Why can't you directly access the secret flag?

When trying to access the flag.txt file, it shows the following error:

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF7_img1.png)

We cannot directly access the flag because the server is configured to block unauthorized or direct requests to the flag.txt file. It enforces restrictions based on context, such as validating headers, cookies, or the origin of the request. This means the file is protected against simple HTTP GET requests and can only be accessed through interactions that occur within the browser, such as JavaScript execution in the context of an authenticated or authorized session.

To bypass this restriction, an XSS (Cross-Site Scripting) attack can be used. This type of attack exploits vulnerabilities in the web application that allow the injection of malicious JavaScript code. When executed in the context of a user's session, this code can interact with the application as if it were part of the trusted session.

In this scenario, an XSS attack enables the execution of JavaScript to request and retrieve the flag from the server. Since the flag is only accessible via JavaScript running in the browser and direct HTTP requests are blocked, XSS provides a way to exploit client-side vulnerabilities to access restricted resources like flag.txt.


##### This service is popular; it might even have known vulnerabilities. Could those help you access the flag?


##### What type of XSS vulnerability (Reflected, Stored, or DOM) allowed you to access the flag?