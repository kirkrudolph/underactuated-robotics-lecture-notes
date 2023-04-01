# Lecture 10 - Lyaponov Sum of Squares
- Co-design the controller and the Lyapnov equation that proves it's stable
- Polynomial is a good basis
- Convex / Bi-linear in desicion variables
    - Can have local minimum
    - Recursively feasable 
        - once a Lyaponov / controller is found, it will only get better.
    - monotomic improvement

[47:00] Powerful recipe
- linearize non-linear dynamics
- Solve LQR
- Compute region of attraction using Sum-of-Squares with $V=x^TSx$ as Lyopnav
- Start alterations to search for new K, V to prove bigger region of attraction
- SOS and Value Iteration is offline
    - Output is a fast and easy to use controller

$u = Kx+\alpha{x^2}+\beta x^3 +...$

Finds a controller that takes into account non-lineararities

[1:00:00] Sums of squares dynamic programming