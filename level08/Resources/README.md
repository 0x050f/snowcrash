# level08

```
level08@SnowCrash:~$ ls -l
total 16
-rwsr-s---+ 1 flag08 level08 8617 Mar  5  2016 level08
-rw-------  1 flag08 flag08    26 Mar  5  2016 token
```

Again some reverse:
```
gdb-peda$ disas main
Dump of assembler code for function main:
   0x08048554 <+0>:	push   ebp
   0x08048555 <+1>:	mov    ebp,esp
   0x08048557 <+3>:	and    esp,0xfffffff0
   0x0804855a <+6>:	sub    esp,0x430
   0x08048560 <+12>:	mov    eax,DWORD PTR [ebp+0xc]
   0x08048563 <+15>:	mov    DWORD PTR [esp+0x1c],eax
   0x08048567 <+19>:	mov    eax,DWORD PTR [ebp+0x10]
   0x0804856a <+22>:	mov    DWORD PTR [esp+0x18],eax
   0x0804856e <+26>:	mov    eax,gs:0x14
   0x08048574 <+32>:	mov    DWORD PTR [esp+0x42c],eax
   0x0804857b <+39>:	xor    eax,eax
   0x0804857d <+41>:	cmp    DWORD PTR [ebp+0x8],0x1
   0x08048581 <+45>:	jne    0x80485a6 <main+82>
   0x08048583 <+47>:	mov    eax,DWORD PTR [esp+0x1c]
   0x08048587 <+51>:	mov    edx,DWORD PTR [eax]
   0x08048589 <+53>:	mov    eax,0x8048780
   0x0804858e <+58>:	mov    DWORD PTR [esp+0x4],edx
   0x08048592 <+62>:	mov    DWORD PTR [esp],eax
   0x08048595 <+65>:	call   0x8048420 <printf@plt>
   0x0804859a <+70>:	mov    DWORD PTR [esp],0x1
   0x080485a1 <+77>:	call   0x8048460 <exit@plt>
   0x080485a6 <+82>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080485aa <+86>:	add    eax,0x4
   0x080485ad <+89>:	mov    eax,DWORD PTR [eax]
   0x080485af <+91>:	mov    DWORD PTR [esp+0x4],0x8048793
   0x080485b7 <+99>:	mov    DWORD PTR [esp],eax
   0x080485ba <+102>:	call   0x8048400 <strstr@plt>
   0x080485bf <+107>:	test   eax,eax
   0x080485c1 <+109>:	je     0x80485e9 <main+149>
   0x080485c3 <+111>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080485c7 <+115>:	add    eax,0x4
   0x080485ca <+118>:	mov    edx,DWORD PTR [eax]
   0x080485cc <+120>:	mov    eax,0x8048799
   0x080485d1 <+125>:	mov    DWORD PTR [esp+0x4],edx
   0x080485d5 <+129>:	mov    DWORD PTR [esp],eax
   0x080485d8 <+132>:	call   0x8048420 <printf@plt>
   0x080485dd <+137>:	mov    DWORD PTR [esp],0x1
   0x080485e4 <+144>:	call   0x8048460 <exit@plt>
   0x080485e9 <+149>:	mov    eax,DWORD PTR [esp+0x1c]
   0x080485ed <+153>:	add    eax,0x4
   0x080485f0 <+156>:	mov    eax,DWORD PTR [eax]
   0x080485f2 <+158>:	mov    DWORD PTR [esp+0x4],0x0
   0x080485fa <+166>:	mov    DWORD PTR [esp],eax
   0x080485fd <+169>:	call   0x8048470 <open@plt>
   0x08048602 <+174>:	mov    DWORD PTR [esp+0x24],eax
   0x08048606 <+178>:	cmp    DWORD PTR [esp+0x24],0xffffffff
   0x0804860b <+183>:	jne    0x804862e <main+218>
   0x0804860d <+185>:	mov    eax,DWORD PTR [esp+0x1c]
   0x08048611 <+189>:	add    eax,0x4
   0x08048614 <+192>:	mov    eax,DWORD PTR [eax]
   0x08048616 <+194>:	mov    DWORD PTR [esp+0x8],eax
   0x0804861a <+198>:	mov    DWORD PTR [esp+0x4],0x80487b2
   0x08048622 <+206>:	mov    DWORD PTR [esp],0x1
   0x08048629 <+213>:	call   0x8048440 <err@plt>
   0x0804862e <+218>:	mov    DWORD PTR [esp+0x8],0x400
   0x08048636 <+226>:	lea    eax,[esp+0x2c]
   0x0804863a <+230>:	mov    DWORD PTR [esp+0x4],eax
   0x0804863e <+234>:	mov    eax,DWORD PTR [esp+0x24]
   0x08048642 <+238>:	mov    DWORD PTR [esp],eax
   0x08048645 <+241>:	call   0x8048410 <read@plt>
   0x0804864a <+246>:	mov    DWORD PTR [esp+0x28],eax
   0x0804864e <+250>:	cmp    DWORD PTR [esp+0x28],0xffffffff
   0x08048653 <+255>:	jne    0x8048671 <main+285>
   0x08048655 <+257>:	mov    eax,DWORD PTR [esp+0x24]
   0x08048659 <+261>:	mov    DWORD PTR [esp+0x8],eax
   0x0804865d <+265>:	mov    DWORD PTR [esp+0x4],0x80487c4
   0x08048665 <+273>:	mov    DWORD PTR [esp],0x1
   0x0804866c <+280>:	call   0x8048440 <err@plt>
   0x08048671 <+285>:	mov    eax,DWORD PTR [esp+0x28]
   0x08048675 <+289>:	mov    DWORD PTR [esp+0x8],eax
   0x08048679 <+293>:	lea    eax,[esp+0x2c]
   0x0804867d <+297>:	mov    DWORD PTR [esp+0x4],eax
   0x08048681 <+301>:	mov    DWORD PTR [esp],0x1
   0x08048688 <+308>:	call   0x8048490 <write@plt>
   0x0804868d <+313>:	mov    edx,DWORD PTR [esp+0x42c]
   0x08048694 <+320>:	xor    edx,DWORD PTR gs:0x14
   0x0804869b <+327>:	je     0x80486a2 <main+334>
   0x0804869d <+329>:	call   0x8048430 <__stack_chk_fail@plt>
   0x080486a2 <+334>:	leave  
   0x080486a3 <+335>:	ret    
gdb-peda$ x/s 0x8048793
0x8048793:	"token"
```

Seems like we have to bypass the exit and strstr !
```
chmod 777 .
mv token flag.txt
level08@SnowCrash:~$ ./level08 flag.txt
quif5eloekouj29ke0vouxean
level08@SnowCrash:~$ su flag08
Password: quif5eloekouj29ke0vouxean
Don't forget to launch getflag !
flag08@SnowCrash:~$ getflag
Check flag.Here is your token : 25749xKZ8L7DkSCwJkT9dyv6f
```
