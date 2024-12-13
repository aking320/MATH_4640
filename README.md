---
Name: Alexander King
Topic: Backward and Forward Errors
Title: Understanding Backward and Forward Errors in Numerical Computations
---
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
Backward error measures the difference in the inputs, and does not accuratel reflect the error in the solution. However, backward error is usually easier to calculate, as will be shown in later sections.

**Example: Solution for Square-Root Function**

Consider a function for finding the square root of a positive number, that approximates √2 as 1.4. The forward error is `|ŷ - y| = |1.4 - 1.41421...| ≈ 0.0142.           

To calculate the backward error, we solve for x̂ using the newly calculated ŷ. $1.4^2 = 1.96$, so the backward error is |x̂ - x| = |1.96 - 2| = 0.04. 

It was possible to calculate the forward error because we know the value of √2 to many decimals of precision. If we do not have the exact value of y, which in most cases is not known, it is more difficult to calculate the forward error than backward error. 

**Example: Solving a Linear System**

Consider solving $A\vec{x} = \vec{b}$ numerically, where A is an n by n matrix, b is an n by 1 vector of known values, and x is the solution vector. This case is confusing because x is the solution vector, and the differece in x and its approximation is the forward error. If $\vec{x_0}$ is the computed solution, and $\vec{x_{a}}$ is the approximate solution, the forward error calculated as follows:

Forward error = $|x_0 - x_{a}|$

The backward error is calculated by first calculating $b_a$, the approximate b vector. 

$\vec{b_{a}}$ = $A\vec{x_{a}}$ 

Backward error = $|\vec{b} - \vec{b_{a}}|$

The backward error here is much easier to calculate than the forward error and this is often the case. Here, to evaluate the forward error, we would have to compute the matrix inversion $A^{-1}$, while for the backward error only a matrix multiplication has to be done. 



### Part 2: Conditioning 
It is intuitive that is a solution has zero backward error it has zero forward error, and vice versa. If x and x̂ are equal, then the outputs of the function are also equal. The objective of these numerical problems is to minimize forward error, but we usually can only measure backward error. An important question to ask is how much can we expect the forward error to change when the backward error changes? 
This question motivates the concept of conditioning. We can define the following terms. 

 - A problem is *well-conditioned* or *insensitive* when a small backward error leads to small amounts of forward error.
 - A problem is *ill-conditioned* or *sensitive* when it is not well conditioned. So, small amount of backward error could mean large amounts of forward error.
   
To be able to tell when a problem is ill conditioned, we can define the *error magnification factor* as the relative forward error divided by the relative backward error for a given input and output (not over the entire range). The relative forward error is the forward error divided by the correct solution, and the relative backward error is the backward error divided by the input. 


Error magnification factor = $\frac{relative forward error}{relative backward error}$ = 
$\frac{|ŷ - y|}{y} / \frac{|x̂ - x|}{x}$ = $\frac{|f(x̂)-f(x)|}{f(x)} / \frac{|x̂ - x|}{x}$


Sometimes, this expression is called the condition number. In some cases, the condition number is described separately, as the limit as |x̂ - x| tends to zero. 

The *condition number* k = $\frac{|f'(x)|}{|f(x)|/|x|}$

In the previous example of f(x) = √x, 

k = $\frac{|f'(x)|}{|f(x)|/|x|}$ = $\frac{|0.5x^{-0.5}|}{|x^{0.5}|/|x|}$ = 0.5

So we can expect that the chance in input to the change in output is 1 to 2, which is not very significant. This problem is well conditioned. 






