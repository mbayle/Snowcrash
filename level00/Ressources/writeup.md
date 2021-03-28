### Level00

First we have to find out which file we can run with user flag00 and for more readability we close stderr

`find / -user flag00 2>/dev/null`

The result of the find command gives us two files :

> /usr/sbin/john
/rofs/usr/sbin/john

Both files contain the same string :

> cdiiddwpgswtgt

After some research I found the string had been modified with a cesar code, when we decrypt it we get :

> nottoohardhere 

We just have to connect to the flag00 (password : nottohardhere) and launch the getflag command :

`su flag00`

`getflag`

You get the flag ! 
> x24ti5gi3x0ol2eh4esiuxias

