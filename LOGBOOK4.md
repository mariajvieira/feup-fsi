## Environment Variable and Set-UID Lab

###  Task 1

- Use of ```printenv``` to print out the environment variables:
 ```
$ printenv PWD
/Users/duartemarques/Desktop/FSI
 ```

- Use of ```export``` and ```unset``` to set or unset environment variables:
 ```
$ export var="try"
$ printenv var
try
$ unset var
$ 
```

###  Task 2

- We compiled the ```myprintenv.c``` program using the command:
```
$ gcc myprintenv.c
$ ./a.out > file
```
- After successful compilation, we executed the program and an executable file named a.out was created along with the output file named ```file```.
```
$ ./a.out > file2
$ diff file file2
```
- After run and compile the code again, another file was created and we concluded that the output from both files is the same, showing that the environment variables are consistent across both processes. This indicates that both the parent and child processes share the same environment variables at the time of the child's creation.

###  Task 3
- We compiled the ```myenv.c``` program using the command:
```
$ gcc myenv.c -o myenv
$ ./myenv
```
- After successful compilation, we executed the program and an executable file named myenv was created along with the output file named ```file3```.
```
$ myenv > file3
```
- Upon analyzing ```file3```, we noticed that it was empty. The environment variables were not being accessed properly by the program. This was due to the environment pointer not being set correctly—it was pointing to NULL.
- After changing the file from ```NULL``` to the variable ```environ```, running and compiling the code again, another file was created:
```
$ gcc myenv.c -o myenv
$ ./myenv
$ myenv > file4
```
- This time, the output in ```file4``` correctly displayed the environment variables, indicating that the program was now properly accessing and printing them.

### Task 4
- We created a new file ```task4.c``` with the following code:
```
#include <stdio.h>
#include <stdlib.h>
int main()
{
system("/usr/bin/env");
return 0 ;
}
```
- Then we compiled and ran that file:
```
$gcc task4.c -o task4
$ ./task4
```
- The ```system()``` function effectively passes all the environment variables from the parent process to the command it executes. Unlike ```execve()```, which directly replaces the process, ```system()``` runs a shell first, allowing it to inherit the environment variables.

### Task 5
- We created a new file ```foo``` with the following code:
```
#include <stdio.h>
#include <stdlib.h>
extern char **environ;
int main()
{
    int i = 0;
    while (environ[i] != NULL) {
        printf("%s\n", environ[i]);
        i++;
    }
}
```

```
$ gcc -o foo foo.c
```
After running this comand, the file was compiled and an executable named foo was created.

```
$ sudo chown root foo
$ sudo chmod 4755 foo
```
- The first command changes the owner of the executable foo to the root user, meaning the program is now owned by the superuser.
- The second changes foo's file permissions and enables Set-UID. The chmod change mode command  sets the permissions to 4755, where 4 activates Set-UID, allowing the program to run with the file owner's (root's) privileges. The 755 grants the owner read, write, and execute rights, while others get read and execute rights. With Set-UID enabled, foo will run with root privileges, even when executed by a regular user.

```
$ export PATH=$PATH:/Documents/Labsetup
$ export LD_LIBRARY_PATH=/Downloads
$ export UNIVERSITY_NAME=Feup
```
![Descrição da Imagem](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task5.jpeg)



### Task 6

- First, we created the new file ```task6.c``` with the following code:
```
int main()
{
  system("ls");
  return 0;
}
```
- Then we compiled and ran that file:
```
$ gcc task6.c -o task6
```
After running this comand, the file was compiled and an executable named ```task6``` was created. Then we changed its owner to root and made it a Set-UID program.
```
$ sudo chown root task6
$ sudo chmod 4755 task6
```
- We saved the malicious script to a file named ```ls.c```:
```
int main()
{
  echo("EXECUTING MALICIOUS SCRIPT as $(whoami)");
  return 0;
}
```
Then, we changed the ```PATH``` environment variable to make :
```
$ export PATH=/home/seed:$PATH
```
We ran the program ls that contains a call to ```system("ls")```. 
However, since the program uses the relative path for the ls command instead of its absolute path, we can create an executable with the same name as the command ls but that executes a completely different instruction.
In this case, we created malicious code whose execution would print a message.





