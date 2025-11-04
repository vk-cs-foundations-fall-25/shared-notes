# Algorithm

> What exactly is an algorithm?

- *Intuitive* notion: a method to solve a problem
  - Independent of programming environment
- In *computer science*: an effective problem-solving method suitable for implementing as a computer program
  - Examples: sorting, searching, expression evaluation, ...
- In *theory*: **a specific TM**
    - What the ...?

## Decidability

- A TM when run on an input can have three possible outcomes:
  1. Stop at an **accept** state
  2. Stop at a **reject** state
  3. **Not stop** (run forever)

> A TM **recognizes** the language that consists of all input strings that lead to an accept state

- Examples:

  - The incrementer TM recognized the language of all binary strings
  - The adder TM recognized the language of valid addition expressions on any two binary strings

- What about input strings that are not in the language?
- Two possibilities
  1. Reject
  2. Run forever

> A TM **decides** the language it recognizes if it rejects all input strings that are not in the language

Examples:

- The incrementer TM decided the language of all binary strings
- The adder TM with the reject state decided the language of valid addition expressions on any two binary strings
  - However, if you remove the reject state then it doesn't decide the language but only recognizes the language
  - Why?
    - Suppose there are two '+' symbols in an invalid input
    - Then it would scan left forever in state q2
- With a DFA no need to distinguish between deciding and recognizing since DFAs always stop when the input is done

### Computability

- Take the output tape into consideration

> A function f(x) is **computable** if there exists some TM such that when the tape is initialized to **x**, it leaves the string $f(x)$ on the tape when it stops

-  Examples: increment and add 

### Algorithm Definition

> A TM that **decides** some language or **computes** some function represents an algorithm for that task

- There may be many TMs for a task => different algorithms for the same task
- TM and algorithm are interchangeable terms
- Allows us to make precise statements about algorithms 

---