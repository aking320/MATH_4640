---
Name: Alexander King
Topic: Backward and Forward Errors
Title: Understanding Backward and Forward Errors in Numerical Computations
---

When solving problems numerically, as opposed to analytically, the generated solution is an approximation of the correct solution. The computational errors of the solution of a numerical problem can be separated into two types, called forward errors and backward errors.

### Forward Error
Forward error refers to the error in the output, specifically the difference between the computed solution and the exact solution. Mathematically, it is expressed as:
`Forward Error = ||x̂ - x||`

where \\( \\hat{x} \\) is the computed solution, and \\( x \\) is the true solution. This error directly measures how far the approximation is from the actual answer. However, forward error alone does not tell us how the algorithm performs with respect to the initial input data.

### Backward Error
Backward error, on the other hand, measures how much the input data needs to be perturbed to make the computed solution \\( \\hat{x} \\) an exact solution to the perturbed problem. For a linear system \\( Ax = b \\), the backward error is the smallest perturbation \\( \\Delta A \\) and/or \\( \\Delta b \\) such that:
### Forward Error

The forward error is expressed as:

\\[
\text{Forward Error} = \\|\\hat{x} - x\\|,
\\]



This metric is crucial for assessing the robustness of numerical algorithms, as it determines whether the computed solution could arise from a slightly altered input problem. In practice, a small backward error indicates that the algorithm is stable, even if the forward error is large in the presence of ill-conditioned problems.

### Interplay Between Forward and Backward Errors
The relationship between forward and backward errors is governed by the conditioning of the problem being solved. The condition number of a problem indicates how sensitive the solution is to small changes in the input data. For a well-conditioned problem, a small backward error typically implies a small forward error. However, in ill-conditioned problems, even a small backward error can result in a large forward error.

### Example: Solving a Linear System
Consider solving \\( Ax = b \\) numerically, where \\( A \\) is a matrix, \\( b \\) is a vector of known values, and \\( x \\) is the solution vector. If \\( \\hat{x} \\) is the computed solution, the forward error is:
\\[
\\| \\hat{x} - x \\|,
\\]
and the backward error involves finding \\( \\Delta A \\) and \\( \\Delta b \\) such that:
\\[
(A + \\Delta A) \\hat{x} = b + \\Delta b.
\\]
The relative magnitude of these errors depends on both the algorithm used and the condition number of \\( A \\).
