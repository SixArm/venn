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

  * The lines that are in only one of the inputs. 

  * `d` `difference` 

  * `⊖` (U+2296 circled minus)

  * `∆` (U+2206 increment)

  * `Δ` (U+0394 delta)

  * `⊻` (U+22BB logical xor)

  * `xor`


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
