# The `setop` command for set operation on text lines

Print the items that are in any of the inputs.

Syntax:

    setop (union|intersection|difference|...) <input> ...

Examples:

    $ setop union 1.txt 2.txt 3.txt
    => items that are in any file

    $ setop intersection 1.txt 2.txt 3.txt
    => items that are in every file

    $ setop difference 1.txt 2.txt 3.txt
    => items that are in one file

Set operations shortlist:

  * `u` `union` `∪` (U+222A union) `+` (U+002B plus sign) `∨` (U+2228 logical or)
  * `i` `intersection` `∩` (U+2229 intersection) `∧` (U+2227 logical and)
  * `d` `difference` `Δ` (U+0394 delta) `∆` (U+2206 increment) `⊻` (U+22BB logical xor)


## Set operations details

Union:

  * `u` `union` `∪` (U+222A union) `+` (U+002B plus sign) `∨` (U+2228 logical or)

  * The lines that are in any of the inputs.

  * This command is (A union B) a.k.a. logical "or".

Intersection:

  * `i` `intersection` `∩` (U+2229 intersection) `∧` (U+2227 logical and)

  * The lines that are in every one of the inputs.

  * Set operation is (A intersection B) a.k.a. logical "and".

Difference:

  * `d` `difference` `Δ` (U+0394 delta) `∆` (U+2206 increment) `⊻` (U+22BB logical xor)

  * The lines that are in only one of the inputs. 

  * Set operation (A difference B) a.k.a. symmetric difference a.k.a. disjoint union a.k.a. logical "xor".


## TODO: Set operations details

Disjoint:

  * Are the inputs disjoint? If yes, print "⊤" (true) and exit 0. If no, print "⊥" (false) and use exit 1.

  * Set operation is (A disjoint B) a.k.a. logical "not".

  * Aliases: difference, d, symmetricdifference, disjointunion.

Equal:

  * TODO

  * Unicode 'EQUALS SIGN' (U+003D)

Not Equal:

  * TODO

  * Unicode 'NOT EQUAL TO' (U+2260)

Except:

  * The lines that are only in the first input.

  * Set theory (A except B) a.k.a. (A - B).

Extra:

  * The lines that are only in the last input.

  * Set theory (A extra B) a.k.a. (B - A).



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

    $ setop intersect 1 2
    alpha

    $ setop difference 1 2
    bravo
    charlie

    $ setop disjoint 1 2
    ⊥ (the symbol false) and exit 1

    $ setop except 1.txt 2.txt
    bravo

    $ setop extra 1.txt 2.txt
    charlie


## Implemenation

This command is currently implemented using `awk` and POSIX.

The goal is to maximize usability on a wide range of Unix systems, including older systems, and pure POSIX systems.


## Tracking

* Program: setop
* Version: 3.0.0
* Created: 2017-01-30
* Updated: 2017-09-14
* License: GPL
* Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
