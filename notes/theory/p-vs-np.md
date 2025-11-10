# P vs NP

- P is the class of problems that can be *decided* (solved) in polynomial time
  - e.g. sorting a list of numbers or finding a path between two nodes in a graph
- NP is the class of problems that can be *verified* in polynomial time
  - Equivalently, that can be solved in *nondeterministic polynomial* time
  - e.g. sudoku puzzles, traveling salesman problem (hamitonian path), prime factorizations, etc.
- What is the relationship between P and NP problems, if any?

## Two Possible Universes

![](../media/PvsNP.excalidraw.svg)

1. $P \subset NP$
2. $P = NP$

- Every problem in P is also in NP
  - Why? If you can solve the problem in polynomial time, you can verify a solution in polynomial time by solving it
- So the set NP can't be smaller than the set P
- Open question: is the set NP larger than the set P or equal to the set P?
- No one knows!
  - Smart folks have tried hard to find a polynomial time solution for an NP problem but failed
  - Literally a million dollar question: one of the seven Millennium Prize Problems (the most famous and difficult unsolved problems in mathematics), announced by the Clay Mathematics Institute (CMI) in 2000

---