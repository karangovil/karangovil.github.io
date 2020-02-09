---
layout: post
title: argc, arv and envp - Know your environment (KYE)
categories: [blog]
---

Every C/C++ and even Python program must have a `main` function which is the entry point for the program. Pretty much everyone who has written a program in any of the languages mentioned above has seen the following signature (or something similar) for the `main` function

{% highlight c %}
int main(int argc, char *argv[], char *envp[]) 
{% endhighlight %}

When a program is executed in the shell, the command line arguments are parsed and passed on to the program through the `argc` and `argv` variables. As the name suggests, `argc` contains the number of arguments passed, including  the name of the program itself. The second variable, `argv`, is a an array of pointers to null terminated strings with `argv[0]` being the name of the program.

Here is a simple example that demonstrates the use of command line arguments in a C program.

{% highlight c %}
/* cmd_arg_print.c */

#include "stdio.h"

int
main(int argc, char *argv[]) {
    int i = 0;

    for(i = 0; i < argc; ++i)
        printf("arg[%d] = %s \n", i, argv[i]);

    return 0;
}
{% endhighlight %}

This can be compiled and run to print all the command line arguments

{% highlight bash %}
>>> gcc cmd_arg_print.c -o cmd_arg_print
>>> cmd_arg_print Hello World
arg[0] = cmd_arg_print
arg[1] = hello
arg[2] = world
{% endhighlight %}

