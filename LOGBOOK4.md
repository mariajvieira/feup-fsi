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

- We compiled the myprintenv.c program using the command:
```
$ gcc myprintenv.c
$ ./a.out > file
```
- After successful compilation, we executed the program and an executable file named a.out was created along with the output file named "file".

- After run and compile the code again another file was created and we concluded that the output from both files is the same, showing that the environment variables are consistent across both processes. This indicates that both the parent and child processes share the same environment variables at the time of the child's creation.