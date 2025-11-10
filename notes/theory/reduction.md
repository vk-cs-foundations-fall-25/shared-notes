# Reduction

## Overview
- We know that there are more languages than algorithms, so some languages are unsolvable
- We saw an example of an unsolvable problem: the halting problem
- What are some other unsolvable problems?
- Determine that using **reduction**

	> convert one problem to another problem such that a solution to the second problem can be used to solve the first problem.


## Warmup

- Problem A: Find the largest number in a list of numbers e.g. [6, 4, 9, 2, 1] => 9
- Problem B: Sort the numbers in a list in ascending order e.g. [6, 4, 9, 2, 1] => [1, 2, 4, 6, 9]
- Problem A reduces to problem B
  - This means that we can use the solution to problem B to solve problem A
- How?
  1. Solve problem B to get the list in ascending order
  2. Then solve problem A by reading the last item in the sorted list to get the max

## Rice's Theorem

> Determining whether a given program has *any* non-trivial property is unsolvable

- What's a non-trivial property of a program?
  1. Something that depends on the behavior of the program rather than say the syntax
  2. Such a property is present in some programs and not in others
  - Examples:
    - Does a program compute a specific function like $x^2$
    - Does a program produce any output
    - ...

### Proof By Reduction To Halt (Sketch)

- Suppose there exists a Java function `hasProperty` that decides whether a given function has a specific non-trivial property (e.g. it outputs fewer than 10 characters)

  - A function in this sketch is modeled as a  Java `Predicate<String>` interface that has a `test` method which takes in a String and returns a boolean


  ```java
  public static boolean hasProperty(Predicate<String> f) {...}
  ```

- Since the property is non-trivial, there must exist:

  - A function `funcYes` that has the property 

    ```java
    Predicate<String> funcYes = ...;
    assertTrue(hasProperty(funcYes));
    ```

  - A function `funcNo` that does not have the property

    - Without loss of generality, assume that funcNo is a non-halting function
      - If non-halting functions have the property of interest then we can consider the complement property and still solve the same problem

    ```java
    Predicate<String> funcNo = ...; // doesn't halt when called
    assertFalse(hasProperty(funcNo));
    ```

- Define a function `Mw`, that takes as input a function `M` and its input `w`, in the following way: 

```java
public static Predicate<String> createMw(Predicate<String> M, String w) {
  return x -> {
    // Run M on w. 
    // If it doesn't halt, the returned predicate is equivalent to funcNo.
  	M.test(w);
    
    // If M on w halts, run funcYes on x.
    // So the returned predicate is equivalent to funcYes in the halting case.
    return funcYes(x);
  }
}
```

- Now we can define a `halts` function using the `hasProperty` function thus:

  ```java
  public static boolean halts(Predicate<String> M, String w) {
    Predicate<String> Mw = createMw(M, w);
    
    // From the definition of createMw, we know:
    // 1. If M halts on w, Mw == funcYes
    // 2. Otherwise, Mw == funcNo
    
    // Halts and returns whether Mw has the specific property.
    // And Mw has the property if and only if M halts on w.
    return hasProperty(Mw);
  }
  ```

- But we know that the function `halts` can't exists!

- So the original assumption that `hasProperty` exists must be wrong

- `halts` reduced to `hasProperty`

  - So if halts can't exist, nor can hasProperty

---

"IN A VERY REAL SENSE, UNSOLVABILITY and Rice’s theorem provide a foundation for understanding why ensuring reliability in software systems is so difficult. Much as we would like to write programs that ensure that our software has any number of desirable properties, it is not possible to do so. People who understand this fact will have much more success engaging with computation than people who do not."

Sedgewick, Robert; Wayne, Kevin. Computer Science: An Interdisciplinary Approach (Function). Kindle Edition. 

## More Unsolvable Problems

- Optimal data compression
  - It's not possible to determine whether some data has been compressed as much as possible or is there still room for improvement
- Optimal compiler
  - There is no compiler that can guarantee its ability to optimize fully every program
- Program equivalence
  - Not possible to determine whether two programs compute the same result
- Virus recognition
  - Not possible to determine whether a given program is a virus
- Memory management
  - Not possible to determine if a given variable will ever be referenced again
- Hilbert's 10th problem
  - Not possible to determine whether a given mutivariate polynomial has integer roots
- Chaos
  - Not possible to determine if a given dynamical system is chaotic

---