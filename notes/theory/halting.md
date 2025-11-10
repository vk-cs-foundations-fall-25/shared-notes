# The Halting Problem

## Overview

- Given a program and an input, write a program to *decide* whether that program will halt when run on that input
  - e.g. no infinite loops
- Quite a useful problem to solve!
- But alas, it is **impossible** to solve
- We present 3 formulations
  - Java
  - TM
  - Diagonalization

- Choose whichever one resonates with you and file it away for life

## Java Formulation

- Universality => we can use Java as a Turing complete computer
- The program we seek to write

   ```java
   // Returns whether f(x) halts.
   public static boolean halts(String javaCodeForF, String x) {...}
   ```

  - Without loss of generality, we're using string representations for the function f and its input x
- Suppose that a correct implementation of the `halts` function exists
- Create a new function `contrarian`:

   ```java
   // If f(f) halts then contrarian(f) does not halt.
   // If f(f) doesn't halt then contrarian(f) halts.
   public static void contrarian(String javaCodeForF) {
      if (halts(f, f)) {
         while (true) {}
      }
   }
   ```

- What happens when we make the call `contrarian(javaCodeForContrarian)`?

   ```java
   public static void main(String[] args) {
      String javaCodeForContrarian = ...;
   
      // If contrarian(javaCodeForContrarian) halts then contrarian(javaCodeForContrarian) doesn't halt.
      // If contrarian(javaCodeForContrarian) doesn't halt then contrarian(javaCodeForContrarian) halts.
      contrarian(javaCodeForContrarian);
   
      // Both statements are contradictions
   }
   ```

- So the assumption that `halts` exists must be wrong.
  - **Proof by contradiction**

> [!IMPORTANT]
>
> The function `boolean halts(String f, String x)` cannot exist.

## TM Formulation

- Let $<M, w>$ be a string encoding of a Turing machine M and the input w to M
- Let H be the language of all $<M, w>$ for which M halts on the input w
  - **H = \{ <M, w> | M is a TM and M halts on input w\}**
- Is H decidable?
- Suppose it is (and this will lead to a contradiction later)
- Then there exists a TM, call it D, that decides the language
  - **D(<M, w>) = accepts if M(w) halts or rejects if M(w) doesn't halt**
- Construct **a Turing machine C, that uses D as a subroutine in a contrarian fashion**:
  - On input \<M\> where M is a TM
    - Run D(<M, \<M>>)
    - If D accepts, then run forever (e.g. keep scanning the infinite tape)
    - If D rejects, then accept
  - C(\<M\>) = accepts if D(<M, \<M>>) rejects or runs forever if D(<M, \<M>>) accepts
- What happens when C is run on the input \<C\>?
  - Case D(<C, \<C>>) rejects i.e C(\<C\>) doesn't halt
    - Then C(\<C\>) accepts and halts
    - Contradiction!
  - Case D(<C, \<C>>) accepts i.e C(\<C\>) halts
    - Then C(\<C\>) runs forever and doesn't halt
    - Contradiction!
- So the assumption that H is decidable is false

> [!IMPORTANT]
>
> The halting problem is undecidable i.e. no TM exists that can decide for all <M, w> whether M(w) halts

### Diagonalization Formulation

- Consider a table in which all TMs are listed down the rows and their string encodings across the columns and the value at a row/column is what the D TM decides when processing $D(<M_i, <M_j>>)$:

| $D(<M_i, <M_j>>)$ | $<M_1>$    | $<M_2>$    | ... |
| ----------------- | ---------- | ---------- | --- |
| $M_1$             | **accept** | reject     | ... |
| $M_2$             | ...        | **reject** | ... |
| ...               | ...        | ...        | ... |

- Since the above table lists all TMs, our contrarian TM C must also be listed:

| $D(<M_i, <M_j>>)$ | $<M_1>$    | $<M_2>$    | ... | $<C>$ | ... |
| ----------------- | ---------- | ---------- | --- | ----- | --- |
| $M_1$             | **accept** | reject     | ... | ...   | ... |
| $M_2$             | ...        | **reject** | ... | ...   | ... |
| ...               | ...        | ...        | ... | ...   | ... |
| $C$               | **reject** | **accept** | ... | **?** | ... |
| ...               | ...        | ...        | ... | ...   | ... |

- The row for $C$ must compute the opposite of the diagnonal entries (based on how C was constructed )
- But then the entry where '?' is requires an opposite of itself, a contradiction! 

---