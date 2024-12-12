---
name: Alexander King
topic: Backward and Forward Errors
title: Understanding Backward and Forward Errors in Numerical Computations
---

When solving problems numerically, as opposed to analytically, the generated solution is an approximation of the correct solution. The computational errors of the solution of a numerical problem can be separated into forward errors and backward errors.

Consider a function `y = f(x), where f: R → R` In this entire report, functions are assumed to exist only in the real numbers, unless otherwise stated. 

Here, `y` is the true output of the function for the given input `x`. We can also define the following. 
- `ŷ` (y-hat): The computed output of the function for the input `x`. This is the approximation of the exact answer. 
- `x̂` (x-hat): The input value that would produce the computed output `ŷ` in the function `f`. In other words, `ŷ = f(x̂)`

Now it is possible to define forward error and backward error. 


### Forward Error
Forward error refers to the error in the output, specifically the difference between the computed solution and the exact solution. Mathematically, it is given as:
```
Forward Error = ||ŷ - y||
```
This error directly measures how far the approximation is from the actual answer. 

### Backward Error
Backward error, on the other hand, measures how much the input data needs to be perturbed to make the computed solution an exact solution to the perturbed problem. 
```
Backward Error = ||x̂ - x||
```
Backward error measures the difference in the inputs, and does not accuratel reflect the error in the solution. However, backward error is usually easier to calculate, as will be shown in later sections. 

### Example: Solution for Square-Root Function
Consider a function for finding the square root of a positive number, that approximates √2 as 1.4. The forward error is `||ŷ - y|| = ||1.4 - 1.41421...|| ≈ 0.0142.           

To calculate the backward error, we solve for x̂ using the newly calculated ŷ. $1.4^2 = 1.96$, so the backward error is ||x̂ - x|| = ||1.96 - 2|| = 0.04. 

It was possible to calculate the forward error in this case because we know the value of √2 to many decimals of precision. If we do not have the exact value of y, which in most cases is not known, it is more difficult to calculate the forward error than backward error. 

### Example: Solving a Linear System
Consider solving $A\vec{x} = \vec{b}$ numerically, where A is an n by n matrix, b is an n by 1 vector of known values, and x is the solution vector. This case is confusing because x is the solution vector, and the differece in x and its approximation is the forward error. If $\vec{x}_0 = A^{-1}b$ is the exact solution, and $\vec{x}_{approx} is the computed solution, the forward error is:
$||x_0 - x_{approx}||$

The backward error is calculated as follows:
$b_{approx} = Ax
