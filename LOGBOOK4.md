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

- We compiled the myprintenv.c program using the command
```
$ gcc myprintenv.c
$ ./a.out > file
```
- After successful compilation, we executed the program and an executable file named a.out was created along with the output file named "file".