# venn: set operations with a command line shell script

<img src="README.png" alt="Realm" style="width: 100%;"/>


Syntax:

    venn (union|intersection|...) <input> ...

Set operations:

  * union: A ∪ B (lines that are in any input stream)

  * intersection: A ∩ B (lines that are in every input stream)

  * difference: A ⊕ B (lines that are in exactly one input stream)

  * except: A - B (lines that are solely in the first input steam)

  * extra: B - A (lines that are solely in the last input stream)

  * disjoint: (is each line in only in one input stream?)


### Examples

Examples use these two example data files:

    $ cat A
    red
    green

    $ cat B
    red
    blue

Union:

    $ venn union A B
    red
    green
    blue

Intersection:

    $ venn intersection A B
    red

Difference:

    $ venn difference A B
    green
    blue

Except:

    $ venn except A B
    green

Extra:

    $ venn extra A B
    blue

Disjoint:

    $ venn disjoint A B
    false


## Set operations details


### Union

Set theory operation (A union B).

Print lines that are in any of the inputs.

Also known as "logical or", "logical inclusive disjunction".

Synonyms:

  * `union`

  * `u` (letter u)

  * `∪` (U+222A union)

  * `∨` (U+2228 logical or)

  * `+` (U+002B plus sign)

  * `&` (U+0026 ampersand)

  * `or`


### Intersection

Set theory operation (A intersection B).

Print lines that are in every one of the inputs.

Also known as "logical and", "logical conjunction".

Synonyms:

  * `intersection`

  * `i` (letter i)

  * `∩` (U+2229 intersection)

  * `∧` (U+2227 logical and)

  * `|` (U+007C vertical line)

  * `and`


### Difference

Set theory operation (A symmetric difference B).

Also known as "logical xor", "logical exclusive disjuntion".

Print lines that are in solely one of the inputs. 

Synonyms:

  * `difference`

  * `d` (letter d)

  * `⊕` (U+2295 circled plus)

  * `∆` (U+2206 increment)

  * `Δ` (U+0394 delta)

  * `⊻` (U+22BB logical xor)

  * `xor`


### Except a.k.a. First

Set operation (A except B) a.k.a. (A - B)

Print lines that are solely in the first input.

Synonyms:

  * `except`

  * `first`

  * `sub` 
  
  * `subtract`
  
  * `subtraction`

  * `-` (U+2212 minus sign)


### Extra a.k.a. Last

Set theory operation (A extra B) a.k.a. (B - A).

The lines that are solely in the last input.

Synonyms:

  * `extra`

  * `last`


### Disjoint

Set operation is (A disjoint B).

Print $TRUE and exit 0, or $FALSE and exit 1. 

Synonyms:

  * `disjoint`

  * `n` (letter n)
  
  * `not` 
  
  * `none`


## Customization


### Custom output for true or false

The `disjoint` operation output is either true or false:

    $ venn disjoint A B
    true

You can customize the output text by using environment variables:

    $ TRUE=yes FALSE=no venn disjoint A B
    yes

You can use Unicode symbols:

    $ TRUE=⊤ FALSE=⊥ venn disjoint A B
    ⊤

We like using these Unicode symbols:

  * true is `⊤` (U+22A4 down tack).

  * false is `⊥` (U+22A5 up tack).


## Implemenation

This command is currently implemented using `awk` and POSIX.

The goal is to maximize usability on a wide range of Unix systems, including older systems, and pure POSIX systems.


## Benchmarks


### random unsorted with some duplicates

Benchmark by using two files each containing a million lines of random 6-digit hex strings.

Generate data files:

    $ hexdump -n 30000000 -v -e '/1 "%02X"' -e "/3 \"\n\"" /dev/urandom > a
    $ hexdump -n 30000000 -v -e '/1 "%02X"' -e "/3 \"\n\"" /dev/urandom > b

Time:

    $ time venn union a b > /dev/null

    real  0m19.953s
    user  0m18.766s
    sys   0m1.026s

Compare another approach that uses typical commands:

    $ time cat a b | sort | uniq > /dev/null

    real  4m39.151s
    user  4m44.682s
    sys   0m2.135s

Conclusion: `venn` is approximately 15x faster.


### sequential sorted with no duplicates

Benchmark by using two files each containing a million lines of random 6-digit hex strings.

Generate data files:

    $ awk 'BEGIN { for(i=0;i<1000000;i++) printf "%6.6X\n", i }' > a
    $ awk 'BEGIN { for(i=1000000;i<2000000;i++) printf "%6.6X\n", i }' > b

Time:

    $ time venn union a b > /dev/null

    real  0m1.466s
    user  0m1.294s
    sys	  0m0.159s

Compare another approach that uses typical commands:

    $ time sort -m a b > /dev/null

    real  0m1.529s
    user  0m1.515s
    sys   0m0.009s

Conclusion: `venn` is a approximately a bit faster.


## Comparisons

Comparisons to other implementations, such as Unix, POSIX, shell scripts, etc.


### sort 

To sort an input file:

    sort A

To sort an input file and make lines unique i.e. suppress duplicate lines:

	  sort -u A

Some shells, such as current `bash` and current `ksh`, can send the output of commands as inputs, such as:

    comm -1 -2 <(sort -u A) <(sort -u B)

Note that the `venn` command works on data that is not sorted, and not unique. In other words, when you use `venn`, you don't need to use `sort -u`. See the "Benchmarks" section for a speed comparison of `venn` when inputs are not sorted, and not unique.


### sort --merge

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


### comm

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


### cat and head

Tip: When composing a command line, some people like to start with `cat` to make it the command easier to understand.

Tip: When working with big files, you can limit the input if you start with something like `head -10`.

Example:

    $ cat A | head -10 | sort | uniq

Then switch to cat after you work out the command. 

Help:

    $ man cat
    $ man head


### cut and join

Tip: the `cut` command and `join` command can both be useful for working with lines of data. 

Help:

    $ man cut
    $ man join


### POSIX redirection

It is POSIX shell parsing behaviour that redirections can appear anywhere in the command (obviously, not in the same word as another parameter, nor inside a quoted string). They have to be stripped out by the shell before execution.

Example of equivalent commands:

    $ <inputfile sort >outputfile

    $ cat inputfile | sort > outputfile


## TODO

Ideas to implement:

  * Add a "--help" option?
  
Want to help? We welcome help. You can open a GitHub issue, or send a GitHub pull request, or email us at sixarm@sixarm.com.


## References

See also:

* [Set operations with uniq](http://blog.deadvax.net/2018/05/29/shell-magic-set-operations-with-uniq/)
* [Hacker News discussion](https://news.ycombinator.com/item?id=17183092)

Thanks:

* [Markus Krüger](https://github.com/markusbk)
* [Brian Pitts](https://github.com/sciurus)


## Tracking

* Program: venn
* Version: 4.1.0
* Created: 2017-01-30
* Updated: 2018-05-30
* License: GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
