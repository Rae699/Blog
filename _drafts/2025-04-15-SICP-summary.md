---
layout: post
title: "SICP #10 — Critical thinking"
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

Before SICP, I saw programming as a set of instructions to be executed. Now, I see it as a process—an unfolding sequence of transformations driven by underlying mathematical principles. This is the difference between knowing how to code and understanding *computation itself*.  

SICP doesn’t just explain concepts; it forces you to *internalize* them through precise, layered exercises. Concepts I once skimmed over—like recursion, evaluation strategies, and process growth—are now concrete, deeply understood mechanics.  


---

### **The Immediate Impact**  

Just 40 pages in, my perspective had already shifted. Take the **substitution model**—I no longer see it as theory. 
I can now visualize exactly how an interpreter evaluates expressions, breaking them down step by step.  

Then, comes the evaluation strategy:  
- **Applicative-order**: Evaluate all arguments first, then apply the function once the code encounters primitives only.
- **Normal-order**: Delay evaluation until absolutely necessary. Deferred options for recursion leads to a growing stack... 

This isn’t just an academic distinction. Knowing when and why an evaluation strategy matters is foundational for performance, optimization, and avoiding unnecessary computation.  

And then there’s recursion. I finally *get* recursion—not just how to write it, but what’s happening at a deeper level:  
- A **recursive process** builds up deferred operations, consuming memory.  
- An **iterative process** runs smoothly in constant space, no matter the depth.  

Understanding this is the difference between writing code that works and writing code that scales.  


---

### **Why This Matters**  

This isn’t just about mastering Scheme or finishing a book. 

SICP builds the mental models that great engineers rely on—models that scale to anything, from algorithmic problem-solving to systems design.  

Next, I’ll move deeper into *Computer Systems: A Programmer’s Perspective*, refining my understanding of memory, CPU performance, and low-level optimizations. 

Then, *The Algorithm Design Manual* to solidify my approach to problem-solving.  

This structured learning approach ensures that I’m not just accumulating knowledge—I’m actively building a foundation that will compound over time.  

More to come.  


---

### **How SICP Connects to Deeper Math**  
- Just two exercises in Chapter 1 tie directly to:  
  - **Combinatorics** (Exercise 1.12) → Pascal’s Triangle.  
  - **Recurrence relations** (Exercise 1.13) → Fibonacci sequences, induction.  
- These aren’t random exercises—they reinforce foundational CS concepts that appear across algorithms and systems design.  


---

## **Part II — Chapter I Summary & Notes**  

### **The Substitution Model of Evaluation**  
- Computation unfolds step by step, just like an interpreter processes code.  
- Two primary evaluation strategies are used:  
  - **Applicative-order evaluation** (evaluate all arguments (= until encountering primitives only) before applying).  
  - **Normal-order evaluation** (delay evaluation as long as possible).  


---

### **Recursive vs. Iterative Processes**  
- **Recursive process:** Deferred operations stack up → takes up memory → potential stack overflow.  
- **Iterative process:** Uses a constant amount of memory → executes efficiently.  
- Example:  
  - A naive recursive Fibonacci function is **tree-recursive** → exponential time complexity.  
  - An optimized version (using tail recursion) is **linear iterative** → constant space.  

---


### **The Ackermann Function**  
- A powerful example of how recursion can explode computational complexity.  
- Small inputs lead to massive recursion depth.  
- Demonstrates why understanding recursion *matters*—it’s not just a coding trick, but a fundamental computational concept.  

![Growth of Functions]({{ site.baseurl }}/assets/growth-of-f-g-h.png)


--- 

### **Time & Space Complexity: Why Order of Growth Matters**  

One of the biggest mental shifts SICP introduces early on is how to analyze an algorithm’s efficiency using **order of growth**.  

Before, I thought of efficiency in terms of “fast” vs. “slow.” Now, I see it in terms of *scaling behavior*.  

- If an algorithm takes 1 second for an input size of 10, how long does it take for 100?  
- How does the memory footprint grow as input scales?  
- What matters more—constants or the fundamental structure of the process?  

That’s where **Big-O notation** comes in.  

Big-O describes how the *order of growth* of an algorithm changes as input size increases. It strips away implementation details and focuses on the **magnitude** of growth.  

For example, consider an algorithm that runs in:  

- \( O(n) \) → Linear time  
- \( O(n^2) \) → Quadratic time  
- \( O(2^n) \) → Exponential time  

A **quadratic** algorithm will always outgrow a **linear** one—even if the linear one has a huge constant overhead.  

One of the first misconceptions people have when learning complexity theory is thinking that constants affect Big-O notation.  

In reality, **constants are irrelevant for asymptotic analysis** because:  
- Complexity theory is about how an algorithm behaves as \( n \) approaches infinity.  
- A function’s order of growth is determined by its dominant term (e.g., in \( 5n^2 + 3n + 1000 \), the \( n^2 \) term dominates for large \( n \)).  
- No matter how large a constant is, a faster-growing function will eventually outgrow a slower-growing one.  

To visualize this, let’s look at an example.  

#### **Visualizing Growth Rates**  

##### **1. Exponential vs. Polynomial Growth**  

The difference between polynomial and exponential growth is *brutal*. Even if a polynomial function (\( O(n^2) \)) starts with a huge constant overhead, an exponential function (\( O(2^n) \)) will eventually overtake it—fast.  

Take a look:  
![Exponential Growth O(2^n) vs Quadratic Growth O(n^2)]({{ site.baseurl }}/assets/complexity_classical_examples.png)  

At first, \( O(n^2) \) appears to be growing at a steady rate. But as \( n \) increases, \( O(2^n) \) explodes.  

This is why algorithms with exponential complexity are **practically unusable for large inputs**. No matter how optimized, they will always be outperformed by even a poorly written polynomial-time solution.  

![Exponential Growth O(2^n) vs Quadratic Growth O(n^2)]({{ site.baseurl }}/assets/complexity_classical_examples.png)


##### **2. Linear Growth and Constant Multiples**  

Now, let’s zoom in on **linear growth** (\( O(n) \)).  

At first glance, these three functions look quite different:  

- \( O(n) \)  
- \( O(2n) \)  
- \( O(6n + 10) \)  

You might think that \( O(6n + 10) \) grows much faster. But in complexity terms, **they are all still O(n)**.  

This is the key idea:  

- **Constants don’t affect asymptotic complexity.**  
- **When trending towards infinity, a function with a faster-growing order will always overtake a function with a lower order, no matter how big the constant.**  

For example:  

- \( O(6n + 10) \) grows faster than \( O(n) \) for small inputs.  
- But if we compare \( O(n) \) to \( O(n^2) \), \( O(n^2) \) will always win eventually—even if it starts 1,000 times slower.  

![Growth of Different Complexities]({{ site.baseurl }}/assets/growth_of_different_complexities.png)  

---

##### **Why This Matters in Practice**  

While complexity theory tells us that constants don’t matter *asymptotically*, in real-world applications, they sometimes do.  

- If two algorithms have the same Big-O complexity, **the one with the smaller constant factor may still be preferable in practice** (e.g., an \( O(n) \) algorithm with a huge overhead might be slower than an \( O(n \log n) \) one for practical input sizes).  
- However, when input sizes grow large enough, **only the order of growth matters**. A well-optimized \( O(n^2) \) algorithm will eventually lose to even a poorly optimized \( O(n \log n) \) algorithm.  

##### **The Complexity Theory vs. Practical Performance Tradeoff**  

TO REVIEW LATER
| **Aspect**           | **Complexity Theory (Big-O)** | **Practical Performance** |
|----------------------|--------------------------------|---------------------------|
| Constants Matter?    | No, ignored in asymptotic analysis | Yes, for small inputs |
| Focus               | Growth rate as \( n \to \infty \) | Execution time for realistic input sizes |
| Example             | \( O(n) \) vs. \( O(n^2) \) → Always prefer \( O(n) \) | A poorly optimized \( O(n) \) function might be slower than a well-tuned \( O(n^2) \) one for small \( n \) |
| Goal                | Identify long-term scaling behavior | Optimize real-world execution time |

---

### **Closing Thoughts**  

SICP is not about learning to code. It’s about learning to *think*.  

Each chapter rewires intuition, forcing a shift from writing instructions to designing *processes*. This is why the book is legendary—it doesn’t just teach programming; it transforms how you approach computation itself.  

This is just the beginning. More deep dives, more structured learning, and more insights to come.  