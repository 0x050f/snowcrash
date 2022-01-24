# level 02

A .pcap file is in the home dir:
```
level02@SnowCrash:~$ ls
level02.pcap
```

We open it in wireshark and sees some login/password things in tcp
Wee see that the password is transmitted 1 byte per 1 byte between No 22 to 40:
```
$> echo "\x6c\x65\x76\x65\x6c\x58\x0d" 
levelX
```

Wee see that the password is transmitted 1 byte per 1 byte between No 45 to 85:
```
$> echo "\x66\x74\x5f\x77\x61\x6e\x64\x72\x7f\x7f\x7f\x4e\x44\x52\x65\x6c\x7f\x4c\x30\x4c\x0d"
ft_wandrNDRelL0L
```
When paying attention you can see that \x7f doesn't print anything, look at ascii table and you see that is the delete char so if we replace every \x7f with a backspace \x08 (to delete the previous char, we obtains this:
```
$> echo "\x66\x74\x5f\x77\x61\x6e\x64\x72\x08\x08\x08\x4e\x44\x52\x65\x6c\x08\x4c\x30\x4c\x0d"
ft_waNDReL0L
```
Bingo !

```
level02@SnowCrash:~$ su flag02
Password: ft_waNDReL0L
Don't forget to launch getflag !
flag02@SnowCrash:~$ getflag
Check flag.Here is your token : kooda2puivaav1idi4f57q8iq
```
