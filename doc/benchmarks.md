# Benchmarks


## Try randomly shuffled data

Benchmark by using two files. Each file contains a million lines of random 6-digit hex strings.

Generate data files:

    $ awk 'BEGIN { for(i=0;i<1000000;i++) printf "%6.6X\n", i }' | shuf > a
    $ awk 'BEGIN { for(i=1000000;i<2000000;i++) printf "%6.6X\n", i }' | shuf > b

Time:

    $ time venn union a b > /dev/null

    real   0m2.066s
    user   0m1.872s
    sys    0m0.178s

    $ time sort -m a b > /dev/null

    real   0m1.525s
    user   0m1.506s
    sys    0m0.011s

    $ time cat a b | sort | uniq > /dev/null

    real  4m39.151s
    user  4m44.682s
    sys   0m2.135s

Result: `venn` is a bit slower than `sort -m`, and both are >100x faster than `cat... sort... uniq`.


## Try sequential sorted data

Benchmark by using two files. Each file contains a million lines of random 6-digit hex strings.

Generate data files:

    $ awk 'BEGIN { for(i=0;i<1000000;i++) printf "%6.6X\n", i }' > a
    $ awk 'BEGIN { for(i=1000000;i<2000000;i++) printf "%6.6X\n", i }' > b

Time:

    $ time venn union a b > /dev/null

    real  0m1.466s
    user  0m1.294s
    sys   0m0.159s

    $ time sort -m a b > /dev/null

    real  0m1.529s
    user  0m1.515s
    sys   0m0.009s

    $ time cat a b | sort | uniq > /dev/null

    real  0m21.907s
    user  0m22.348s
    sys   0m0.186s

Result: `venn` is approximately the same speed as `sort -m`, and both are >10x faster than `cat... sort... uniq`.


## Conclusions

The `venn` command can do more than the `sort -m` command, and is close to the same speed.

Prefer `venn` or `sort -m` over `cat... sort... uniq`.

