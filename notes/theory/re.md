# Regular Expressions

- An arithmetic expression such as $2 * (8 + 9)$ has numbers as operands and '*', '+' etc. as operators
- Similarly a **regular expression (RE)** has alphabet symbols as operands and regular language operators as operators
- The symbols for the operators in a regular expression are sometimes different from the set operator symbol

|                   | Set             | RE              |
| ----------------- | --------------- | --------------- |
| **Union**         | $\cup$          | \|              |
| **Concatenation** | Implicit (or .) | Implicit (or .) |
| **Closure**       | *               | *               |

- The operators have the following precedence in an RE
  - Closure before concatenation before union
- Parenthesis can be used to override the precedence

- Here are some examples of regular expressions (and their associated language) over the binary alphabet {0, 1}:

| Regular Language                                  | RE             |
| ------------------------------------------------- | -------------- |
| {0}                                               | 0              |
| {1}                                               | 1              |
| {0} U {1} = {0, 1}                                | 0\|1           |
| {0, 1} . {0, 1} = {00, 01, 10, 11}                | (0\|1).(0\|1)  |
| {0, 1}* = {$\epsilon$, 0, 1, 00, 01, 10, 11, ...} | (0\|1)*        |
| Binary strings with no leading 0s                 | 0\|(1.(0\|1)*) |

- REs are a **compact and precise way to specify a regular language**

## Regular Languages

Complete definition: 

> A formal language is called a **regular language** if some DFA or NFA recognizes it or it is specified by an RE.

A class of formal languages with the following properties:

- A simple **specification**
  - using an RE
- Automated **recognition** of strings in the language
  - using an NFA/DFA
- Several practical applications
  - input validation
  - Searching for patterns (e.g. grep)
  - syntax specification
  - ...

### Kleene's Theorem

> (1951) REs, DFAs, and NFAs are equivalent models to characterize the regular languages

## Aside: Generalized REs

- We've defined a minimal RE
- In practice it's useful to make additions to REs
  - Escape mechanisms to allow operator symbols to be present in the alphabet
  - Shorthand notations
    - Wildcard symbol for any alphabet symbol
    - Escaped symbol for subsets of alphabet symbols
    - Symbols for the beginning of a line and the end of a line
    - A list or range of symbols
    - A negated list or range of symbols
  - Enhanced closure
    - One or more
    - Zero or one
    - Exactly n
    - Between m and n
- Be aware of the generalized RE when using RE in the wild
- But for this class we'll stick with the minimal RE

## Grep

`grep` is a command-line utility in Unix and Unix-like operating systems used for searching plain-text data for lines that match a regular expression. 

See the notes on [shell commands](../practice/shell.md#grep-and-regular-expressions) for more details on `grep` and regular expressions.
