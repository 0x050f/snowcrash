# level04

As always:
```
level04@SnowCrash:~$ ls -l
total 4
-rwsr-sr-x 1 flag04 level04 152 Mar  5  2016 level04.pl
```

Hmm.. a perl file:
```
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

We sees that we can exploit the second argument like:
```
level04@SnowCrash:~$ perl level04.pl x="$(whoami)"
Content-type: text/html

level04
```

Let's try to did it on the localhost:4747 !
```
level04@SnowCrash:~$ curl localhost:4747?x=$(whoami)
level04
```
Ok, same thing :c
