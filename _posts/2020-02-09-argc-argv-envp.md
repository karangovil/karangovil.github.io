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
$ gcc cmd_arg_print.c -o cmd_arg_print
$ cmd_arg_print Hello World
arg[0] = cmd_arg_print
arg[1] = hello
arg[2] = world
{% endhighlight %}

A neat trick that exploits the fact that the program has access to its own name is that it can behave differently when called by different names. For example, `gzip`, `gunzip` and `zcat` commands on some UNIX/Linux distributions are all links to the same executable. This trick comes with a caveat that the user can invoke the executable with a link unknown to the program.

The third variable, `envp`, is often overlooked but can play a useful role in setting up the environment for a child program or for the program to interact with its environment and modify behavior accordingly. Each process has an associated array of strings called the `environment list`, or just the `environment`. When a new process is created, it inherits its parent's environment which provides a one-way (and once only) transfer of information between the parent and child process.

In the Bourne shell and its descendants, one can add values to the environment used to execute a single program without affecting the parent shell using the following syntax:

{% highlight bash %}
$ NAME=value program
{% endhighlight %}

From a C program, one can access the environment either from the arguments to main or by using the global variable `char **environ` (it is set up and defined by the C run-time startup code). Similarly to `argv`, `environ` points to a NULL terminated array of pointers to NULL terminated strings. 
