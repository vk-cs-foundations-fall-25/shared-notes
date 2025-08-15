---
marp: true
theme: default
paginate: true
header: Introduction &nbsp;&nbsp; | &nbsp;&nbsp; CS301: Foundations of CS &nbsp;&nbsp; | &nbsp;&nbsp; Fall'25 &nbsp;&nbsp; | &nbsp;&nbsp; Vishesh Khemani
---

<!-- _class: lead -->

# Welcome to CS 301
# Foundations of Computer Science

<!-- _footer: Slides based on my lecture notes (formatted with the help of Claude Opus 4.1) -->
---

# Course Overview

## Two Interconnected Worlds

<style scoped>
.columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
</style>

<div class="columns">
<div>

### 🧮 Computational Theory
What are the fundamental **capabilities** and **limitations** of computers?

</div>
<div>

### ⚙️ Computational Practice
How to solve problems using **industry-standard** approaches?

</div>
</div>

---

# The Balancing Act

![bg right:40% fit](media/1872.jpg)

## Like Philippe Petit on a Tightrope...

We'll balance theory and practice through:

1. **Drawing problems from theory**
   - Example: Build an arithmetic expression interpreter
   
2. **Focusing on practical applications**
   - Example: Implement regular expression matching

---

<!-- _class: lead -->

# 🤔 Quick Check-In

## Think-Pair-Share (3 minutes)

**Question:** What's one theoretical concept you've learned that had a surprising practical application?

1. Think (1 min)
2. Share with a neighbor (1 min)
3. Class discussion (1 min)

---

# World 1: Computational Theory

## Three Fundamental Areas

1. **Automata and Formal Languages** 🤖
   - What IS a computer? What IS a computational problem?

1. **Computability** 🎯
   - What CAN we solve? What's IMPOSSIBLE to solve?

1. **Complexity** ⏱️
   - What's TRACTABLE? What's INTRACTABLE?

---

# Our Theory Approach

## Focus on **Insights**, Not Proofs

### ✅ What we'll emphasize:
- **Conclusions** and their real-world relevance
- **Practical implications** of theoretical limits
- **Intuitive understanding** of concepts

### 📚 Helpful background (but not required!):
- Data structures (stacks, queues, graphs)
- Basic mathematics (sets, functions, logic)

> *Missing something? No worries! We'll cover it together.*

---

# World 2: Computational Practice

## Industry-Standard Approaches

<style scoped>
.columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-top: 20px;
}
.column h3 {
  margin-top: 0;
}
</style>

<div class="columns">
<div class="column">

### 🤝 **Collaboration**
- Version control (Git/GitHub)
- Parallelized development
- Code reviews

### 🚀 **Performance**
- Algorithm selection
- Memory management
- Profiling and optimization

</div>
<div class="column">

### 💻 **Modern Tools**
- Terminal/command line mastery
- Generative AI for development

</div>
</div>

---

# How We'll Practice

## Learning by Doing

<style scoped>
ul li {
  margin: 15px 0;
}
</style>

- **Individual assignments** - Build your skills
- **Group projects** - Learn to collaborate
- **In-class exercises** - Apply concepts immediately
- **"Tales from the Trenches"** - Real industry stories

---

<!-- _class: lead -->

# 🎮 Interactive Activity

## Terminal Challenge! (5 minutes)

Open your terminal and try these commands:
1. `pwd` - Where are you?
2. `ls -la` - What's here?
3. `echo "Hello Computation" > myfile.txt`
4. `cat myfile.txt`

**Bonus:** Can you create a directory and move your file into it?

---

# Sneak Peek: Mind-Blowing Conclusions

## Three Big Ideas We'll Explore

---

# 1. Universality 🌍

## All computers are created equal!

Your laptop ≈ Your phone ≈ Supercomputer ≈ **Turing Machine**

They all have the same fundamental computational power
*(just different speeds and memory)*

---

# 2. Computability 🚫

## Some problems are **impossible** to solve

No computer, no matter how powerful, will EVER solve certain problems

**Example:** The Halting Problem
- Can we write a program that determines if any program will halt or run forever?
- **Answer:** Provably impossible!

---

# 3. Complexity 🤯

## Some solvable problems might be **practically impossible**

There exist problems where:
- We CAN solve them (in theory)
- But it might take longer than the age of the universe
- We don't know if there's a faster way!

**Example:** Traveling Salesman Problem for large number of cities

---

<!-- _class: lead -->

# 📝 Reflection Activity

1. **One thing** that excited you about this course
2. **One concern** you have
3. **One question** you want answered

---

<!-- _class: lead -->

# 🚀 Let's Begin!

