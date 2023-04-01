# Dynamic Programming II

- Discrete states -> continuous states
- Discrete actions -> continuous actions
- Discrete time -> continuous time
- Hamilton-Jacobi Bellmen (HJB)
- Linear Quadratic Regulator

Motivations for continuous time:
- Accuracy. Discrete is systematically wrong. Discretization errors are hard to bound and add up a lot as you integrate across the state-space.
- Scalling. Continuous time can handle higher order systems for some classes of problems.

$s[n+1]=f_d(s[n],a[n])$
- $l_d(s,a)$ - one step cost function

$min_{a[*]} \Sigma_{n=0}^{\infty}l(s[n],a[n])$

$J^*(s_i) = min_a[l(s_i,a)+J^*(f_d(s,a))]$ 

$\pi^*(s_i)=argmin_aJ^*(s_i)$

--------------

$\dot{x}(t)=f_c(x(t),u(t))$

$l_c(x,u)$

$min_{u(*)} \int_0^{\infty}dt l_c(x,u)$


$0=min_u[l_c(x,u)+\frac{\partial{J^*}}{\partial x}f_c(x,u)]$ 

- (HJB)
- partial differential equation of J
- "if walking along optimal policy, J must decrease at the rate the cost is accumulating"

$\pi^*(x)=armin_u$

[10:30] Derivation

$x[n+1] \approx x[n] + \Delta tf_c(x[n],u[n])$

$...$

[25:00] Example: Double integrator with quadratic cost

$\ddot q=u$

$l_c(q,\dot q, u) = q^2 +\dot q^2+u^2$

$x = [q,\dot q]$

$u^*=-q-\sqrt{3}\dot q$

$J^*=\sqrt{3}q^2+2q\dot q+\sqrt{3}\dot q^2$

... Lots of partial diffy q that I barely remember

[43:00] LQR Derivation
----------------------

Dynamics: $\dot{x}=Ax+Bu$

Cost: 
$l_c(x,u)=x^TQx+u^tRu$

where
- $Q=Q^T>=0$
- $R=R^T>0$

then, lets assume the cost to go ($J^*$) will take the form

$J^*(x)=x^TSx$

Turn the crank,

$\frac{\partial J}{\partial x} = 2x^TS$

$0 = min_u[x^TQx+u^TRu+\frac{\partial J}{\partial x}(Ax+Bu)]$

$0 = min_u[x^TQx+u^TRu+2x^TS(Ax+Bu)]$

$0 = min_u[x^TQx+u^TRu+2x^TSAx+2x^TSBu)]$

There is a quadratic and linear term for $u$ 
- i.e. take derivative and set = 0 to find minimum $\frac{\partial }{\partial u}$

$0 =2u^TR+2x^TSB$

$u^TR+x^TSB = 0$

$u^T =-x^TSBR^{-1}$

$u^*=-R^{-1}B^{T}Sx=-Kx$

- $S$ is "Get down hill as fast as poosible" (i.e. $-\frac{\partial J}{\partial x}$)
- $B$ "modifies $S$ in the direction that's possible to flow"
- $R$ is "not all actuation is equal"

But how do you find $S$ that fit's the relationship between $J^*$ and $u^*$? Plug $u^*$ back in.

$0 = x^TQx+x^TBSR^{-1}RR^{-1}B^TSx+2x^TSAx-2x^TSBR^{-1}B^TSx$

$0 = x^TQx+x^TBSR^{-1}B^TSx+2x^TSAx-2x^TSBR^{-1}B^TSx$

...

$0= x^T[Q-SBR^{-1}B^TS+SA+A^TS]x$

$0= Q-SBR^{-1}B^TS+SA+A^TS$ 

This is the `Continuous Algerbraic Ricatti Equation`
- S = CARE(A,B,Q,R)
- Quadradic in S
- Numerical algorithm that converges on S (Almost a closed form solution)
- [K,S] = lqr(A,B,Q,R)

**Balancing control used on balancing robots (like atlas) is only a slight generalization of lqr that deals with when you're in contact vs not in contact.**

I'm curious about the "in contact vs not in contact"

[1:05:00] Continuous Actions (more general than LQR)

If I have `Control Afine Dynamics`

$\dot{x}=f_1(x)+f_2(x)u$

and am convex in $u$,

$l_c(x,u) = l_1(x) +u^TRu$

(i.e. I can have very complicated dynamics and cost as long as my preference of actuation is simple)

If you give a cost to go function (even an estimate in the middle of Value Iteration), the same equations apply:

$ 0 = min_u[l_1(x)+u^TRu+\frac{\partial J}{\partial x}[f_1(x)+f_2(x)u]$


"Still take derivative with respect to u and the same methods work. It's a complicated function in x but still simple in u. In the continuous domain, you can solve $min_u()$ away to make an elegant solution. For example, if you have limits on $u$, this becomes an optimization problem. This is particular to continuous time problem formulations. Normaly if people have continuous action spaces, they turn to `actor-critic` algorithm because $min_u$ is a hard problem that Q-learning struggles to (but can) solve for $u$ in an arbitrary setting. But if you know the model (an assumption) given just a cost to go guess, the $min_u$ can be taken analyticaly (don't have to make a hard search over u). That is lost in discrete time. Even with afine dynamics, in discrete time $u[n]$ gets shuved through $J^*$ (most likely a DNN) "

[1:12:00] Continuous States
---------------------------

Cost to go on a discrete state space is easy. It's a list of numbers (one $J^*$ for every state). In continuous time, $J^*$ is a function. The algorithm necessary to implement $J^*$ changes; we need function aproximation (simple analytical methods vs DNN that can generalize extremely well). 

