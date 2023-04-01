# Lecture 11 - Trajectory Optimization

## Themes of Class
    
    We should be doing optimization to solve the problems but the dynamics should matter. Optimizing a dynamic system isn't the same as general optimization because we know more about it. There's "structure in the equations" that we should exploit. Should make optimization scale, require less compute, be more reliable, ect.

## High Level Review

Dynamic Programming 
- Value Iteration
    - Discritized meshes good for small systems 
        - hasn't changed in 20 years
        - ~5 state variables
        - exponentially expensive
    - Neural approaches can extend but with fewer guarentees
- LQR (special case)
    - Arbitrary high dimensions
    - Requires linearization of dynamics
Lyaponov (relaxed optimal definition)
- Sums of Squares
    - Why SoS? Equation of motion shows up in optimization in a deep, integrated way.

**All of these methods are trying to solve for all x (full state space)**
- Very hard (maybe artifictially hard) problem
- Instead, could we solve for only the important and relative states

## Trajectory Optimization

Trajectory optimization is a direct attack against creating a controller that works for all states. Instead, we switch the problem to solve a smaller problem of "finding a controller that works for a particular `x[0]`". One trajectory that determines what the controll action should be for a finite amount of time.

    We try to handle very high demensional problems by solving a more narrow problem which scales only with parameterization in time, not state.

This is what Atlas uses at Boston Dynamics. It does scale and work in practice.

## [ 9:30 ] Story of "Bird Landing on Pirtch"

- Angle of Attack (deep stall)
- Birds have "Mad Stop"
- Controls problem or hardware problem?
- Dimensional Analysis (compare on fair scale)
- Experiment Design
- Dynamic Model
- Simulation

1. Take trajectory that's pre-computed
2. Stabalize trajectory (local LQR or ther means)
3. Lyaponav functions around trajectory that certifies a range of ic to range of fc
4. Repeat for multiple "funnels" of ic

## [29:00] Problem Definition

For some system $\dot{x} = f(x,u)$,

Find $u(.)$ control action that minimizes cost from $t_0$ to $t_f$ subject to system dyanmics, initial condition, and additional constraints (actuator limits, state limits, etc.).

$
min_{u(.)} \int_{t_0}^{t_f}l(x,u)dt \\
s.t.                                \\ 
\dot{x}=f(x,u)                      \\
x(0) = x_0                          \\
+additional constraints
$

Only difference from earlier problems is,
1. Given initial condition
2. Instead of searching for control policy, we're searching over an open loop trajectory $u(t)$

Note: if $f(x,u)$ has modeling erros and/or you predict far into the future, this is where feedback will save the day

## [35:00] Linear discrete-time case