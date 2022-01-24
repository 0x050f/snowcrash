# level00

Watching the video of Snowcrash on the intra we see that we have to find a file that is executable by level00. So the executable could bbe in the $PATH folder like every executable.

We search for groups of the current user:
```
level00@SnowCrash:~$ groups
level00 users
```

And seek on common executable dir for level00 or flag00 rights:
```
level00@SnowCrash:~$ find / -user level00 2>/dev/null | grep -v proc
level00@SnowCrash:~$ find / -user flag00 2>/dev/null | grep -v proc
/usr/sbin/john
/rofs/usr/sbin/john
```

Checking what's inside:
```
level00@SnowCrash:~$ cat /usr/sbin/john
cdiiddwpgswtgt
```

https://www.dcode.fr/cipher-identifier -> ROT/Caesar:
NOTTOOHARDHERE

```
level00@SnowCrash:~$ su flag00
Password: nottoohardhere
Don't forget to launch getflag !
level00@SnowCrash:~$ getflag
Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias
```
