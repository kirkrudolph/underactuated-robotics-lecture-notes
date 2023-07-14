# Stocastic Dynamics

So far

$\dot{x}=f(x,u)$

Add in noise

$\dot{x}=f(x,u,w(t))$

where $w(t)$ is an output of a random process

For example
- process noise
- disturbances
- model uncertainty/errors/changes

Not
- sensor noise
- measurement noise

I know most of this. Only writing what's important.

Notable differences
- Notion of fixed point is gone
- Stability isn't the right question / language

## 19:00

Example: Cubic polynomial with Noise

## 29:00 

Example: The logistics map
- simplest example of chaos
    - random initial conditions
    - deterministic dynamics
    - Perrion-Frebinous
    - Liouville Equations
- solvable in closed form
- individual paths very hard to predict
- probablistic path easy to predict


>   
    Very hard to predict the future of an individual but it's very easy to predict the future of a population.
    
    That's a very compelling idea. Sometimes very complicated dynamics can be rendered easy by putting them into this probability space.

    Sometimes control can become easy (not always)

## 40:00

Example: Linear Gaussian

## 48:00

Example: Cubic Poly + Noise

- autonomous cars will eventually crash
- robots will eventually fall
- "meta stable"

## 1:00:00

Example: Rimless wheel on rough terrain

## 1:11:00

Did we invalidate everything? Do we need this always?
- 2 types of disturbances
    - impulse
    - continuous

>
    If the rate at which the disturbance effects you couples with the rate with which your dynamics converge, then the noise is important to the dynamics and they should be taken into account simultaneously.

    Time constant of stability
    Time constant of noise

    Are those close? Is it a "deterministic" with rare events or does noise impact your stability.

Modeling decisions do impact how you do control

- Optimal deterministic controller for compass gate does really badly on rough terrain.
- Optimal "mean time to failure" controller given dynamics of stocastic terrain, the controller is much stronger.
