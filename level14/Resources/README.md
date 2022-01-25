# level14

```
level14@SnowCrash:~$ ls -l
total 0
```

Nothing ? Hm.. okay

```
level14@SnowCrash:~$ find / -user level14 2>/dev/null | grep -v proc
level14@SnowCrash:~$ find / -user flag14 2>/dev/null | grep -v proc
```

Still nothing...
Soooo let's try to break the /bin/getflag:
```
level14@SnowCrash:~$ chmod 777 .
level14@SnowCrash:~$ cp -f /bin/getflag .
level14@SnowCrash:~$ chmod 777 getflag
level14@SnowCrash:~$ gdb /bin/getflag
GNU gdb (Ubuntu/Linaro 7.4-2012.04-0ubuntu2.1) 7.4-2012.04
Copyright (C) 2012 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "i686-linux-gnu".
For bug reporting instructions, please see:
<http://bugs.launchpad.net/gdb-linaro/>...
Reading symbols from /bin/getflag...(no debugging symbols found)...done.
(gdb) r
Starting program: /bin/getflag 
You should not reverse this
[Inferior 1 (process 3080) exited with code 01]
```

So it doesn't allow us to reverse..? Hmm let's still try :p
When disassembling, we see those lines:
```
   0x08048989 <+67>:	call   0x8048540 <ptrace@plt>
   0x0804898e <+72>:	test   %eax,%eax
   0x08048990 <+74>:	jns    0x80489a8 <main+98>
```
in objdump:
```
 8048989:	e8 b2 fb ff ff       	call   8048540 <ptrace@plt>
 804898e:	85 c0                	test   %eax,%eax
 8048990:	79 16                	jns    80489a8 <main+0x62>
```
So let's edit 79 with eb (instruction for jmp): (did it with vim xxd, search for 7916 and edit to eb16)
```
   0x08048989 <+67>:	call   0x8048540 <ptrace@plt>
   0x0804898e <+72>:	test   %eax,%eax
   0x08048990 <+74>:	jmp    0x80489a8 <main+98>
```
Now we can reverse and trick the thing !
By reversing we see that the program is doing a getuid and show flag, so let's pretend we are flag14:
Add breakpoint after the getuid:
```
   0x08048afd <+439>:	call   0x80484b0 <getuid@plt>
   0x08048b02 <+444>:	mov    %eax,0x18(%esp)
```
```
(gdb) b* 0x08048b02
Breakpoint 1 at 0x8048b02
(gdb) r
Starting program: /home/user/level14/getflag 

Breakpoint 1, 0x08048b02 in main ()
(gdb) i r
eax            0x7de	2014 # -> 2014 is level14 uid (we can see all uid in /etc/passwd)
ecx            0xb7fda000	-1208115200
edx            0x20	32
ebx            0xb7fd0ff4	-1208152076
esp            0xbffff600	0xbffff600
ebp            0xbffff728	0xbffff728
esi            0x0	0
edi            0x0	0
eip            0x8048b02	0x8048b02 <main+444>
eflags         0x200246	[ PF ZF IF ID ]
cs             0x73	115
ss             0x7b	123
ds             0x7b	123
es             0x7b	123
fs             0x0	0
gs             0x33	51
(gdb) set $eax=3014
(gdb) s
Single stepping until exit from function main,
which has no line number information.
Check flag.Here is your token : 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```

:)
