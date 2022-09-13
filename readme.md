# Programming

Lets remember  Hello world in C:

```code
#include <stdio.h>
int main()
{
int i;
for(i=0; i < 10; i++)
{
puts("Hello, world!\n");
}
return 0;
}
```

Compile hello world:

```shell
└─$ gcc firstprog.c -o firstprog
                                                                                                                 
└─$ ls -lrt
total 20
-rw-r--r-- 1 darthv darthv   102 Sep 13 19:25 firstprog.c
-rwxr-xr-x 1 darthv darthv 15960 Sep 13 19:27 firstprog
                                                                                                                 
└─$ ./firstprog 
Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

Hello, world!

                                                                                                                 
└─$ 

```


