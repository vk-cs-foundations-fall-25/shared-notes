# Formal Systems/Languages

> What is a computational problem solved by a computer?
>
> A **formal system/language**

## Definitions

### Alphabet

> An **alphabet** is a finite set of symbols

- Examples:
  - Decimal digits: $\{0, 1, 2, ..., 9\}$
  - Binary digits: $\{0, 1\}$
  - Lowercase english letters: $\{a, b, c, ..., z\}$

### String

> A **string** is a finite sequence of alphabet symbols

Examples:

- Decimal strings: $21456, ...$
- Binary strings: $101110, ...$
- English strings: $good, ogdo, ...$

### Formal Language

> A **formal language** is a set of strings (possibly infinite), all over the same alphabet

Examples over various alphabets:

| Formal Language                                              | In the language                                         | Not in the language          |
| ------------------------------------------------------------ | ------------------------------------------------------- | ---------------------------- |
| Palindromes in English                                       | bob, racecar                                            | Apple, banana                |
| Prime integers                                               | 3, 5, 7, 11                                             | 2, 8, 100                    |
| English words                                                | Apple, banana                                           | Abc, irregardless            |
| Valid English sentences                                      | This is a sentence                                      | Lorem Ipsum                  |
| Valid Java identifiers                                       | x, class                                                | 6, 1a                        |
| Valid Java programs                                          | Class Hi { public static void main(String[] args) { } } | int main(void) { return 0; } |
| Integers z such that $x^n + y^n = z^n$ for some integers $x, y, n > 2$ | no integers                                             | all integers                 |

## Why Formal Languages?

- Can be used to define computational problems in a precise way
  - Examples:
    - Is x a prime number? => is x in the language {3, 5, 7, 11, ...}
    - Is a graph G connected? => is \<G\> in the language {\<G\> | G is a connected graph }
      - Notation: \<G\> denotes a string representation of the graph G
        - e.g. a list of nodes followed by a list of node pairs denoting edges
          - e.g. "[n1,n2,n3], [(n1,n2),(n1,n3)]"
- Precision allows us to prove facts around what's possible and what's not
  - Proving some problem is unsolvable is hard otherwise
    - How do we know if it's unsolvable or simply hard to solve and the solution is out there for us to discover?
- Can be mapped to real-world things
  - e.g. [PQ-system](pq-system.md) <=> integer addition
  - Mathematics in general
