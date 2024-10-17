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
- After successful compilation, we executed the program and an executable file named a.out was created along with the output file named "file".
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
- After successful compilation, we executed the program and an executable file named myenv was created along with the output file named "file3".
```
$ myenv > file3
```
- Upon analyzing file3, we noticed that it was empty. The environment variables were not being accessed properly by the program. This was due to the environment pointer not being set correctly—it was pointing to NULL.
- After changing the file from "NULL" to the variable "environ", running and compiling the code again, another file was created:
```
$ gcc myenv.c -o myenv
$ ./myenv
$ myenv > file4
```
- This time, the output in file4 correctly displayed the environment variables, indicating that the program was now properly accessing and printing them.


