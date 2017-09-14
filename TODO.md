# TODO

Create more operations.


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

## Code

```
  disjoint|n|not|none)
    awk 'seen[$0]==1 {x=1;exit} {seen[$0]=1} END { print x ? ${FALSE:-⊥} : ${TRUE:-⊤}; exit !!x}' "$@"
    ;;
  eq|equal|"=","==")
    #TODO 
    # awk 'NR==FNR{seen[$0]=1;next} seen[$0]=0; END { for (key in seen) { if (seen[key]) { print key } } }' "$@"
    ;;
  ne|not-equal|"!=")
    #TODO awk 'NR==FNR{seen[$0]=1;next} seen[$0]=0; END { for (key in seen) { if (seen[key]) { print key } } }' "$@"
    ;;
  e|except|exclude|minus|omit|subtract|subtraction|"-")
    #TODO
    # awk 'NR==FNR{seen[$0]=1;next} seen[$0]=0; END { for (key in seen) { if (seen[key]) { print key } } }' "$@"
    ;;
  extra)
    #TODO
    # awk 'BEGIN{argindmax=ARGC-1} FNR==1{argind+=1} argind<argindmax {seen[$0]; next}!($0 in seen)' "$@"
    ;;
```
