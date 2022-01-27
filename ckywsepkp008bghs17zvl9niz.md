## Install APUE enviroment on macOS12.1

> Since I prepare to study cpp and choose <Advanced Programming in the UNIX Environment 3rd> as my guide book, I am suppose to install the development environment so called apue.3e.

# 1
Download the source code from the official website of APUE
http://www.apuebook.com/code3e.html


# 2
Go into the code directory, run the following commands so that the header file `apue.h` can be included in a C file.
```
cp ./include/apue.h /usr/local/include/
cp ./lib/error.c /usr/local/include/
```

# 3
Then run `make` under the code directory.

- First Error
```
gcc -ansi -I../include -Wall -DMACOS -D_DARWIN_C_SOURCE   -c -o bufargs.o bufargs.c
In file included from bufargs.c:1:0:
../include/apue.h:15:62: fatal error: sys/types.h: No such file or directory
```

  Edit the Makefile `Make.defines.macos`, change the 6th line `CC=gcc` to `CC=clang` , and clang will be used to compile the files.

- Second Error
```
ar: internal ranlib command failed
```
 The fix method is shown in the figure below.
  
  ![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643276284381/bqJW1o4dq.png)

Run `make` again.
