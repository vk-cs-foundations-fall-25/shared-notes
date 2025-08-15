# The PQ System

- Invented by Douglas Hofstadter in his 1979 book "Gödel, Escher, Bach"
- A useful illustration of a formal system and its relevance to math and computation

## Formal Language

- **Alphabet**

  - >  $\{p, q, -\}$

- **Axioms** (strings that are given to be in the language)

  - >  "$xp-qx-$" is an axiom whenever $x$ is composed only of '$-$'

  - Examples:

    - $-p-q--$
    - $--p-q---$
    - $\underbrace{---}_x p \underbrace{-}_1 q \underbrace{----}_z$
    - ...

- **Theorems** (strings in the language that can be produced from axioms and other theorems following **substitution/production rules**)

  - >  If $xpyqz$ is a theorem then $xpy-qz-$ is also a theorem where $x, y, z$ are composed only of '$-$'

  - Examples

    - $-p-q--$ (axiom) 
      - $\implies$ $-p--q---$ (Theorem)
        - $\implies -p---q----$ (Theorem)
          - ...
    - $--p-q---$ (axiom) 
      - $\implies$ $--p--q----$ (Theorem)
        - $\implies --p---q-----$ (Theorem)
          - ...

## Practice

- Is $---p--q-----$ in the language?
  - $---p-q----$ (axiom) $\implies$ $---p--q-----$ (theorem) $\implies$ Yes!
- Is $---p--q----$ in the language?
  - $---p-q----$ (axiom) $\implies$ $---p--q-----$ (theorem) $\implies$ No!
  - How do we know there's no other rule path that derives the string?

## Implementation

  ```java
  public class PQTheorem {
    /** Constructs an axiom with 'x' dashes to the left of p. */
    public PQTheorem(int x) {...}
    
    /** Constructs a theorem derived from the base theorem. */
    public PQTheorem(PQTheorem base) {...}
    
    @Override
    public String toString() {...}
    
    /** Number of dashes to the left of p. */
    public int x() {...}

    /** Number of dashes between p and q. */
    public int y() {...}

    /** Number of dashes to the rigt of q. */
    public int z() {...}
    
    // State
    ...
  }
  ```

```java
/**
 * Derives the target theorem by starting at an axiom and applying the theorem
 * rule repeatedly until either the target theorem with the specified x, y, z is
 * derived or the target is not a theorem.
 * Returns whether the target is a theorem.
 */
public static boolean derive(int x, int y, int z) {
    // Starting axiom.
    PQTheorem t = ...
    System.out.println("Starting axiom: " + t);

    // Repeatedly derive a theorem until the y-dashes match.
    while (t.y() < y) {
        ...
        System.out.println("=> " + t);
    }

    // Check whether the theorem was derived or not.
    return ...
}
```

---

## Interpretation

>  The $pq$ formal language lists all true statements about **positive-integer addition**

- *Isomorphism* between $pq$ and addition
  - Each part of pq has a corresponding part in addition and vice versa

$$
p \iff plus \\
q \iff equals \\
- \iff one \\
-- \iff two \\
etc.
$$

- Meaningful interpretation maps theorems (strings) in a formal system to some reality
  - $--p---q----- \iff 2 + 3 = 5$
- Meaningless interpretation doesn't

$$
p \iff horse \\
q \iff happy \\
- \iff apple \\
-- \iff apple apple \\
etc.
\\
\\
-p-q-- \iff \text{apple horse apple happy apple apple}
$$

---

## Double-Entendre

Consider the following isomorphism:
$$
p \iff equals \\
q \iff taken from \\
- \iff one \\
-- \iff two \\
etc.
$$
Now $--p---q-----$ has a new interpretation:
$$
2 \; \text{equals} \; 3 \; \text{taken from} \; 5 \\
\text{or} \; 5 - 3 = 2
$$
So which is the "true meaning" of the pq system?

- Both!
- Addition and subtraction are isomorphic to one another!
- So of course the pq system is isomorphic to both

## Formal Systems and Reality

- The pq system is an example of a formal system that mimics a portion of reality perfectly
- Did it discover any new truths about addition? No!
- But it did show that addition can be mimicked by a typographical rule governing meaningless symbols
- Can all of reality be turned into a formal system?
  - May be!
  - e.g. symbols are elementary particles (electrons, quarks, etc.) and typographical rules are laws of physics
    - But quantum mechanics and other considerations throw a wrench
- Can all of ***mathematical* reality** be turned into a formal system?
  - Yes, and this includes the theory of computation!
- That's why we'll spend some time on formal systems
