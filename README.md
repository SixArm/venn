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

We like to customize the output text by using environment variables and Unicode symbols `⊤` (U+22A4 down tack) and `⊥` (U+22A5 up tack) like this:

    $ TRUE=⊤ FALSE=⊥ venn disjoint A B
    ⊤


## Implemenation

This command is currently implemented using `awk` and POSIX.

The goal is to maximize usability on a wide range of Unix systems, including older systems, and pure POSIX systems.


## TODO

Ideas to implement:

  * Add a "--help" option?
  
Want to help? We welcome help. You can open a GitHub issue, or send a GitHub pull request, or email us at sixarm@sixarm.com.


## References

Documentation:

* [Benchmarks](doc/benchmarks.md): Benchmarks of millions of lines of data, such as random unsorted data.
* [Comparisons](doc/comparisons.md): Comparisons to other implementations, such as Unix/POSIX shell scripts.

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
