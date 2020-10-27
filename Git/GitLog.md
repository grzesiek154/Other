One of the more helpful options is -p, which shows the diff introduced in each commit. You
can also use -2, which limits the output to only the last two entries:

```
$ git log -p -2  
```

Sometimes it’s easier to review changes on the word level rather than on the line level. There
is a --word-diff option available in Git, that you can append to the git log -p command to
get word diff instead of normal line by line diff. Word diff format is quite useless when applied to
source code, but it comes in handy when applied to large text files, like books or your dissertation.
Here is an example:

```
$ git log -U1 --word-diff  
```

As you can see, there is no added and removed lines in this output as in a normal diff. Changes
are shown inline instead. You can see the added word enclosed in {+ +} and removed one enclosed
in [- -]. You may also want to reduce the usual three lines context in diff output to only one line,
as the context is now words, not lines. You can do this with -U1 as we did in the example above.
You can also use a series of summarizing options with git log. For example, if you want to
see some abbreviated stats for each commit, you can use the --stat option:

```
$ git log --stat  
```

Another really useful option is --pretty. This option
changes the log output to formats other than the default. A few prebuilt options are available for
you to use. The oneline option prints each commit on a single line, which is useful if you’re looking
at a lot of commits. In addition, the short, full, and fuller options show the output in roughly
the same format but with less or more information, respectively:

```
$ git log --pretty=oneline  
```

The most interesting option is format, which allows you to specify your own log output format. This is especially useful when you’re generating output for machine parsing — because you
specify the format explicitly, you know it won’t change with updates to Git:

```
$ git log --pretty=format:"%h - %an, %ar : %s  
```


