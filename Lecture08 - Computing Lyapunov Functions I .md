# Lecture 8 - Computing Lyapunov Functions I

- Gone through Optimal Control
    - Can be a hard problem to solve
    - unique solution
- [9:00] Lyapunov Function is an alternative
    - Simplify condition so it's an easier problem to solve.
    - many solutions
    - Not optimal but achieves "the goal"
    - Very robust
    - Often energy based
    - Totaly different experience than neural nets.
    - Tools based on convex optimization

## [18:00] Parameterize Lyapunov candidate

- Linear program with two constraints
- Can find a valid lyaponav function V(x) via sample based method. 
- Simple linear program.
- Evaluating function and derivative at many sample points. 
- Limitation: doesn't certify for all x. Only certifies at sample points.

[28:00] Example basis function for pendulum

[32:00] How to find for all x
- Square all the features of the basis function
- Now it's a convex problem instead of linear
- Proving stability for linear system the hard way

[53:00] Robust Stability
- "Common lyapnov function"
    - One function that verifies many systems

[1:01:00] Extend to non-linear systems
- Polynomial basis example
- Sums of squares optimization
- semi-definite programming
