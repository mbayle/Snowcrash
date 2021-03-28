### Level01

After some research we can see a very interesting line in the file /etc/passwd :

> flag01 : 42hDRfypTqqnw : 3001 : : /home/flag/flag01 : /bin/bash

To decrypt 42hDRfypTqqnw I use JohnTheRipper which gives me the result:

> abcdefg

We just have to connect to the flag01 (password : abcdefg) and launch the getflag command :

`su flag01`

`getflag`

You get the flag ! 
> f2av5il02puano7naaf6adaaf
