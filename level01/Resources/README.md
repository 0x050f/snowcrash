# level01

Nothing interesting on home checking for some file access:
```
level01@SnowCrash:~$ groups
level01
```
```
level01@SnowCrash:~$ find / -user level01 2>/dev/null | grep -v proc
level01@SnowCrash:~$ find / -user flag01 2>/dev/null | grep -v proc
```
Nothing !

Check for users in /etc/passwd:
```
level01@SnowCrash:/$ cat /etc/passwd | grep -e level01 -e flag01
level01:x:2001:2001::/home/user/level01:/bin/bash
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```

https://www.dcode.fr/cipher-identifier -> Vigenere:
42iNGtheCrack

And... it don't works :c

Let's check for a hash:
hash-identifier said that it's a possible DES(Unix) hash.
So it might be a hash, let's john it:
```
$> echo "42hDRfypTqqnw" > hash.txt && john hash.txt --show
?:abcdefg

1 password hash cracket, 0 left
```

Bingo, the password is `abcdefg`
let's get the flag:
```
level01@SnowCrash:~$ su flag01
Password: abcdefg
Don't forget to launch getflag !
flag01@SnowCrash:~$ getflag
Check flag.Here is your token : f2av5il02puano7naaf6adaaf
```
