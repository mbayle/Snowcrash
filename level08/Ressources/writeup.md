### Level08

We start by looking level08 with strings and notice calls to the following functions: `printf strstr read open`. We can deduce the program is doing a comparison during his execution.

If we run ./level08, we got usage 

    ./level08 [file to read]

To see where the comparison is done we can use `ltrace ./level08 test` and see that the program is comparing argv with the string "token":

    strstr("test", "token") = NULL

If I run `ltrace` again with token as argument the result of the comparison is :

    strstr("token", "token") = "token"

For create a new file in my HOME I just have to do a `chmod 777 .`
After creating the test file, I try to run the command again with this file as an argument but it only prints the contents:

    level08@SnowCrash:~$ ltrace ./level08 test2
    __libc_start_main(0x8048554, 2, 0xbffff7a4, 0x80486b0, 0x8048720 <unfinished>
    strstr("test2", "token") = NULL
    open("test2", 0, 014435162522) = 3
    read(3, "this is a test", 1024) = 17
    write(1, "this is a test", 17this is a test) = 17
    +++ exited (status 17) +++

Now that I have the rights to my HOME and I know `level08` is just printing the contents I just need to change the token name to pass the `strstr` condition with `mv token test`

We just have to connect to the flag09 (password : `quif5eloekouj29ke0vouxean`) and launch the getflag command :

`su flag08`

`getflag`

You get the flag ! 
> 25749xKZ8L7DkSCwJkT9dyv6f

