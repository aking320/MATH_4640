---
Name: Alexander King
Topic: Backward and Forward Errors
Title: Understanding Backward and Forward Errors in Numerical Computations
---

[Part 1: Definitions](#part-1-definitions)

[Part 2: Introductory Examples](#part-2-introductory-examples)



### Part 1: Definitions
When solving problems numerically, as opposed to analytically, the generated solution is an approximation of the correct solution. The computational errors of the solution of a numerical problem can be separated into forward errors and backward errors. 

Consider a function `y = f(x), where f: R → R` In this entire report, functions are assumed to exist only in the real numbers, unless otherwise stated. 

Here, `y` is the true output of the function for the given input `x`. We can also define the following. 
- `ŷ` (y-hat): The computed output of the function for the input `x`. This is the approximation of the exact answer. 
- `x̂` (x-hat): The input value that would produce the computed output `ŷ` in the function `f`. In other words, `ŷ = f(x̂)`

Now it is possible to define forward error and backward error. 



**Forward Error**

Forward error refers to the error in the output, specifically the difference between the computed solution and the exact solution. Mathematically, it is given as:
```
Forward Error = |ŷ - y|
```
This error directly measures how far the approximation is from the actual answer. 

**Backward Error**

Backward error, on the other hand, measures how much the input data needs to be perturbed to make the computed solution an exact solution to the perturbed problem. 
```
Backward Error = |x̂ - x|
```
Backward error measures the difference in the inputs, and does not accurately reflect the error in the solution. However, backward error is usually easier to calculate, as will be shown in later sections. $^{[1, 2]}$

### Part 2: Introductory Examples

**Example: Solution for Square-Root Function**

Consider a function for finding the square root of a positive number, that approximates √2 as 1.4. The forward error is |ŷ - y| = |1.4 - 1.41421...| ≈ 0.0142.           

To calculate the backward error, we solve for x̂ using the newly calculated ŷ. $1.4^2 = 1.96$, so the backward error is |x̂ - x| = |1.96 - 2| = 0.04. 

It was possible to calculate the forward error because we know the value of √2 to many decimals of precision. If we do not have the exact value of y, which in most cases is not known, it is more difficult to calculate the forward error than backward error. 

**Example: Solving a Linear System**

Consider solving $A\vec{x} = \vec{b}$ numerically, where A is an n by n matrix, b is an n by 1 vector of known values, and x is the solution vector. This case is confusing because x is the solution vector, and the differece in x and its approximation is the forward error. If $\vec{x_0}$ is the computed solution, and $\vec{x_{a}}$ is the approximate solution, the forward error calculated as follows:

Forward error = $|x_0 - x_{a}|$

The backward error is calculated by first calculating $b_a$, the approximate b vector. 

$\vec{b_{a}}$ = $A\vec{x_{a}}$ 

Backward error = $|\vec{b} - \vec{b_{a}}|$

The backward error here is much easier to calculate than the forward error and this is often the case. Here, to evaluate the forward error, we would have to compute the matrix inversion $A^{-1}$, while for the backward error only a matrix multiplication has to be done. This is an example of "backward error analysis" - measuring error in data rather than in results. 

The developer of backward error analysis is James Hardy Wilkinson. Wilkinson was one of the first large contributers to the field of numerical analysis. He studied at the Trinity College in Cambrige, graduating in 1939 with his degree in pure mathematics. After serving in the british military, he worked for the UK National Physical Laboratory, where he worked with Alan Turing on developing some of the the earliest computers. The concept of backward error analysis was introduced in his book "Rounding Errors in Algebraic Processes" (1960). $^{[6]}$


### Part 3: Conditioning 
It is intuitive that is a solution has zero backward error it has zero forward error, and vice versa. If x and x̂ are equal, then the outputs of the function are also equal. The objective of these numerical problems is to minimize forward error, but we usually can only measure backward error. An important question to ask is how much can we expect the forward error to change when the backward error changes? 
This question motivates the concept of conditioning. We can define the following terms. 

 - A problem is *well-conditioned* or *insensitive* when a small backward error leads to small amounts of forward error.
 - A problem is *ill-conditioned* or *sensitive* when it is not well conditioned. So, small amount of backward error could mean large amounts of forward error.
   
To be able to tell when a problem is ill conditioned, we can define the *error magnification factor* as the relative forward error divided by the relative backward error for a given input and output (not over the entire range). The relative forward error is the forward error divided by the correct solution, and the relative backward error is the backward error divided by the input. 


Error magnification factor = $\frac{relative forward error}{relative backward error}$ = 
$\frac{|ŷ - y|}{y} / \frac{|x̂ - x|}{x}$ = $\frac{|f(x̂)-f(x)|}{f(x)} / \frac{|x̂ - x|}{x}$

In some texts, this expression is called the condition number. $^{[2,3]}$ In some texts, the condition number is described separately, as the limit as |x̂ - x| tends to zero. $^{[1,4]}$ This can be evaluated as the following: 

The *condition number* k = $\frac{|f'(x)|}{|f(x)|/|x|}$


**Example: Condition Number of a Square Root Function**

In the previous example of f(x) = √x, 

k = $\frac{|f'(x)|}{|f(x)|/|x|}$ = $\frac{|0.5x^{-0.5}|}{|x^{0.5}|/|x|}$ = 0.5

So we can expect that the chance in input to the change in output is 2 to 1, which is not very significant. This problem is well conditioned. It then becomes possible to estimate the forward error in a result by onl doing backward error analysis, if the condition number can be found. 

It is also possible to show that the condition number for a linear system is the coefficient matrix times its inverse. This is often the way it is calculated. 
Suppose we wish to compute the linear system y = Ax, but we instead compute a small error, and the computed result is $ŷ = (A+E)x$. 

The absolute forward error is:

$\frac{||ŷ - y||}{||y||}$ = $\frac{||(A+E)x - Ax||}{||y||}$ = $\frac{||Ex||}{||y||}$

Assuming that A is invertable and we are using consistent norms, then we have

$||Ex|| = ||EA^{-1}y||$  ≤ $||E||$ $*$ $||A^{-1}||$ * $||y||$

This gives us 

$\frac{||ŷ - y||}{||y||}   ≤   ||A||*||A^{-1}|| * \frac{||E||}{||A||}  $

The important thing to note from this derivation is that the condition number k is the coefficient matrix times its inverse. $^{[5]}$ This will be important 

### Part 4: Edge Cases

**Example: Equation with multiple roots**

Consider the function $f(x) = x^2-2x+1 = (x-1)^2$, and suppose we wish to find its roots. 
A small change in the coefficients leads to a large change in the roots. Consider the following similar function. 

$x^2-2x+0.9999 = (x-0.99)(x-1.01)$

Even though the function changed by 0.0001, the roots changed by 0.01. 
When we try to calculate the condition number, we find that 
The condition number of this problem is undefined, some texts would say infinite, at x=1, since
 f(1) = f'(1) = 0. 

 The point being made with the previous example is that the condition number is not always calculable, and can be undefined for specific roots of a function. When k is infinite, then the problem is called "ill posed". 

 ### Part 5: Example Code

Pseudocode for a function that takes in inputs into a function, computes the function, and returns the backward error multiplied by the condition number as an estimate for forward error is shown here.


```
Input: Matrix A, Vector b

x_computed = solve(A,b)

residual = b - multiply(A, x_computed)

backward error = norm(residual) / norm(b)

cond_A = ||A|| * ||A^-1||                                                   ## condition number

estimate of forward error = cond_A * backward error

output: backward error, cond_A, forward error 


```


### References
1. Notes on error analysis. (n.d.). http://people.whitman.edu/~hundledr/courses/M467F06/ConvAndError2.pdf
2. Numerics and error analysis. (n.d.-b). https://graphics.stanford.edu/courses/cs205a-13-fall/assets/notes/chapter1.pdf
3. Verschelde, J. (2022, August 29). Numerical Conditioning. http://homepages.math.uic.edu/~jan/mcs471/conditioning.pdf
4. Driscoll, T. (2023). Problems and conditioning. 1.2. Problems and conditioning - Fundamentals of Numerical Computation. https://tobydriscoll.net/fnc-julia/intro/conditioning.html
5. Bindel. (2015). Error measures and norms introducing the condition number. https://www.cs.cornell.edu/~bindel/class/cs4220-s15/lec/2015-02-04-notes.pdf
6. Wilkinson, J. H. W. (2023). Rounding errors in algebraic processes. Society for Industrial and Applied Mathematics. 




