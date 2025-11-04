# Church-Turing Thesis

> [!IMPORTANT]
>
> Church-Turing Thesis: **a universal Turing machine (UTM) can perform any computation (decide a language or compute a function) that can be done by any physically realizable computing device**

- This reduces the study of computation in the real world to the study of TMs
- The statement is not a mathematical statement subject to a rigorous proof
- The statement is about a law of nature and which kinds of computations can be done in our universe
- Overwhelming evidence that it is true (though not a proof)
  - All conceived computational models have been shown to be equivalent to a TM
  - If you come up with a more powerful model the thesis will be disproved and you will achieve fame and glory!
    - Maybe a homework problem 😀
- Contrapositive of the thesis: **if some computation can't be done on a TM then it can't be done at all!**

## Variations

- Changes in the TM model => all can be simulated by a UTM
  - Multiple tapes
  - Nondeterminism
  - ...

## Turing Completeness

> [!IMPORTANT]
>
> A model is said to be **Turing complete** or **Turing universal** if it is equivalent to the Turing machine model (it can recognize/decide the same set of languages and compute the same set of functions)

- Examples of Turing complete models:
  - Lambda calculus (Church)
  - Counter machines (Minsky)
  - Cellular automata (Conway)
  - Your computer
  - Any general-purpose language (Java, Python, C, JavaScript, etc.)
  - C++ templates
  - ...
- Despite decades of attempts, every reasonable computational model can simulate a TM (at least as powerful as a TM) and can be simulated by a TM (no more powerful than a TM)
- Proven facts about TMs apply to our real-world computers in practice

---