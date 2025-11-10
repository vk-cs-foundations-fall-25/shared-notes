# Complexity

1. **Universailty** (recap)

   - A Turing machine (TM) can perform any computation that can be done by any physically realizable computer (**Church-Turing thesis**)

   - Not a proven mathematical truth

   - But rather a statement about the natural world supported by a preponderance of evidence
     - Smart folks have developed many computational models over the decades but each is no more powerful than a Turing machine i.e. can be simulated by a Turing machine

2. **Computability** (recap)

   - **There exist problems that can't be solved by a TM** (and so, because of universality, by any other computer)

   - This is a mathematical truth (#problems > #TMs)

   - Many of the unsolvable problems are problems we care about
     - Halting: whether a given program halts
       - Rice's theorem: whether a given program has any specific non-trivial property

3. **Complexity** (new)

   1. **A TM can *efficiently* perform any computation that can be efficiently computed by any physically realizable computer (extended Church-Turing thesis)**
      1. Not a mathematical truth but rather a statement about the natural world
      2. For any given algorithm that runs in time proportional to $T(n)$ on some physically realizable computer, where $n$ is the problem size, we can construct a TM that performs the same computation in time proportional to $(T(n))^k$ for some constant $k$
      3. So although the TM may be slower, it won't be exponentially slower
   2. Tractable problems can be solved in **polynomial** time whereas intractable problems seem to require **exponential** time
   
      - Polynomial time $\propto n^k$
   
      - Exponential time $\propto 2^{(n^k)}$
   
---