# level13

```
level13@SnowCrash:~$ ls -l
total 8
-rwsr-sr-x 1 flag13 level13 7303 Aug 30  2015 level13
level13@SnowCrash:~$ ./level13 
UID 2013 started us but we we expect 4242
```

Ok, seems like we have to find a uid injection, so let's make a small dynamic library:

```
level13@SnowCrash:~$ echo -e "int getuid(void){ return 4242; }" > /tmp/main.c
level13@SnowCrash:~$ cd /tmp
level13@SnowCrash:/tmp$ gcc -shared -o ./libgetuid.so /tmp/main.c
level13@SnowCrash:/tmp$ cd $HOME
level13@SnowCrash:~$ export LD_PRELOAD=/tmp/libgetuid.so
level13@SnowCrash:~$ gdb ./level13 
GNU gdb (Ubuntu/Linaro 7.4-2012.04-0ubuntu2.1) 7.4-2012.04
Copyright (C) 2012 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "i686-linux-gnu".
For bug reporting instructions, please see:
<http://bugs.launchpad.net/gdb-linaro/>...
Reading symbols from /home/user/level13/level13...(no debugging symbols found)...done.
(gdb) r
Starting program: /home/user/level13/level13 
your token is 2A31L79asukciNyi8uppkEuSx
[Inferior 1 (process 2515) exited with code 050]
(gdb)
```

Done !
