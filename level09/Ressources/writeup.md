### Level09

In this level we have again an executable and a file. To start, I run this one with and without arguments:
```
level09@SnowCrash:~$ ./level09
You need to provied only one arg.
level09@SnowCrash:~$ ./level09 token
tpmhr
level09@SnowCrash:~$ ./level09 aaaaa
abcde
```
As we can see, the program takes an argument read from stdin and prints the result of a transformation. With the last example we can easily deduce that the program takes our argument character by character and adds its index to it:

`
a + 0 = a | a + 1 = b | a + 2 = c | etc ....
`

To obtain the token, we must reverse this hash function. For that I coded the following small program:
```
#include <stdio.h>
#include <unistd.h>

int main(int argc, char **argv)
{
    int i = 0;
    if (argc != 2)
        return (0);
    while (argv[1][i])
    {
	argv[1][i] -= i;
        i++;
    }
    printf("Password is : %s\n", argv[1]);
    return (1);
}
```
Now, I just need to use the following command to get my token:
```
level09@SnowCrash:~$ ./reverse_hash `cat token`
Password is: f3iji1ju5yuevaus41q1afiuq
```

We just have to connect to the flag09 with this password and launch the getflag command 

You get the flag!
> s5cAJpM8ev6XHw998pRWG728z
