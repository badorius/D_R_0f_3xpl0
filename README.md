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
The GNU development tools include a pro-gram called **objdump**, which can be used to examine compiled binaries. Let’sstart by looking at the machine code the main() function was translated into.

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

Each byte is represented in hexadecimal notation, which is a base-16 numbering system. hexadecimal notation is a conventional notation since a byte contains 8 bits, each of which can be either true or false. This means a byte has 256 (28) possible values, so each byte can be described with 2 hexadecimal digits.

The hexadecimal numbers—starting with 0x8048374 on the far left—are memory addresses. The bits of the machine language instructions must be put somewhere, and this somewhere is called memory. Memory is just a collection of bytes of temporary storage space that are numbered with addresses. 

Each byte of memory can be accessed by its address, 
Older Intel x86 processors use a 32-bit addressing scheme, while newer ones use a 64-bit one. The 32-bit processors have 2^32 (or 4,294,967,296) possible addresses, while the 64-bit ones have 2^64 (1.84467441 × 10^19) possible addresses.

Personally, I think Intel syntax is much more readable and easier to understand
```shell
objdump -M intel -D firstprog| grep -A20 main.:
0000000000001139 <main>:
    1139:	55                   	push   rbp
    113a:	48 89 e5             	mov    rbp,rsp
    113d:	48 83 ec 10          	sub    rsp,0x10
    1141:	c7 45 fc 00 00 00 00 	mov    DWORD PTR [rbp-0x4],0x0
    1148:	eb 13                	jmp    115d <main+0x24>
    114a:	48 8d 05 b3 0e 00 00 	lea    rax,[rip+0xeb3]        # 2004 <_IO_stdin_used+0x4>
    1151:	48 89 c7             	mov    rdi,rax
    1154:	e8 d7 fe ff ff       	call   1030 <puts@plt>
    1159:	83 45 fc 01          	add    DWORD PTR [rbp-0x4],0x1
    115d:	83 7d fc 09          	cmp    DWORD PTR [rbp-0x4],0x9
    1161:	7e e7                	jle    114a <main+0x11>
    1163:	b8 00 00 00 00       	mov    eax,0x0
    1168:	c9                   	leave
    1169:	c3                   	ret

Disassembly of section .fini:

000000000000116c <_fini>:
    116c:	48 83 ec 08          	sub    rsp,0x8
    1170:	48 83 c4 08          	add    rsp,0x8

```

Processors also have their own set of special variables called registers. Most of the instructions use these registers to read or write data, so understanding the registers of a processor is essential to understanding the instructions.


A breakpoint is set on the main() function so execution will stop right before our code is executed. Then GDB runs the program, stops at the breakpoint, and is told to display all the processor registers and their current states.

```shell
gdb -q ./firstprog
Reading symbols from ./firstprog...
(No debugging symbols found in ./firstprog)
(gdb) break main
Breakpoint 1 at 0x113d
(gdb) run
Starting program: /home/darthv/git/badorius/D_R_0f_3xpl0/code/GettingYourHandsDirty/firstprog 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/usr/lib/libthread_db.so.1".

Breakpoint 1, 0x000055555555513d in main ()
(gdb) 

```
The first four registers (EAX, ECX, EDX, and EBX) are known as general-purpose registers. These are called the Accumulator, Counter, Data, and Baseregisters, respectively.
The second four registers (ESP, EBP, ESI, and EDI) are also general-purpose registers, but they are sometimes known as pointers and indexes.These stand for Stack Pointer, Base Pointer, Source Index, and Destination Index,respectively. The first two registers are called pointers because they store 32-bit
addresses, which essentially point to that location in memory.

The last two registers are also technically pointers,