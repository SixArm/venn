# Comparisons

Comparisons to other implementations, such as Unix, POSIX, shell scripts, etc.


## sort 

To sort an input file:

    sort A

To sort an input file and make lines unique i.e. suppress duplicate lines:

	  sort -u A

Some shells, such as current `bash` and current `ksh`, can send the output of commands as inputs, such as:

    comm -1 -2 <(sort -u A) <(sort -u B)

Note that the `venn` command works on data that is not sorted, and not unique. In other words, when you use `venn`, you don't need to use `sort -u`. See the "Benchmarks" section for a speed comparison of `venn` when inputs are not sorted, and not unique.


## sort --merge

You can use the `sort --merge` command to merge inputs. 

These examples work when the inputs are presorted.

Union:

    $ sort -m A B | uniq

Intersection:

    $ sort -m A B | uniq -d

Relative complement:

    $ sort -m A A B | uniq -u

Help:

    $ man sort
    $ man uniq


## comm

You can use the `comm` command to print lines in common.

These examples work when the inputs are presorted.

Show only items in both A and B:

    $ comm -1 -2 A B

Show only items unique to A:

    $ comm -2 -3 A B

Show only items unique to B:

    $ comm -1 -3 A B

Help:

    $ man comm


## cat and head

Tip: When composing a command line, some people like to start with `cat` to make it the command easier to understand.

Tip: When working with big files, you can limit the input if you start with something like `head -10`.

Example:

    $ cat A | head -10 | sort | uniq

Then switch to cat after you work out the command. 

Help:

    $ man cat
    $ man head


## cut and join

Tip: the `cut` command and `join` command can both be useful for working with lines of data. 

Help:

    $ man cut
    $ man join


## POSIX redirection

It is POSIX shell parsing behaviour that redirections can appear anywhere in the command (obviously, not in the same word as another parameter, nor inside a quoted string). They have to be stripped out by the shell before execution.

Example of equivalent commands:

    $ <inputfile sort >outputfile

    $ cat inputfile | sort > outputfile
