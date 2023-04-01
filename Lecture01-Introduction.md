# Underactuated Robotics Notes

[Spring 2022](https://www.youtube.com/watch?v=PRaSlUA78gQ&list=PLkx8KyIQkMfXyKku6DstXjD9xU93ptDyc&index=29)

## Lecture 1: 
Non-linear dynamics
Dimensionless coordinates?
Conqury Map?

---> Agent / Policy / Controller ---|
|                                   |
--------Enviornment / Plant <--------


x. = f(x,u)
y = g(x)
x is a state vector
u is a control input vector
f is a vector-value function

        ---------
u ----->| Plant |-----> y
        ---------


What makes control hard? (i.e. discision making)
- GO
- Atlis Backflip

Stability
Dim(x) is large
Stocastic
Observability
Complicated interactions
Delayed Reward / Long term dynamics
Underactuated

Mechanical is second order in nature, "more" structure in second order even if you can write it in first order

q - vector of "generalized positions"
q. - velocities

mechanical systems (F=ma) (Control affine form)
q.. = f1(q,q.)+f2(q,q.)u

Fully actuated iff f2 is full row rank
Under actuated iff rank(f2) < dim(q)

u is a vector
q, q., q.. are vectors of same length (this doesn't hold for all cases like quaternions)
f2 is a matrix (size qxu)

Feeback Linearization
---------------------
Let's prove fully actuated problems are easy.

q.. = f1(q,q.)+f2(q,q.)u

assume f1 and f2 are known

given q..* (desired acceleration)

u = P(q,q.) (control policy pi that we get to choose)
u = f2^-1(q,q.)[q..*-f1(q,q.)]
This control policy is a valid controller because f2 is invertable when u is full row rank

Closed loop dynamis q.. = q..*

This system is now a double integrator:
- q.. = u
- Trivial linear system
- Very well defined control laws even in there are long term objectives

Goal of the course
"How to do good control when f is complicated and you can't erase it."
- Backflips
- UAV moving fast
- "Any time the dynamics overcome your ability to do control"
Bring together
- Nonlinear dynamics
- Optimization
- Control
- Machine Learning
Rigorous thinking about "model systems"
Algorithm toolkit for more complex systems


The Leg Laboritory [32:00] (worth a rewatch because it's cool)
- Robots started by moving very slow, getting COG over the foot, stepping very slow.
- Started by canceling dynamics
- Harder to control, less efficient, huge penelty for fighting natural dynamics, Large control authority
- Then, leg laboritory started taking advantage of the system dynamics.
- Robots throw themselves through the air and stabalize

Passive Dynamic Walking
- Robots that walk without actuation
- Beautiful way to think about control
- Atlis Parcor (joints are ridgid )

Other factors that can prevent q.. = u feedback equivalence
- Actuator limits (Input limits)
- State constraints
    - Joint limits
    - Colision avoidance
- Model Uncertainty, etc.

Equations of motion of our robots (double pedulum) [48:00]
- Lagrangian Method (L=T-U)
- Generalize form of dynamics (M(q.)q..+C(q,q.) = T_g(q)) + Bu
- M(q.)     - Generalized Mass/Inertia Matrix
- C(q,q.)   - Coriolis Terms
- T_g(q)    - Gravity Terms
- B         - Actuation Matrix
- u         - Control Inputs

"If you had more funding would you work on fully actuated robots" lol
- Walking is fundamentaly underactuated.
- Can't fall faster than gravity (without a jetpack). 

- Nonlinear dynamics
- Optimization and optimal control
- Control Theory vs Machine Learning aproaches
- Simple Model Systems
    - Acrobots
    - Carpoles
    - Quadroder
- Motion Planning
- Limit Cycles
- Control Through Contact
- Stocastic + Robust + Sys ID + Model Free
- Toolbox for complicated robots


