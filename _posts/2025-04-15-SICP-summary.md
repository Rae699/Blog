---
layout: post
title: "SICP #10 — Finale thoughts"
date: 2025-03-07
categories: cs
author: Remy
description: "SICP #10"
github: https://github.com/Rae699
comments: false
---

## **Part I — Rethinking Programming from First Principles**  

### **Why SICP?**  

Most programming books teach syntax, frameworks, or best practices. *Structure and Interpretation of Computer Programs* (SICP) does something entirely different—it rewires how you *think*.  

Before SICP, I saw programming as a set of instructions to be executed where syntax was almost the most important thing.
Now, I see it as a process—an unfolding sequence of transformations driven by underlying mathematical principles. 

The impact of SICP on the thought process is profound:
1.	It teaches abstraction deeply. You don't just write functions—you learn to create powerful abstractions, thinking in terms of layers and compositions. That's a crucial skill for designing scalable systems.
2.	It rewires your thinking to focus on expressiveness over syntax. Unlike books that focus on syntax-heavy programming, SICP forces you to think in terms of mathematical rigor and expressive models of computation.
3.	It reveals deep principles of software engineering. Recursion, higher-order functions, data abstraction, modularity, and interpreters—all central to writing robust software—are taught in an elegant way.
4.  It teaches computation as a craft. You're not just solving problems, you're designing elegant, efficient solutions using minimal yet expressive constructs.
5.	It has shaped legendary engineers. It was the core MIT curriculum for decades, influencing the design of Lisp, Scheme, and many modern functional programming paradigms.


---

### **The Immediate Impact**  

Just 40 pages in, my perspective had already shifted. Take the **substitution model**—I no longer see it as theory. 
I can now visualize exactly how an interpreter evaluates expressions, breaking them down step by step.  

Then, comes the evaluation strategy:  
- **Applicative-order**: Evaluate all arguments first, then apply the function once the code encounters primitives only.
- **Normal-order**: Delay evaluation until absolutely necessary. Deferred options for recursion leads to a growing stack... 

This isn't just an academic distinction. Knowing when and why an evaluation strategy matters is foundational for performance, optimization, and avoiding unnecessary computation.  

And then there's recursion. I finally *get* recursion—not just how to write it, but what's happening at a deeper level:  
- A **recursive process** builds up deferred operations, consuming memory.  
- An **iterative process** runs smoothly in constant space, no matter the depth.  

Understanding this is the difference between writing code that works and writing code that scales.  


---

### **Why This Matters**  

This isn't just about mastering Scheme or finishing a book. 

SICP builds the mental models that great engineers rely on—models that scale to anything, from algorithmic problem-solving to systems design.  

Next, I'll move deeper into *Computer Systems: A Programmer's Perspective*, refining my understanding of memory, CPU performance, and low-level optimizations. 

Then, *The Algorithm Design Manual* to solidify my approach to problem-solving.  

This structured learning approach ensures that I'm not just accumulating knowledge—I'm actively building a foundation that will compound over time.  

More to come.  


---

### **How SICP Connects to Deeper Math**  
- Just two exercises in Chapter 1 tie directly to:  
  - **Combinatorics** (Exercise 1.12) → Pascal's Triangle.  
  - **Recurrence relations** (Exercise 1.13) → Fibonacci sequences, induction.  
- These aren't random exercises—they reinforce foundational CS concepts that appear across algorithms and systems design.  


---

## **Part II — Chapter I Summary & Notes**  

### **The Substitution Model of Evaluation**  
- Computation unfolds step by step, just like an interpreter processes code.  
- Two primary evaluation strategies are used:  
  - **Applicative-order evaluation** (evaluate all arguments immediately).  
  - **Normal-order evaluation** (delay evaluation as long as possible).  


---

### **Recursive vs. Iterative Processes**  
- **Recursive process:** Deferred operations stack up → takes up memory → potential stack overflow.  
- **Iterative process:** Uses a constant amount of memory → executes efficiently.  
- Example:  
  - A naive recursive Fibonacci function is **tree-recursive** → exponential time complexity.  
  - An optimized version (using tail recursion) is **linear iterative** → constant space.  

How to properly build an iterative process?
As demonstrated in exercise 1.16, *the technique of defining an invariant quantity that remains unchanged from state to state is a powerful way to think about the design of iterative algorithms.*

The keys to problems are:
- breakdown problems into subproblems, using mathematical properties (like if n is even do, b^n = (b^{n/2})^2 or if n is odd, bring it to an even form to compute it: b^n = b \times b^{n-1} )
- is to use the invariant to define the sate transformation in such a way that for instance the product ab^n is unchanged from state to state. In the exercise, the invariant is acting as an accumulator in a way.

---

### **The Ackermann Function**  
- A powerful example of how recursion can explode computational complexity.  
- Small inputs lead to massive recursion depth.  
- Demonstrates why understanding recursion *matters*—it's not just a coding trick, but a fundamental computational concept.  

![Growth_of_Functions]({{ site.baseurl }}/assets/growth_of_f_g_h_k_from_the_ackermann_function_examples.png)


---

### **Normal-Order Evaluation and the Stack Explosion in GCD**  

When we talk about evaluating functions, most programmers are used to **applicative-order evaluation**—where arguments are computed before a function is applied. 
But what happens when we delay evaluation and only substitute arguments without computing them immediately? 

Enter **normal-order evaluation**, where things quickly get out of hand.

Let's break down what happens when we compute `gcd(a, b)` using **normal-order evaluation**, step by step. 
This will show why normal-order recursion can lead to **stack explosion** and unnecessary recomputation.


#### **The Problem: Computing GCD Using Normal-Order Evaluation**

Given Euclid's algorithm for the greatest common divisor:

```scheme
(define (gcd a b)
  (if (= b 0)
      a
      (gcd b (remainder a b))))
```

Instead of computing `remainder(a, b)` before making the recursive call, **normal-order evaluation** delays all computation and just substitutes expressions, leading to deeper and deeper function calls before any actual numbers are calculated.


#### **Breaking Down Normal-Order Expansion**

Let's go through the expansion step by step using `gcd(a, b)`. Each step **substitutes** the remainder operation instead of evaluating it, causing a deep nesting effect.

```
Step 1: First Expansion
gcd(a, b)
   |
   ├── gcd(b, r(a, b))  ⬅︎ Substituting, not computing
   |
Step 2: Expand Again
   |
   ├── gcd(r(a, b), r(b, r(a, b)))  ⬅︎ Substituting again
   |
Step 3: Expand Further
   |
   ├── gcd(r(b, r(a, b)), r(r(a, b), r(b, r(a, b))))  ⬅︎ Even deeper
   |
Step 4: Expansion Continues (Stack Grows)
   |
   ├── gcd(r(r(a, b), r(b, r(a, b))),
   |       r(r(b, r(a, b)), r(r(a, b), r(b, r(a, b)))))  ⬅︎ Substitution explosion
   |
Step 5: Keep Expanding Until Base Case
   |
   ├── ...
   |
   ├── gcd(m, 0)  ⬅︎ Base case reached
   |
Step 6: Unwinding Phase (Stack Shrinks)
   |
   ├── return m
   |
   ├── return m
   |
   ├── return m
   |
   ├── return m  ⬅︎ Final answer propagates back
```

At this point, the **call stack has exploded**, containing deeply nested expressions before ever reaching the base case.

#### **What Happens in the Call Stack?**

To visualize the problem, let's break it down into **expansion** and **unwinding** phases.

##### **Call Stack (Expanding Phase)**
```
gcd(a, b)  
gcd(b, r(a, b))  
gcd(r(a, b), r(b, r(a, b)))  
gcd(r(b, r(a, b)), r(r(a, b), r(b, r(a, b))))  
gcd(r(r(a, b), r(b, r(a, b))), r(r(b, r(a, b)), r(r(a, b), r(b, r(a, b)))))  
...
gcd(m, 0)  ⬅︎ Base Case Hit
```

At this point, the function calls are deeply nested, **waiting for every remainder operation to be computed.**
Upon reaching the base case, we cease deferring the computation and proceed to execute it.
Why? Because we reach a point where only primitives are left, there is no operation to defer anymore, only integers.

##### **Call Stack (Unwinding Phase)**
```
return m  
return m  
return m  
return m  
return m  ⬅︎ Final Answer  
```
Upon reaching the base case, the function starts to unwind the call stack, returning the final GCD at each level until it reaches the initial call.
In essence, each return statement corresponds to one level of the stack being resolved.

#### **Key Takeaways**
✅ **Normal-order evaluation substitutes before computing**, leading to deeply nested expressions.  
❌ **This causes redundant re-computation of `remainder(a, b)`, leading to inefficiency.**  
💡 **Applicative-order evaluation avoids this problem by computing `remainder(a, b)` first before making recursive calls.**  

This is why most programming languages use **applicative-order evaluation** by default. When using recursion, normal-order evaluation can lead to massive stack growth, unnecessary computations, and inefficiency.
Understanding how evaluation strategies impact recursion is crucial. The difference between **substituting first vs. computing first** can mean the difference between an efficient algorithm and one that crashes your system. This breakdown of `gcd(a, b)` under **normal-order evaluation** highlights why **execution order matters**, and why we should always be mindful of how function calls expand before they collapse.


--- 

### **Time & Space Complexity: Why Order of Growth Matters**  

One of the biggest mental shifts SICP introduces early on is how to analyze an algorithm's efficiency using **order of growth**.  

Before, I thought of efficiency in terms of "fast" vs. "slow." Now, I see it in terms of *scaling behavior*.  

- If an algorithm takes 1 second for an input size of 10, how long does it take for 100?  
- How does the memory footprint grow as input scales?  
- What matters more—constants or the fundamental structure of the process?  

That's where **Big-O notation** comes in.  

Big-O describes how the *order of growth* of an algorithm changes as input size increases. It strips away implementation details and focuses on the **magnitude** of growth.  

For example, consider an algorithm that runs in:  

- \( O(n) \) → Linear time  
- \( O(n^2) \) → Quadratic time  
- \( O(2^n) \) → Exponential time  

A **quadratic** algorithm will always outgrow a **linear** one—even if the linear one has a huge constant overhead. THink about extending the lines towards infinity if it is not clear. 

**Constants are irrelevant for asymptotic analysis** because:  
- Complexity theory is about how an algorithm behaves as \( n \) approaches infinity.  
- A function's order of growth is determined by its dominant term (e.g., in \( 5n^2 + 3n + 1000 \), the \( n^2 \) term dominates for large \( n \)).  
- No matter how large a constant is, a faster-growing function will eventually outgrow a slower-growing one.  

To visualize this, let's look at an example.  

#### **Visualizing Growth Rates**  

##### **1. Exponential vs. Polynomial Growth**  

The difference between polynomial and exponential growth is *brutal*. Even if a polynomial function (\( O(n^2) \)) starts with a huge constant overhead, an exponential function (\( O(2^n) \)) will eventually overtake it—fast.  

Take a look:  
![complexity_classical_examples]({{ site.baseurl }}/assets/complexity_classical_examples.jpg)  

At first, \( O(n^2) \) appears to be growing at a steady rate. But as \( n \) increases, \( O(2^n) \) explodes.  

This is why algorithms with exponential complexity are **practically unusable for large inputs**. No matter how optimized, they will always be outperformed by even a poorly written polynomial-time solution.  


##### **2. Linear Growth and Constant Multiples**  

Now, let's zoom in on **linear growth** (\( O(n) \)).  

At first glance, these three functions look quite different:  

- \( O(n) \)  
- \( O(2n) \)  
- \( O(6n + 10) \)  

You might think that \( O(6n + 10) \) grows much faster. But in complexity terms, **they are all still O(n)**.  

This is the key idea:  

- **Constants don't affect asymptotic complexity.**  
- **When trending towards infinity, a function with a faster-growing order will always overtake a function with a lower order, no matter how big the constant.**  

For example:  

- \( O(6n + 10) \) grows faster than \( O(n) \) for small inputs.  
- But if we compare \( O(n) \) to \( O(n^2) \), \( O(n^2) \) will always win eventually—even if it starts 1,000 times slower.  

![Growth_of_Different_Complexities]({{ site.baseurl }}/assets/Growth_of_Different_Complexity_Classes.png)  

Remember, a function could be classified as:
- **Linear**: \( f(x) = ax \)
- **Affine**: \( f(x) = ax + b \)
- **Constant**: \( f(x) = n \)

If we were to oversimplify the maths logic behind Big O, and in order to evaluate Big O notation:
- Additive constants are irrelevant in the grand scheme, so an affine function reduces to a linear one.
- Multiplicative constants (slope coefficients) are also irrelevant, so a linear function is simply proportional to \( x \).

Remember: While this is a helpful starting point, it's an oversimplification. Real algorithmic analysis requires considering a broader spectrum of complexities including logarithmic (\( O(\log n) \)), linearithmic (\( O(n \log n) \)), polynomial (\( O(n^k) \)), and exponential (\( O(2^n) \)) growth rates. The principles above are just the basics of understanding how we simplify complexity analysis.

In terms of asymptotic analysis (Big O notation), here's how we analyze complexity:

1. **Basic Principles of Big O**:
   - We focus on the growth rate as input size approaches infinity
   - We consider the worst-case scenario
   - We drop lower-order terms
   - We drop constant coefficients

2. **Common Time Complexities** (from fastest to slowest):
   - \( O(1) \) - Constant time
   - \( O(\log n) \) - Logarithmic time
   - \( O(n) \) - Linear time
   - \( O(n \log n) \) - Linearithmic time
   - \( O(n^2) \) - Quadratic time
   - \( O(2^n) \) - Exponential time

3. **Simplification Rules**:
   - Drop constants: \( O(2n) = O(n) \)
   - Drop lower-order terms: \( O(n^2 + n) = O(n^2) \)
   - Keep the highest-order term: \( O(n^3 + n^2 + n) = O(n^3) \)

4. **Examples**:
   ```python
   # O(1) - Constant time
   def get_first(arr):
       return arr[0]
   
   # O(n) - Linear time
   def find_max(arr):
       max_val = arr[0]
       for x in arr:  # n iterations
           if x > max_val:
               max_val = x
       return max_val
   
   # O(n²) - Quadratic time
   def bubble_sort(arr):
       n = len(arr)
       for i in range(n):  # n iterations
           for j in range(n-1):  # n iterations
               if arr[j] > arr[j+1]:
                   arr[j], arr[j+1] = arr[j+1], arr[j]
   ```

Remember: Big O notation gives us an upper bound on the growth rate of an algorithm's resource usage (usually time or space) relative to input size. It helps us make informed decisions about algorithm selection and optimization.

##### **3. Why This Matters in Practice**  

While complexity theory tells us that constants don't matter *asymptotically*, in real-world applications, they sometimes do.  

- If two algorithms have the same Big-O complexity, **the one with the smaller constant factor may still be preferable in practice** (e.g., an \( O(n) \) algorithm with a huge overhead might be slower than an \( O(n \log n) \) one for practical input sizes).  
- However, when input sizes grow large enough, **only the order of growth matters**. A well-optimized \( O(n^2) \) algorithm will eventually lose to even a poorly optimized \( O(n \log n) \) algorithm.  


---

##### **The Complexity Theory vs. Practical Performance Tradeoff**  

TO REVIEW LATER

| **Aspect**           | **Complexity Theory (Big-O)** | **Practical Performance** |
|----------------------|--------------------------------|---------------------------|
| Constants Matter?    | No, ignored in asymptotic analysis | Yes, for small inputs |
| Focus               | Growth rate as (n \to \infty) | Execution time for realistic input sizes |
| Example             | \( O(n) \) vs. \( O(n^2) \) → Always prefer \( O(n) \) | A poorly optimized \( O(n) \) function might be slower than a well-tuned \( O(n^2) \) one for small \( n \) |
| Goal                | Identify long-term scaling behavior | Optimize real-world execution time |


---

### **Closing Thoughts**  

SICP is not about learning to code. It's about learning to *think*.  

Each chapter rewires intuition, forcing a shift from writing instructions to designing *processes*. This is why the book is legendary—it doesn't just teach programming; it transforms how you approach computation itself.  

This is just the beginning. More deep dives, more structured learning, and more insights to come.  