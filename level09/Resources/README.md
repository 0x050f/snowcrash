# level09

```
level09@SnowCrash:~$ ls -l
total 12
-rwsr-sr-x 1 flag09 level09 7640 Mar  5  2016 level09
----r--r-- 1 flag09 level09   26 Mar  5  2016 token
```

```
level09@SnowCrash:~$ cat token
f4kmm6p|=�p�n��DB�Du{��
```

Hmm.. okay seems like we need to decrypt this
Testing the executable:
```
level09@SnowCrash:~$ ./level09
You need to provied only one arg.
level09@SnowCrash:~$ ./level09 token
tpmhr
level09@SnowCrash:~$ ./level09 aaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
abcdefghijklmnopqrstuvwxyz{|}~
level09@SnowCrash:~$ ./level09 $(cat token)
f5mpq;v�E��{�{��TS�W�����
```

Seems like it's just rotating char and it must be how token is encoded. Let's do a little main:
```
#include <stdio.h>

int			main(int argc, char *argv[])
{
	int i = 0;
	int j = 0;
	if (argc != 2)
		return (1);
	while (argv[1][i])
	{
		printf("%c", argv[1][i] + j);
		j--;
		i++;
	}
	return (0);
}
```
Compile it, then:
```
level09@SnowCrash:~$ ./a.out $(cat token)
f3iji1ju5yuevaus41q1afiuq
```

Not bad, let's test it ?
```
level09@SnowCrash:~$ su flag09
Password: 
Don't forget to launch getflag !
flag09@SnowCrash:~$ getflag
Check flag.Here is your token : s5cAJpM8ev6XHw998pRWG728z
```
Coool
