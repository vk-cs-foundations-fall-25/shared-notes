---
marp: true
theme: default
paginate: true
header: Church-Turing Thesis &nbsp;&nbsp;|&nbsp;&nbsp; CS301: Foundations of CS &nbsp;&nbsp;|&nbsp;&nbsp; Fall'25 &nbsp;&nbsp;|&nbsp;&nbsp; Vishesh Khemani
style: |
  .cols {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  section.lead h1 {
    text-align: center;
    font-size: 2.5em;
  }
  img {
    display: block;
    margin: 0 auto;
  }
---

<!-- _class: lead -->

# Church-Turing Thesis

## The Universal Nature of Computation

---

# The Central Question

> **What is the most powerful computational model possible?**

**We've seen:**
- DFAs → Limited power (regular languages only)
- PDAs → More powerful (context-free languages)
- TMs → Even more powerful

**Question:** Is there something even MORE powerful than TMs?

---

<!-- _class: lead -->

# The Remarkable Answer

## **NO!**

Turing Machines represent the **pinnacle** of computational power

---

# Church-Turing Thesis

> **A Universal Turing Machine (UTM) can perform any computation that can be done by any physically realizable computing device**

**In other words:**
- TMs are **as powerful as** any possible computer
- No machine can compute **more** than a TM
- TMs represent **maximal computational power**

---

# What This Means

**Implications:**

1. **Theoretical Simplification**
   - Study TMs instead of all possible machines
   - Proven facts about TMs apply to real computers

2. **Computational Limits**
   - If a TM can't do it, **nothing** can
   - Defines absolute boundaries of computation

3. **Universal Applicability**
   - Results apply to past, present, AND future computers

---

# Why It's a "Thesis" Not a "Theorem"

**Important Distinction:**

<div class='cols'><div>

### Mathematical Theorems
- Rigorous formal proof
- Based on axioms
- Absolute certainty

</div><div>

### Church-Turing Thesis
- **Statement about nature**
- **Physical/empirical claim**
- Cannot be "proved" mathematically

</div></div>

**Like laws of physics:** Based on overwhelming evidence, not formal proof

---

# The Evidence is Overwhelming

**Decades of attempts to find something more powerful:**

✓ **All** alternative models shown equivalent to TMs
✓ **No** counterexample ever found
✓ **Every** reasonable computational model studied

**Models proven equivalent to TMs:**
- Lambda calculus (Church)
- Counter machines (Minsky)
- Cellular automata (Conway)
- Your laptop
- Quantum computers (for decidable problems)

---

# The Contrapositive

> **If some computation can't be done on a TM, then it can't be done at all!**

**This is incredibly powerful for proving impossibility:**

- To show problem X is **unsolvable**
- We only need to show **no TM** can solve it
- Then we know **no machine ever** can solve it

---

# TM Variations (All Equivalent)

Many variations of TMs have been studied:

<div class='cols'><div>

### Enhanced TMs
- Multiple tapes
- Multiple tape heads
- 2D tape
- Nondeterministic

</div><div>

### Result
- **All** can be simulated by standard TM
- **All** equivalent in power (ignoring performance)
- Further evidence for thesis

</div></div>

**Key Insight:** These variations don't add computational power

---

# Example: Multiple Tape TM

**Intuition:** More tapes might be more powerful?

**Reality:** Single-tape TM can simulate it!

**How:**
1. Encode multiple tapes on single tape
2. Use special markers to track positions
3. Simulate each step of multi-tape TM

**Result:** Same power, just slower (but speed doesn't matter for computability)

---

# Turing Completeness

> A computational model is **Turing complete** (or **Turing universal**) if it is equivalent to the Turing machine model

**What this means:**
- Can recognize/decide the **same languages** as TMs
- Can compute the **same functions** as TMs
- Has **maximal computational power**

---

# Turing Complete Systems

**Surprisingly diverse list:**

<div class='cols'><div>

**Expected**
- Your computer
- Java, Python, C
- JavaScript

**Theoretical**
- Lambda calculus
- Counter machines
- Cellular automata
- Post systems

</div><div>

**Unexpected**
- Excel spreadsheets
- C++ templates
- PowerPoint
- Magic: The Gathering
- Minecraft redstone

</div></div>

**All of these are as powerful as TMs!**

---

# 🎯 Active Learning Challenge

**Which of these are Turing complete?**

1. Finite State Machines (DFAs)
2. Regular Expressions
3. HTML/CSS (no JavaScript)
4. Conway's Game of Life
5. A simple calculator

**Think, then discuss with neighbor**

---

# Challenge Answers

| System                    | Turing Complete? | Why/Why Not?                         |
| :------------------------ | :--------------- | :----------------------------------- |
| DFAs/Regular Expressions  | ❌ No            | Can't count unboundedly              |
| HTML/CSS                  | ❌ No            | Static, no computation               |
| Conway's Game of Life     | ✅ Yes           | Can simulate TM                      |
| Simple calculator         | ❌ No            | Fixed operations, limited memory     |

---

# Real-World Implications

1. **Programming Languages**
   - All general-purpose languages are equivalent in power
   - Choice is about convenience, not capability

2. **Hardware**
   - Modern computers are Turing complete
   - Adding more hardware doesn't increase **what** can be computed

3. **Algorithms**
   - If problem solvable on one computer, solvable on all
   - Results transfer across systems

---

# The Universal Nature of Computation

**Profound Insight:**

Computation is a **universal** concept:
- Independent of physical implementation
- Same across all systems
- Governed by mathematical principles

**Like physics:**
- Laws of motion apply to all objects
- Laws of computation apply to all machines

---

# Limitations Still Exist

**Important Caveat:**

The thesis says TMs are **maximally powerful**, but:

✓ TMs still have limits
✓ Some problems are **undecidable** (no TM can solve)
✓ Some decidable problems are **intractable** (too slow)

**The thesis doesn't say everything is computable!**

---

# Quantum Computing Note

**Common Question:** Don't quantum computers violate this?

**Answer:** No!

<div class='cols'><div>

### Quantum Computers
- Can be **faster** for some problems
- Can solve some problems **efficiently** that classical computers can't

</div><div>

### But...
- Don't compute **different** decidable problems
- Still bounded by Turing computability
- Turing complete, not "super-Turing"

</div></div>

---

# Why the Thesis Matters

1. **Theoretical Foundation**
   - Defines scope of computer science
   - Enables rigorous study of computation

2. **Practical Guidance**
   - Know when to stop looking for algorithms
   - Understand fundamental limitations

3. **Universal Framework**
   - Results proven once apply everywhere
   - Past, present, future computers

---

# 🎯 Active Learning: Apply the Concept

**Scenario:** Your friend claims they've invented a new programming language that can solve problems no other language can solve.

**Questions:**
1. What does the Church-Turing Thesis tell us about this claim?
2. How would you respond to your friend?
3. What might they actually mean?

---

# Connecting to Earlier Material

**Recall our journey:**

1. DFAs → Recognize regular languages
2. PDAs → Recognize context-free languages
3. TMs → Recognize decidable languages
4. UTMs → Can simulate **any** TM

**Church-Turing Thesis:** UTMs represent the peak of this hierarchy

---

# The Language Hierarchy Revisited

**Complete picture:**

- **Regular** ⊂ **Context-Free** ⊂ **Decidable** ⊂ **Recognizable**
- TMs can decide all **decidable** languages
- TMs can recognize all **recognizable** languages
- **No machine** can do more

**Some languages are unrecognizable** (we'll see why later)

---

# Historical Context

**1930s Parallel Developments:**

<div class='cols'><div>

### Alan Turing (1936)
- Turing Machines
- Mechanical model
- "On Computable Numbers..."

</div><div>

### Alonzo Church (1936)
- Lambda Calculus
- Functional model
- Different approach

</div></div>

**Amazing Result:** Proven equivalent! This convergence strongly supports the thesis.

---

# Testing the Thesis

**How could the thesis be disproven?**

Find a computational model that:
1. Is clearly "computable" in intuitive sense
2. Cannot be simulated by any TM

**After 90 years:** No such model found

**If you find one:**
- You'll achieve **fame and glory**
- Redefine computer science
- Maybe a homework problem? 😀

---

# Key Takeaways

✓ **Church-Turing Thesis:** TMs represent maximal computational power

✓ **Universal:** All reasonable computational models are equivalent to TMs

✓ **Turing Complete:** System equivalent in power to TMs

✓ **Evidence:** Decades of failed attempts to find something more powerful

✓ **Implications:** Results about TMs apply to all computers

✓ **Limitations:** Thesis doesn't say everything is computable

---

# What This Enables

**With the Church-Turing Thesis, we can:**

1. **Prove impossibility results**
   - Show no algorithm exists for certain problems

2. **Study complexity**
   - Classify problems by difficulty

3. **Understand limits**
   - Know boundaries of computation

**Next:** We'll see examples of undecidable problems

---

# Looking Ahead

**Coming Topics:**

1. **Undecidability**
   - Problems no TM can solve
   - The Halting Problem

2. **Complexity Theory**
   - Classes P and NP
   - Practical vs. impractical

3. **Reductions**
   - Relating problems to each other

---

# Summary

**The Big Picture:**

- **Turing Machines** = Universal computational model
- **Church-Turing Thesis** = No more powerful model exists
- **Turing Completeness** = Equivalent to TM
- **Proven facts about TMs** apply to all computers

**This reduces all of computing to the study of TMs!**

---

# Final Thought

> "The Church-Turing Thesis is the foundation that allows computer science to be a science."

**It tells us:**
- What **can** be computed (decidable problems)
- What **cannot** be computed (undecidable problems)
- What is **practical** to compute (tractable problems)

**This is why TMs matter beyond being a historical curiosity!**

---