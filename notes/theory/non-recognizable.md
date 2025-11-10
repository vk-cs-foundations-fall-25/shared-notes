# Unrecognizable Languages

## Overview

- \# Languages = $\infty$
- \# TMs = $\infty$
- Infinite sets can be compared sensibly
  - e.g. # real numbers > # integers
- Turns out, #Languages > #TMs
- So, **some problems are unsolvable!**

## Comparing Infinities

- See, for example, https://www.cantorsparadise.com/number-of-numbers-infinite-weirdness-9387faa58368

- Math facts
  - If two infinite sets have a **1:1 correspondence** (i.e. every element of each set maps to a unique element in the other set), then they have the same size

  - A set is **countable** if it is finite or has the same size as the set of natural numbers {1, 2, 3, ...}
    - Natural numbers, even numbers, rational numbers are all countable infinite sets (and thus have the same size)

    - A countable set's elements can be enumerated systematically, without repetition nor omission

  - An infinite set  is **uncountable** if it does not have a correspondence with the set of natural numbers
    - Real numbers, irrational numbers are all uncountable
    - **Uncountable sets are large than countable sets**


## Languages vs TMs

- How large is the language of **all possible strings**?
  - **Countable**
  - Why?
    - Enumerate strings by length (each length has a finite number of strings)
    - First length 0: $\epsilon$
    - Then length 1: ...
    - And so on
- How large is the language of **all possible TMs** (represented as strings)?
  - **Countable**
  - Why?
    - The set of all possible strings is countable
    - So the subset of those strings that represent TMs is countable
- How large is the language of **infinitely long binary strings**?
  - **Uncountable**
  - Why?
    - Suppose it's countable
    - Then you can enumerate the strings thus:
    
     | n   | f(n)    |
     | --- | ------- |
     | 1   | 0110... |
     | 2   | 1101... |
     | 3   | 0100... |
     | ... |         |
    	
    - You can construct a string that's not in the enumeration 
    
      - x = 101...
      - The ith digit of x is the opposite of the ith digit of the ith string in the above enumeration

- How large is the set of **all formal languages?**
  - **Uncountable**
  - Why?
    - Each formal language corresponds to a unique infinite binary string
    - How?
      - The ith bit is 0 if the ith string in the countable set of all possible strings is in the language (otherwise it's 1)
      - Example over the alphabet {a, b}:

        |                            |            |     |     |     |     |     |     |     |      |     |
        | -------------------------- | ---------- | --- | --- | --- | --- | --- | --- | --- | ---- | --- |
        | All strings                | $\epsilon$ | a   | b   | aa  | ab  | ba  | bb  | aaa | aaab | ... |
        | Language of a(a\|b)*       |            | a   |     | aa  | ab  |     |     | aaa | aaab | ... |
        | Binary string for a(a\|b)* | 0          | 1   | 0   | 1   | 1   | 0   | 0   | 1   | 1    | ... |

    - The set of infinite binary strings is uncountable (see above)
    - So, by correspondence, the set of all languages is uncountable
- \# languages is uncountable, \# TMs is countable, so **# languages > # TMs**

> [!IMPORTANT]
>
> Some languages are not recognizable by any conceivable machine

## Unrecognizable Languages

- What does it mean for a language to be unrecognizable?
- It means that no possible algorithm exists to verify that every string in the language is indeed in the language
- And, since formal languages map to computational problems, the corresponding computational problem can't be solved!
- Ok, some problems are unsolvable, but do we care about such problems or are they irrelevantly abstract?
- We care! There are practical problems that are known to be impossible, as we shall see next

---