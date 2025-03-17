---
layout: post
title: "SICP #Notes"
date: 2025-03-07
categories: reading
author: Remy
description: "SICP #10"
github: https://github.com/Rae699
comments: false
---


## Chapter I - Deeper Summary & Notes**  

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

### **Understanding Higher-Order and Lower-Order Functions**

A key insight from SICP is how to structure programs using higher-order functions (functions that take other functions as arguments) and lower-order functions (functions that do the actual computation). 
This abstraction allows for modular, reusable code that is both elegant and efficient.

A higher-order function is:
- a function that takes another function as an argument. In other words, it is a procedure that manipulates one or more procedures.
- It serves as a powerful abstraction. 

We'll create a higher-order function that applies a given operation to a range of numbers.

Let's say we want to sum or multiply numbers from a to b. We'll create a general higher-order function that takes:
	•	A function (operation) that defines what to do with each number.
	•	A starting number (a).
	•	An ending number (b).

#### Higher-Order Function: apply_operation
```
def apply_operation(operation, a, b):
    result = 1  # Start with 1 for multiplication
    for i in range(a, b + 1):
        result = operation(result, i)
    return result
```

#### The Lower-Order Functions

The lower-order function does the actual computation.
Hence, let's define a lower-order function that specify what operation to perform.
```
def add(x, y):
    return x + y

def multiply(x, y):
    return x * y
```

#### Calling the higher-order f specifying which lower-order f to use

Now we can call apply_operation with different lower-order functions:
```
# Sum of numbers from 1 to 5
sum_result = apply_operation(add, 1, 5)  # 1 + 2 + 3 + 4 + 5 = 15
print("Sum:", sum_result)

# Product of numbers from 1 to 5 (Factorial of 5)
product_result = apply_operation(multiply, 1, 5)  # 1 * 2 * 3 * 4 * 5 = 120
print("Product:", product_result)
```

```
Finale output will be:
Sum: 15
Product: 120
```

#### What's happening?

It is simple:
	1.	We call the higher-order function: apply_operation(add, 1, 5).
	•	It loops through 1 to 5 and applies add(x, y), accumulating the sum.
	2.	We call apply_operation(multiply, 1, 5).
	•	It loops through 1 to 5 and applies multiply(x, y), accumulating the product.

It is important because:
✅ Code Reusability → We can use apply_operation for many different operations.
✅ Clear Abstraction → Separates "what to do" (add, multiply) from "how to iterate" (apply_operation).
✅ Scalability → We can easily add new operations without rewriting the logic.


#### Going a little bit further: General Logic of product Function

We define a general function, product, that computes the product of values between a lower bound a and an upper bound b, applying a function f to each value. 
It also takes a step function next_func to determine how the sequence progresses.

- f is a placeholder function that represents the transformation applied to each value.
- a is the starting (lower bound) value.
- next_func is a function that defines how we move to the next step, often maintaining an invariant in an iterative process.
- b is the upper bound (stopping condition).

Thus, the end-user calls a higher-order function, which in turn invokes a lower-order function to perform the actual computation.

```
# Recursive version
def product_recursive(f, a, next_func, b):
    if a > b:
        return 1  # Base case: return multiplicative identity
    return f(a) * product_recursive(f, next_func(a), next_func, b)

# Iterative version (preferred for efficiency)
def product_iterative(f, a, next_func, b):
    result = 1
    while a <= b:
        result *= f(a)
        a = next_func(a)
    return result
```

#### Using product to Compute Factorial
A lower-order function implements a specific computation using product. To compute factorial, we set f(x) = x and next_func(x) = x + 1:
```
# Recursive factorial
def factorial_recursive(n):
    return product_recursive(lambda x: x, 1, lambda x: x + 1, n)

# Iterative factorial (better for large numbers)
def factorial_iterative(n):
    return product_iterative(lambda x: x, 1, lambda x: x + 1, n)
```

#### Execution Flow When Calling These Functions

The user calls factorial_iterative(5):
- This invokes product_iterative(lambda x: x, 1, lambda x: x + 1, 5).
- product_iterative loops through numbers 1 to 5, multiplying them together.
- The final result 120 is returned.

This structured approach ensures that we can reuse product for different computations, improving code clarity and efficiency—one of the key lessons from SICP. 🚀


### **Finding Fixed Points and Newton's Method**

One of the most elegant applications of higher-order functions is finding fixed points of functions. A fixed point is a value where f(x) = x. This concept is fundamental in mathematics and computer science, appearing in everything from recursive algorithms to numerical methods.

#### **The Fixed-Point Abstraction**

The beauty of SICP's approach is how it abstracts the process of finding fixed points into a general procedure:

```scheme
(define tolerance 0.00001)

(define (fixed-point f first-guess)
  (define (close-enough? v1 v2)
    (< (abs (- v1 v2)) tolerance))
  (define (try guess)
    (let ((next (f guess)))
      (if (close-enough? guess next)
          next
          (try next))))
  (try first-guess))
```

This higher-order function takes:
- A function `f` whose fixed point we want to find
- An initial guess to start the iteration

The process is remarkably simple:
1. Apply `f` to our current guess to get a new value
2. If the new value is close enough to our guess, we've found the fixed point
3. Otherwise, recursively try again with the new value as our guess

#### **Practical Application: Computing Square Roots**

We can use this fixed-point finder to compute square roots. The square root of x is a value y where y² = x, which means y = x/y.

```scheme
(define (sqrt x)
  (fixed-point (lambda (y) (/ x y)) 1.0))
```

However, this naive approach oscillates between values without converging. The key insight is to use **average damping** to stabilize the process:

```scheme
(define (sqrt x)
  (fixed-point (lambda (y) (average y (/ x y))) 1.0))
```

By averaging the current guess with the next computed value, we create a convergent sequence that efficiently finds the square root.

#### **Newton's Method: A Powerful Generalization**

Newton's method is a powerful technique for finding roots of functions (values where f(x) = 0). The method uses the derivative of a function to iteratively improve approximations:

```scheme
(define (newton-transform g)
  (lambda (x) (- x (/ (g x) ((deriv g) x)))))

(define (newton-method g guess)
  (fixed-point (newton-transform g) guess))
```

This elegant implementation shows how higher-order functions allow us to express complex mathematical methods concisely:
- `newton-transform` takes a function and returns a new function that performs one step of Newton's method
- `newton-method` uses our fixed-point finder with this transformed function

We can now redefine our square root function using Newton's method:

```scheme
(define (sqrt x)
  (newton-method (lambda (y) (- (square y) x)) 1.0))
```

#### **Key Insights**

The power of these abstractions lies in their composability:
- We defined a general fixed-point finder
- We created transformations that modify functions (average damping, Newton's transform)
- We composed these to create efficient numerical methods

This approach demonstrates how functional programming enables us to:
1. **Express mathematical concepts directly** in code
2. **Build layers of abstraction** that hide implementation details
3. **Compose simple functions** to create powerful algorithms

### **Abstractions and First-Class Procedures**

The culmination of SICP's first chapter reveals how procedures as first-class objects enable powerful abstractions. By treating procedures like any other data, we can create general methods that transform, combine, and apply functions in flexible ways.

#### **Procedures as Returned Values**

One of the most powerful patterns is creating procedures that return other procedures:

```scheme
(define (average-damp f)
  (lambda (x) (average x (f x))))

(define (sqrt x)
  (fixed-point (average-damp (lambda (y) (/ x y))) 1.0))
```

This approach allows us to:
- Create reusable transformations that modify how functions behave
- Apply these transformations in different contexts
- Build complex behaviors from simple components

#### **Abstracting Common Patterns**

The real power comes when we abstract common patterns into higher-order procedures:

```scheme
(define (fixed-point-of-transform g transform guess)
  (fixed-point (transform g) guess))

(define (sqrt x)
  (fixed-point-of-transform 
    (lambda (y) (/ x y)) average-damp 1.0))

(define (sqrt x)
  (fixed-point-of-transform
    (lambda (y) (- (square y) x)) newton-transform 1.0))
```

Notice how both implementations of `sqrt` now follow the same pattern, differing only in the function being transformed and the transformation applied.

#### **The Essence of Abstraction**

This approach to programming embodies the essence of abstraction:
1. **Identify common patterns** in different procedures
2. **Extract these patterns** into higher-order procedures
3. **Express specific cases** as instances of these general patterns

The result is code that is:
- More **concise** (fewer lines of code)
- More **expressive** (captures intent clearly)
- More **maintainable** (changes can be made at the appropriate level of abstraction)
- More **reusable** (general patterns can be applied in new contexts)

#### **Practical Takeaways**

These concepts translate directly to modern Python programming:
- Python's `map()`, `filter()`, and `functools.reduce()` are direct implementations of these functional programming ideas
- Python decorators are higher-order functions that transform other functions
- Libraries like `itertools` and `functools` build on these functional programming foundations
- Frameworks like Django and FastAPI use higher-order functions for middleware and request handling

By understanding these fundamental abstractions, we gain the ability to:
- **Recognize patterns** across seemingly different problems
- **Create elegant solutions** using Python's functional programming features
- **Build powerful abstractions** that make complex tasks simple
- **Write more maintainable code** by separating concerns through function composition

This is the true power of functional programming in Python—not just using functions as organizational units, but as powerful tools for abstraction and composition.


---

## **Closing Thoughts**  

SICP is not about learning to code. It's about learning to *think*.  

Each chapter rewires intuition, forcing a shift from writing instructions to designing *processes*. This is why the book is legendary—it doesn't just teach programming; it transforms how you approach computation itself.  

This is just the beginning. More deep dives, more structured learning, and more insights to come.  