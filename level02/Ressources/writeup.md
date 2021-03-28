### Level02
Once on the home of level02, we can see a pcap file :

> ----r--r-- 1 flag02 level02 8302 Aug 30 2015 level02.pcap

First of all to be able to analyse it with Wireshark we must first retrieve it on our computer. Just type the following command (remember to make a chmod once on the computer):

`scp -P 4242 level02@<replace with your IP>:~/level02.pcap ~/Desktop`

Package 43 contains the word password, so let's see the details. To do this we can right click and then "Follow -> TCP Stream". So we can read the client input: `ft_wandr...NDRel.L0L`.

If we try to type it we can see it's incorrect. We changing the view of the software (Hex Dump) we can see more information:

> 000000B9 66 f
000000BA 74 t
000000BB 5f _
000000BC 77 w
000000BD 61 a
000000BE 6th n
000000BF 64 d
000000C0 72 r
000000C1 7f .
000000C2 7f .
000000C3 7f .
000000C4 4th N
000000C5 44 D
000000C6 52 R
000000C7 65 e
000000C8 6c l
000000C9 7f .
000000CA 4c L
000000CB 30 0
000000CC 4c L
000000CD 0d .

The character `7f` corresponds to `DEL` so we can deduce that the real password is: ` ft_waNDReL0L`.

We just have to connect to the flag01 (password : ft_waNDReL0L) and launch the getflag command :

`su flag02`

`getflag`

You get the flag ! 
> kooda2puivaav1idi4f57q8iq

