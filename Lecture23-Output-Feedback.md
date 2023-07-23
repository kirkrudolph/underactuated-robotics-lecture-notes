# Output Feedback

Controllers are dynamical systems too.


DP (or other optimal policies)
- The optimal policy was always a "static" function (function of state).
- $u^*=\pi^*(x)$
- Full-state feedback

Estimate $x$ from $y$
- not necessary?
- may be a bad idea?

Why not "static output feedback"
$u=\pi(y)$

Linear case
- $\dot{x}=Ax+BU$
- $y=Cx$
- find $u=-Ky$

Static output feedback is NP hard
- Disconnected sets of solutions
- Harder than full state feedback
- Can be useful but no general solution that will always work.


## 20:00

Observer-based feedback
- Luenburger Observer
- Kalman Filter (dual of LQR)

#1 result in output feedback
- If LQG system, optimal thing is Y -> Kalman -> xhat -> LQR -> u
- "separation principle"

> 
    Only holds for linear problems! This is not justified in the general sense even though it is done in practice
    
    To use deterministic control and feed it your best estimate is not guarenteed to be optimal in any way. It's a heuristic. 

More generally,
- Y -> Optimal Bayes Filter -> $\hat P(x) -> Controlelr -> u$
- Must pass an entire estimate of distribution of possible states
- Controller must be designed to take in the entire distribution
- "Belief state planning" 

## 38:00

Example: Acrobot balancing from only joint positions

- Ecoder calibartion offsets
- Quatization
- Actuator Backlash
- Actuator Sticktion

## 52:00

Dynamical Controller

Can you search for A,B,C,D directly?
- Yes. Kinda. Convex representations for LQR
Does Gradient decent work.
- No. 

Linear Dyanmiscs
- State-Space Models
- ARX Models

Neural Nets for control
- LSTM (recurant networks)
- FIR models
