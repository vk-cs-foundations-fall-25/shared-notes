# Measuring Complexity

## What Is Complexity?

- Of all solvable problems, some are more complex than others
- Complex $\neq$ how hard  it is to come up with a solution 
  - Take human ability out of the equation and assume an optimal human who can solve any solvable problem

- Complexity = feasibility/**tractability** of finding a solution
  - Tractablity => runs in a reasonable amount of **time** and uses a reasonable amount of resources (like **memory**)


- A program that is much slower than required or requires more memory than available is useless for all practical purposes
- How can you know the tractability of a program?
  - *a posteriori*: run the program and measure the time/memory
  - *a priori*: analyze the program to determine the time/memory (without running the program)
- So which strategy should you use? Both!
  - Before coding, analyze the run-time of the algorithms to determine if they meet the performance requirements
  - After coding, measure the run-time of the program to verify that it meets the requirements
- How can you analyze the run-time of a program without running it?
  - That's what this section is about!

## Runtime Analysis

- Donald Knuth: Turing award winner and the father of algorithms analysis
- Total run time is based on two factors
  
  1. The cost of executing each statement

       - property of the system (language and hardware)
  
  2. The frequency of executing each statement

        - property of the algorithm (independent of language and hardware)
  
- Total run time = $\sum c_i f_i$ where $c_i, f_i$ are the cost and frequency respectively of statement $i$
  - But that is a tedious calculation!

- A simpler, yet powerful, approach is to use a model of running time called **order of growth**
  - Most programs have a *problem size* that characterizes the difficulty of the computational task
    - e.g. a program that computes $n!$ has a problem size of $n$
  - As the problem size increases, the runtime increases
    - e.g. if you double $n$ it takes twice as long to compute the factorial
  - The order of growth of the runtime is a *function of the problem size* and denotes *how the runtime increase when the problem size increases* (with a few caveats)
  - It is expressed using the **"Big O" notation** $O(f(n))$
      - $n$ is the problem size
      - $f(n)$ is a function of $n$ 
  - There are a few caveats on $f(n)$ that simplify the analysis
    
      1. Only keep the leading term (highest power) in $n$ 
         - e.g. $n^2 + 2n+ 3 \rightarrow n^2$
      2. Set the coefficient of the leading term to 1 (regardless of what the actual coefficient is)
         - e.g. $6n^2 \rightarrow n^2$
  - The above caveats mean that although $f(n)$ doesn't specify the precise runtime of a program, it does specify the **ratio of runtimes** for two different **large problem sizes** (thereby justifying the name order-of-growth)
    - $\text{runtime}(n_2) / \text{runtime}(n_1) = f(n_2) / f(n_1)$ for large $n_1$ and $n_2$
  - What about small problem sizes?
    - That's already fast, so no need to worry about it

### Example: Factorial

```java
public static long factorial(long n) {
    long result = 1;
    for (long i = 1; i <= n; i++) {
        result = result * i;
    }
    return result;
}
```

Somewhat precise runtime:
- $1 + n \times 2 + 1 = 2n + 2$
  

Keeping only the leading term with coefficient 1, the runtime becomes:
- $O(n)$

Results from running the program:
```java
public static void main(String[] args) {
    final int numRuns = 100_000;
    double previousSeconds = -1;
    System.out.println("| n | seconds | doubling-ratio |");
    System.out.println("| --- | --- | --- |");
    for (long n = 100; n < 100_000; n *= 2) {
        Stopwatch stopwatch = new Stopwatch();
        for (int i = 0; i < numRuns; i++) {
            factorial(n);
        }
        double elapsedSeconds = stopwatch.getElapsedSeconds();
        if (previousSeconds > 0) {
            double ratio = elapsedSeconds / previousSeconds;
            System.out.println("| " + n + " | " +
                    String.format("%.2f", elapsedSeconds) +
                    " | " + String.format("%.2f", ratio) + " |\n");
        } else {
            System.out.println("| " + n + " | " +
                    String.format("%.2f", elapsedSeconds) + " | |\n");
        }
        previousSeconds = elapsedSeconds;
    }
}
```

| n     | seconds | measured-ratio | O-ratio |
| ----- | ------- | -------------- | ------- |
| 100   | 0.01    |                |         |
| 200   | 0.01    | 2.20           | 2.0     |
| 400   | 0.02    | 2.18           | 2.0     |
| 800   | 0.05    | 2.17           | 2.0     |
| 1600  | 0.11    | 2.06           | 2.0     |
| 3200  | 0.22    | 2.07           | 2.0     |
| 6400  | 0.44    | 1.96           | 2.0     |
| 12800 | 0.87    | 2.00           | 2.0     |
| 25600 | 1.75    | 2.00           | 2.0     |
| 51200 | 3.50    | 2.01           | 2.0     |

## Order-of-growth Classifications

Here are the most common order-of-growth classifications:
| $O$           | description  | doubling ratio | example programs          | notes                                     |
| ------------- | ------------ | -------------- | ------------------------- | ----------------------------------------- |
| $O(1)$        | constant     | 1              | print "Hello World"       |                                           |
| $O(\log n)$   | logarithmic  | 1              | binary search             | reduce problem by half: T(n) = T(n/2) + 1 |
| $O(n)$        | linear       | 2              | factorial                 | single loop over $n$                      |
| $O(n \log n)$ | linearithmic | 2              | mergesort                 | divide-and-conquer: T(n) = 2 T(n/2) + n   |
| $O(n^2)$      | quadratic    | 4              | insertion sort            | two nested loops                          |
| $O(n^3)$      | cubic        | 8              | all triples that sum to 0 | three nested loops                        |
| $O(2^n)$      | exponential  | $2^n$          | all subsets of n elements | impractical for large problems!           |

## Exercises

1. What is the big-O runtime of the following method?

   ```java
   public static boolean contains(int[] a, int target) {
       if (a.length < 1) {
           return false;
       }
       for (int i = 0; i < a.length; i++) {
           if (a[i] == target) {
               return true;
           }
       }
       return false;
   }
   ```

   <details>


   <summary>Answer</summary>

   - $O(n)$ where $n$ is the array length
     - Best case: $1$
     - Worst case: $n$
     - **Average case**: $n/2 \rightarrow n$

   </details>

2. What is the big-O runtime of the following method?

   ```java
   public static void printPairsThatSumToZero(int[] a) {
       for (int i = 0; i < a.length; i++) {
           for (int j = i + 1; j < a.length; j++) {
               if ((a[i] + a[j]) == 0) {
                   System.out.println(a[i] + " + " + a[j] + " = 0");
               }
           }
       }
   }
   ```

   <details>


   <summary>Answer</summary>

   - $O(n^2)$ where $n$ is the array length
     - number of times the ```if``` statement runs:
       - $(n-1) + (n-2) + (n-3) + ... 1 = \frac{n(n-1)}{2} \rightarrow n^2$
         </details>

3. What is the big-O runtime of the following method?

   ```java
   public static void printTriplesThatSumToZero(int[] a) {
       for (int i = 0; i < a.length; i++) {
           for (int j = i + 1; j < a.length; j++) {
               int sum = a[i] + a[j];
               for (int k = j + 1; k < a.length; k++) {
                  if ((sum + a[k]) == 0) {
                   System.out.println(a[i] + " + " + a[j] + " + " + a[k] + " = 0");
               }
           }
       }
   }
   ```

   <details>


   <summary>Answer</summary>

   - $O(n^3)$ where $n$ is the array length
     - number of times the ```if``` statement runs:
       - $\sum_{i=1}^{n-2} \sum_{j=i+1}^{n-1} \sum_{k=j+1}^{n} 1$ 
       - $= \sum_{i=1}^{n-2} \sum_{j=i+1}^{n-1} (n - j)$
       - $= \sum_{i=1}^{n-2} \left[ n(n - 1 - i) - \frac{n(n-1)}{2} + \frac{i(i + 1)}{2}\right]$
       - $=\sum_{i=1}^{n-2} \left[ \frac{n(n-1)}{2} + i(\frac{1}{2} - n) + \frac{1}{2} i^2\right]$
       - $\rightarrow n^3$
         </details>

## Two Broad Classes

1. **Polynomial** time: $O(n^b)$ where $b$ is a positive constant
   - e.g. $O(1), O(\lg n ), O(n), O(n \lg n), O(n^2), O(n^3), ...$
   - Most algorithms you've encountered so far were likely poylynomial time algorithms
2. **Exponential** time: $O(2^{n^b})$
   - e.g. $O(2^n)$
   - These are intractable even for moderate problem sizes

### Back Of The Envelope

- The most poweful supercomputer today can execute ~$10^{18}$ instructions per second (exaflop)

- Here's a table of some common algorithms and approximately how long the above supercomputer would take to solve those problems:

  | Algorithm      | O(n)                                                             | n                  | Supercomputer Run Time                                           |
  | -------------- | ---------------------------------------------------------------- | ------------------ | ---------------------------------------------------------------- |
  | Insertion sort | $n^2$ (polynomial)                                               | $10^9$             | ~1 second                                                        |
  | Subsets        | $2^n$ (exponential)                                              | 100                | > 10,000 years                                                   |
  | Permutations   | $n! \sim \sqrt{2\pi n} \left(\frac{n}{e}\right)^n$ (exponential) | 52 (deck of cards) | > $10^{42}$ years > age of the universe ($14 \times 10^9$ years) |

- Clearly the polynomial time algorithm is tractable, even for large problem sizes

- And the exponential time algorithms are intractable, even for moderate problem sizes

### Exercises

1. Implement each of the algorithms in the table above in Java

## The Worst Case

- Three cases for big-O
  - Best: the fastest run time (specific inputs)
    - e.g. O(1) when linearly searching over a list for the element which happens to be first in the list
  - Average: the average run time (random inputs)
    - e.g. O(n) when linearly searching over a list for random elements (taking n/2 on average)
  - Worst: the slowest run (specific inputs)
    - e.g. O(n) when linearly searching over a list for the element which happens to be last in the list
- For practical purposes we're usually interested in the average case, while being aware of the worst case
- For Complexity theory, we'll focus on the worst case to simplify analysis and to provide guarantees

---