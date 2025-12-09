---
marp: true
theme: default
paginate: true
header: Course Summary &nbsp;&nbsp;|&nbsp;&nbsp; CS301: Foundations of CS &nbsp;&nbsp;|&nbsp;&nbsp; Fall'25 &nbsp;&nbsp;|&nbsp;&nbsp; Vishesh Khemani
---

<!-- _class: lead -->

# CS 301: Foundations of Computer Science
## Major Conclusions & Key Takeaways

**Fall 2025**

---

# Course Overview

**Two Complementary Areas:**

<div class="columns">
<div>

### Computational Theory
*What are the fundamental capabilities and limitations of computers?*

</div>
<div>

### Computational Practice
*How to solve problems using industry-standard approaches?*

</div>
</div>

**Goal:** Bridge abstract theory with practical programming

---

# The Three Big Theoretical Questions

1. **What is a computer?**
   - Automata and Formal Languages

2. **What problems are solvable?**
   - Computability Theory

3. **What problems are practical?**
   - Complexity Theory

---

<!-- _class: lead -->

# Major Conclusion #1: Universality

---

# Universality: All Computers Are Equivalent

**The Church-Turing Thesis:**

> All computational models that capture the intuitive notion of "algorithm" are equivalent in power to Turing Machines

**What this means:**
- Your laptop, smartphone, and supercomputers are all equivalent to a simple Turing Machine
- Different in *speed*, identical in *capability*
- If a TM can't solve it, no computer can

---

# Abstract Machines (Computational Models)

![width:400px](media/abstract-machine-2.excalidraw.svg)

---

# Practical Impact of Universality

**Implications:**

1. **Portability:** Algorithms work on any computer
2. **Theoretical Analysis:** We can study TMs to understand all computing
3. **Universal Truth:** Results proven for TMs apply everywhere

**One Model Rules Them All:** Understanding TMs means understanding all computation

---

<!-- _class: lead -->

# Major Conclusion #2: Undecidability

---

# Undecidability: Some Problems Are Unsolvable

**The Halting Problem:**

> No algorithm can determine whether an arbitrary program will halt or run forever

**Proof Technique:** Self-reference creates logical contradictions

**Reality Check:** Some problems have *no algorithmic solution*, ever.

---

# Rice's Theorem: Undecidability Is Widespread

**Rice's Theorem (1953):**

> Any non-trivial property about the *behavior* of programs is undecidable

**What this means:**
- Can't determine if a program computes a specific function
- Can't detect if a program outputs only even numbers
- Can't verify if a program ever uses a variable

**Impact:** The halting problem is not an isolated case—undecidability is pervasive in program analysis

---

# What Undecidability Means for You

**You cannot build:**

- A perfect debugger (detecting all infinite loops)
- A complete virus scanner (detecting all malware)
- A universal code optimizer (finding all optimizations)
- A perfect program verifier (checking all properties)

**The Boundary:** Fundamental limits on software tools

---

<!-- _class: lead -->

# Major Conclusion #3: Intractability

---

# Complexity: Tractable vs. Intractable

**Two Key Classes:**

- **P:** Problems solvable in polynomial time (practical)
- **NP:** Problems where solutions are verifiable in polynomial time

**The Million Dollar Question:** Is P = NP?

**Most Believe:** P ≠ NP (some problems are inherently hard)

---

# NP-Complete: The Hardest Practical Problems

**Thousands of important problems are NP-complete:**

- Traveling Salesman Problem
- Graph Coloring
- Knapsack Problem
- Circuit Design Optimization
- Protein Folding
- Scheduling Problems

**If any one has a polynomial solution, they ALL do**

---

# What Complexity Theory Means for You

**When you encounter NP-complete problems:**

1. **Don't** search for perfect polynomial algorithms (no one has found one)
2. **Do** use approximation algorithms
3. **Do** use heuristics that work well in practice
4. **Do** restrict to special cases with polynomial solutions
5. **Accept** exponential time for small inputs

**Reality:** Some problems require creative compromises

---

<!-- _class: lead -->

# The Formal Language Hierarchy

---

# Computational Power Spectrum

![width:700px](media/venn-formal-2.excalidraw.svg)

**From weakest to strongest:** Regular → Context-Free → Decidable → Recognizable

---

<!-- _class: lead -->

# Practical Takeaways

---

# Industry-Standard Practices Covered

**Collaboration & Development:**
1. Version control with Git and GitHub
2. Terminal/command-line proficiency
3. Build systems (Ant, Maven)
4. Unit testing

**Optimization:**
5. Memory management techniques
6. Algorithm and data structure choices
7. Performance analysis with Big-O

**Modern Tools:**
8. Using generative AI effectively for programming

---

<!-- _class: lead -->

# Course Completed

**You now understand:**
- What computers fundamentally are
- What they can and cannot do
- What's practical vs. theoretical
- How to build software professionally

**Welcome to understanding the foundations of computer science!**

