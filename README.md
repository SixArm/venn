# setop command for set operation on text line inputs

<img src="README.png" alt="Realm" style="width: 100%;"/>

Syntax:

    setop (union|intersection|...) <input> ...

Examples:

    $ setop union 1.txt 2.txt 3.txt
    => items that are in any file

    $ setop intersection 1.txt 2.txt 3.txt
    => items that are in every file

Set operations summary:

  * union
  * intersection
  * difference
  * disjoint
  * except
  * extra


## Set operations details

Union:

  * Set operation is (A union B) a.k.a. logical "or".

  * Print lines that are in any of the inputs.

  * `u` `union`

  * `∪` (U+222A union)

  * `∨` (U+2228 logical or)

  * `+` (U+002B plus sign)

  * `&` (U+0026 ampersand)

  * `or`

Intersection:

  * Set operation is (A intersection B) a.k.a. logical "and".

  * Print lines that are in every one of the inputs.

  * `i` `intersection`

  * `∩` (U+2229 intersection)

  * `∧` (U+2227 logical and)

  * `|` (U+007C vertical line)

  * `and`

Difference:

  * Set operation (A symmetric difference B) a.k.a. logical "xor".

  * Print lines that are in only one of the inputs. 

  * `d` `diff` `difference` 

  * `⊖` (U+2296 circled minus)

  * `∆` (U+2206 increment)

  * `Δ` (U+0394 delta)

  * `⊻` (U+22BB logical xor)

  * `xor`

Disjoint:

  * Set operation is (A disjoint B) a.k.a. logical "not".

  * Print $TRUE and exit 0, or $FALSE and exit 1. 

  * `disjoint`

  * `n` `not` `none`

Except:

  * Set theory (A except B) a.k.a. (A - B)

  * The lines that are only in the first input.

  * `ex` `except` `exclude`

  * `sub` `subtract` `subtraction`

  * `-` (U+2212 minus sign)

Extra:

  * Set theory (A extra B) a.k.a. (B - A).

  * The lines that are only in the last input.

  * `extra`


## Examples

Example file 1:

    alpha
    bravo

Example file 2:

    alpha
    charlie

Example set operations:

    $ setop union 1 2
    alpha
    bravo
    charlie

    $ setop intersection 1 2
    alpha

    $ setop difference 1 2
    bravo
    charlie

    $ setop disjoint 1 2
    ⊥

    $ setop exclude 1 2
    bravo

    $ setop extra 1 2
    charlie


## Output true or false

Default output text:

  * TRUE is `⊤` (U+22A4 down tack).

  * FALSE is `⊥` (U+22A5 up tack).

Example of customizing:

  $ TRUE=yes FALSE=no setup disjoint 1 2
  no


## Implemenation

This command is currently implemented using `awk` and POSIX.

The goal is to maximize usability on a wide range of Unix systems, including older systems, and pure POSIX systems.


## Tracking

* Program: setop
* Version: 3.1.0
* Created: 2017-01-30
* Updated: 2017-09-15
* License: GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
