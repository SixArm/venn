# Benchmarks


## Try random unsorted data with some duplicates

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

Result: `venn` is approximately 15x faster.


## Try sequential sorted data with no duplicates

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

Result: `venn` is a approximately a bit faster.
