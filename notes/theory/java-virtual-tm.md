# Virtual TM in Java

- Recall we implemented a virtual DFA and NFA in Java
- Similarly we can implement a virtual TM
- Here's a sketch of the implementation
  - The full implementation will be a homework problem

## Tape

- Not sufficient to just track the input
- Need access to parts of the tape beyond the input
- And tape is infinite
- Strategy:
  - Use two stacks to track symbols to the left and the right of the current symbol

```java
public class Tape {
  public Tape(String input) {
    right.push(' ');
    for (int i = input.length() - 1; i >= 0; i--) {
      right.push(input.charAt(i));
    }
    currentSymbol = right.pop();
  }
  
  public char read() {...}
  public void write(char symbol) {...}
  
  public void moveLeft() {
    right.push(currentSymbol);
    if (left.isEmpty()) {
      left.push(' ');
    }
    currentSymbol = left.pop();
  }
  public void moveRight() {...}
  
  private char currentSymbol;
  private final Stack<Character> left = new Stack<>();
  private final Stack<Character> right = new Stack<>();
}
```

## State

- Similar to the DFA case

```java
public class State {
  public void addTransition(Character inputSymbol, Transition transition) {...}
  public Transition getTransition(Character inputSymbol) {...}
  ...
}
```



## Transition

- Need to track the following in a state transition:
  - next state
  - output symbol
  - move left or right

```java
public class Transition {
  public enum Direction { L, R}
  
  public Transition(State nextState, Character writeSymbol, Direction direction) {...}
  ...
}
```

## TM

```java
public class TM {
  public TM() {...}
  
  public void setStartState(State state) {...}
  public void addAcceptState(State state) {...}
  public void addRejectState(State state) {...}

  /** Returns a string containing the final state (accept/reject) and the tape contents. */
  public String run(String input) {
    Tape tape = new Tape(input);
    ...
  }
}
```

## UTM

- The `TM` class can be used to programatically construct any specific TM
- Its also possible to implement a Universal Turing Machine (UTM) that can simulate any specific TM on any input
- Key idea: **a TM can be specified in the same way as data** e.g. via a string
  - *Stored program concept* in the *von Neumann architecture* leading to **general-purpose computers**
  - Turing imagined this even before the first computer was ever built!

Here's a virtual UTM in Java:

```java
public class UTM {
  public UTM(String TM) {...}
  
  /** 
   * Simulates running the specific TM on the specified input.
   * Returns a string containing the final state (accept/reject) and the tape contents. 	 */
  public String simulate(String input) {...}
}
```

- It's possible to implement a UTM as a Turing machine itself. It can simulate the operation of any TM on any given input (with the specific TM provided as part of the input to the UTM)
  - The construction is beyond the scope of this course
    - Turing's paper showed it (albeit with some bugs)

### String Representation

- We'll use the notation \<TM\> to denote a string representation of TM

![](tm-incrementer.excalidraw.svg)

- The actual representation is not all that important

- Possible \<TM\> formats:

  - Graphviz

  ```graphviz
  digraph {
      start [style=invisible];
      accept [color=green];
      start -> q0;
      q0 -> q0 [label="R"];
      q0 -> q1 [label="⊔:L"];
      q1 -> q1 [label="1:0,L"];
      q1 -> q2 [label="0:1"];
      q1 -> q2 [label="⊔:1"];
      q2 -> accept;
  }
  ```

	- Your own

  ```
  start q0
  accept q2
  q0 q0 0:0,R # a transition
  q0 q0 1:1,R
  q0 q1 ⊔:⊔,L
  q1 q1 1:0,L
  q1 q2 0:1
  q1 q2 ⊔:1
  ```

### Programs that process other programs

- Does the idea of a program that processes another program sound strange to you?

- It shouldn't!

- You encounter this all the time:

  - Your phone app downloader processes an app program
  - Your compiler processes your high-level program into assembly
  - Your Java compiler (`javac`) converts your Java program into another programming language called Java bytecode
  - The Java Virtual Machine (JVM) (`java`) takes a bytecocde program as input and runs it, ultimately using your computer's machine language
