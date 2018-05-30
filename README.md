# venn: set operations with a command line shell script

<img src="README.png" alt="Realm" style="width: 100%;"/>


Syntax:

    venn (union|intersection|...) <input> ...

Set operations:

  * union: A ∪ B (lines that are in any input stream)

  * intersection: A ∩ B (lines that are in every input stream)

  * difference: A ⊖ B (lines that are in exactly one input stream)

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

Set operation is (A union B) a.k.a. logical "or".

Print lines that are in any of the inputs.

Synonyms:

  * `u` `union`

  * `∪` (U+222A union)

  * `∨` (U+2228 logical or)

  * `+` (U+002B plus sign)

  * `&` (U+0026 ampersand)

  * `or`


### Intersection

Set operation is (A intersection B) a.k.a. logical "and".

Print lines that are in every one of the inputs.

Synonyms:

  * `i` `intersection`

  * `∩` (U+2229 intersection)

  * `∧` (U+2227 logical and)

  * `|` (U+007C vertical line)

  * `and`


### Difference

Set operation (A symmetric difference B) a.k.a. logical "xor".

Print lines that are in only one of the inputs. 

Synonyms:

  * `d` `diff` `difference` 

  * `⊖` (U+2296 circled minus)

  * `∆` (U+2206 increment)

  * `Δ` (U+0394 delta)

  * `⊻` (U+22BB logical xor)

  * `xor`


### Except a.k.a. First

Set theory (A except B) a.k.a. (A - B)

Print lines that are only in the first input.

Synonyms:

  * `except`

  * `first`

  * `sub` `subtract` `subtraction`

  * `-` (U+2212 minus sign)


### Extra a.k.a. Last

Set theory (A extra B) a.k.a. (B - A).

The lines that are only in the last input.

Synonyms:

  * `extra`

  * `last`


### Disjoint

Set operation is (A disjoint B).

Print $TRUE and exit 0, or $FALSE and exit 1. 

Synonyms:

  * `disjoint`

  * `n` `not` `none`


## Output true or false

Default output text:

  * TRUE is `⊤` (U+22A4 down tack).

  * FALSE is `⊥` (U+22A5 up tack).

Example of customizing:

    $ TRUE=yes FALSE=no venn disjoint 1 2
    no


## Implemenation

This command is currently implemented using `awk` and POSIX.

The goal is to maximize usability on a wide range of Unix systems, including older systems, and pure POSIX systems.


## Benchmarks

Benchmark by using two files each containing a million lines of random 6-digit hex strings:

    $ hexdump -n 30000000 -v -e '/1 "%02X"' -e "/3 \"\n\"" /dev/urandom > A
    $ hexdump -n 30000000 -v -e '/1 "%02X"' -e "/3 \"\n\"" /dev/urandom > B

Calculate:

    $ time setop union a b > /dev/null

    real  0m19.953s
    user  0m18.766s
    sys 0m1.026s

Compare another approach that uses typical commands:

    $ time cat a b | sort | uniq > /dev/null

    real  4m39.151s
    user  4m44.682s
    sys 0m2.135s


## Tracking

* Program: venn
* Version: 4.0.0
* Created: 2017-01-30
* Updated: 2018-05-30
* License: GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
