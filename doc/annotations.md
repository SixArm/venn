

# Annotations


## Variables

Awk variables that are especially useful:

  * FS: Field Separator (for input)
  * OFS: Output Field Separator
  * RS: Record Separator (for input)
  * ORS: Output Record Separator
  * NR: Number of Records
  * NF: Number of Fields in a record
  * FNR: File Number of Records
  * FILENAME: File name of the current input file
  * ARGIND: The index in ARGV of the current file being processed. 


## NR==FNR

The awk variable `NR` refers to the total record number read so far.

  * Example: suppose awk uses typical line separators to process two typical text files each with 10 lines. NR increments from 1 to 20 because there are 20 lines total.

The awk variable `FNR` refers to the current file's record number read so far.

  * Example: suppose awk uses typical line separators to process two typical text files each with 10 lines. FNR increments from 1 to 10 during the first file, and from 11 to 20 during the second file.

NR keeps increasing. 

FNR resets back to 1 for the first line of each file.

The condition NR==FNR is true during the first file, and false otherwise.

This means that NR==FNR is useful to test if you're processing the first file.


## Union

Code:

    awk '!seen[$0] {print} {seen[$0]=1}' "$@"

Meaning:

  * If this is the first time we're seeing the current record, then print it, else remember it.

  * `$0` is the current record, which by default is the current line.

  * `seen[$0]` means "have we seen the current record?". 

    * `seen[...]` is an associative array lookup i.e. we are asking if the `seen` hash has a key. 

    * `seen[...]` defaults to undefined, which is evaluated as false, unless we do something later on to change it.

  * `seen[$0]=1` means "we are seeing the current line". 

    * We could have set this to anything, because all we care about is defining a value; we typically use 1 to mean true.

    * We could have named this array anything; we typically use the name `seen` to emphasize that we're seeing items.

  * `!seen[$0] {...} {...}` means "if we have not seen the current record, then do the first thing, else do the second thing".

  * `print` without any arguments means print the current record.
 
  * `$@` means "the rest of the shell arguments from the invocation of this script".

    * For example if the script is invoked as `venn union a b c` then `$@` is an array of `a`, `b`, `c`.

    * `"$@"` means quote the arguments; this is a shell security habit that protects them from accidential expansion.


