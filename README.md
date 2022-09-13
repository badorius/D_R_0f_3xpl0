# D_R_0f_3xpl0
D_R_0f_3xpl0 personal notes
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
The GNU development tools include a pro-
gram called objdump, which can be used to examine compiled binaries. Let’s
start by looking at the machine code the main() function was translated into.

```shell
└─$ objdump -D firstprog|grep -A20 main.:
0000000000001139 <main>:
    1139:       55                      push   %rbp
    113a:       48 89 e5                mov    %rsp,%rbp
    113d:       48 83 ec 10             sub    $0x10,%rsp
    1141:       c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
    1148:       eb 13                   jmp    115d <main+0x24>
    114a:       48 8d 05 b3 0e 00 00    lea    0xeb3(%rip),%rax        # 2004 <_IO_stdin_used+0x4>
    1151:       48 89 c7                mov    %rax,%rdi
    1154:       e8 d7 fe ff ff          call   1030 <puts@plt>
    1159:       83 45 fc 01             addl   $0x1,-0x4(%rbp)
    115d:       83 7d fc 09             cmpl   $0x9,-0x4(%rbp)
    1161:       7e e7                   jle    114a <main+0x11>
    1163:       b8 00 00 00 00          mov    $0x0,%eax
    1168:       c9                      leave
    1169:       c3                      ret

Disassembly of section .fini:

000000000000116c <_fini>:
    116c:       48 83 ec 08             sub    $0x8,%rsp
    1170:       48 83 c4 08             add    $0x8,%rsp

```


