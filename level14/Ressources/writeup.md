### Level 14

This time we have nothing in our HOME. After following a false trail with the find command, I decide to look directly at the getflag binary and his main:
```
level14@SnowCrash:~$ which getflag
/bin/getflag
level14@SnowCrash:~$ gdb /bin/getflag
Reading symbols from /bin/getflag...(no debugging symbols found)...done.
(gdb) disas main
Dump of assembler code for function main:
   0x08048946 <+0>: push %ebp
   0x08048947 <+1>: mov %esp,%ebp
   0x08048949 <+3>: push %ebx
   0x0804894a <+4>: and $0xfffffff0,%esp
   0x0804894d <+7>: sub $0x120,%esp
   0x08048953 <+13>: mov %gs:0x14,%eax
   0x08048959 <+19>: mov %eax,0x11c(%esp)
   0x08048960 <+26>: xor %eax,%eax
   0x08048962 <+28>: movl $0x0,0x10(%esp)
   0x0804896a <+36>: movl $0x0,0xc(%esp)
   0x08048972 <+44>: movl $0x1,0x8(%esp)
   0x0804897a <+52>: movl $0x0,0x4(%esp)
   0x08048982 <+60>: movl $0x0,(%esp)
   0x08048989 <+67>: call 0x8048540 <ptrace@plt>
   0x0804898e <+72>: test %eax,%eax
   (...)
```
We can see at main+67 a call to ptrace is made followed by a comparison. Let's look at the register values:
```
(gdb) break *main+72
Breakpoint 1 at 0x804898e
(gdb) r
Starting program: /bin/getflag
Breakpoint 1, 0x0804898e in main ()
(gdb) p $eax
$1 = -1
```

So it's the return value of ptrace that prevents us from continuing the execution. We can simply change it as with level13 :
```
((gdb) s $eax=0
(gdb) p $eax
$2 = 0
(gdb) c
Continuing.
Check flag.Here is your token :
Nope there is no token here for you sorry. Try again :)
[Inferior 1 (process 3001) exited normally]
```
This still doesn't work, there must be a uid check as in the previous level and we want the uid of user flag14. Just look in the `/etc/passwd` file to get it. After several minutes I find the call to `getuid` (main+439) and then the comparison et main+452. Now that we have this information we just need to change the value of `eax` and continue the execution:
```
(gdb) break *main+452
(gdb) p $eax
$3 = 2014
(gdb) s $eax=3014
Single stepping until exit from function main,
which has no line number information.
Check flag.here is your token : 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
Single stepping until exit from function __libc_start_main,
which has no line number information.
Inferior 1 (process 3023) exited normally]
```
Last step:
```
level14@SnowCrash:~$ su flag14
Password:
Congratulation. Type getflag to get the key and send it to me the owner of this livecd :)
flag14@SnowCrash:~$ getflag
Check flag.Here is your token: 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```
