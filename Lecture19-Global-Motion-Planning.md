# Lecture 19: Gloabal Motion Planning

From last time: If you have enough degrees of freedom, some of the dynamics become easier.
- Abstract dynamics into dynamics of CoM and angular momentum

With lots of joints, we add the extra complexity of all the motion planning.
- Collision free trajectories.
- Trying to solve tricky kinematic puzzles.

Inbetween problems.
- Quadcopter navigating forest of trees.

## [6:30] Motion Planning as Search
- Dynamics + complex kinematics (many links / obstacles)
- UAV planning at high speeds in dense obstacles

Background Kinematic Motion Planning
- **Great book. Planning Algorithms by Steve Lavalle**
- For a start and end goal with obstacles in between.
- We've already solved this (grid world) using DP value iteration
    - Tops out at 5-6 dimensions
    - Not clearly a great solution because discretized space my miss a good solution.
- Alternative approach: Sampling
- Probabilistic Roadmap (PRM)
    - draw a random sample
    - reject if in collision
    - find nearest neighbors
    - add edges if collision free
    - Virtues:
        - Multi-qurry algorithm (reuse same map for many different goals)
        - Probabilistically complete
            - A planner is "complete" iff it returns a path whenever it exists or says "no path"
            - Probabilistically complete if a number of samples -> inf, prob of finding an existing path -> 1.
        - Scalling up to ~10 dimensions
        - number of samples in solution is unspecified
    - What if we have dynamics?
        - Undirected graph -> directed graph
        - Distance metric. x1-x2 small doesn't mean reachable. Eulidean distance isn't right.
- Rapidly-exploring Random Trees (RRT)
    - Once dynamics and reachibility and constrains start to dominate PRM doesn't work well
    - Start with a sample at the start state
    1. Pick a point at random (in state space)
    2. Find closest point in the existing tree
    3. Extend from closest point towards the sample s.t. dynamic constraints are met
    - Virtues:
        - Probabilistically complete
        - Voronous Bias
            - Probability of extending a node is proportional to the volume of the Voronous area
        - Works in high dimensions.
        - Captures dynamics
        - To solve underactuated systems need stronger heurisitics
            - 3 steps of the algorithm:
            1. Choose $x_{random}$ <- better sampling distribution. Target useful dynamic locations
            2. Find closest oint <- better distance metrics
            3. Chose u to extend <- better control

## [53:00] Distance metrics for dynamic systems

## [1:08:00] Sampling Distributions for dynamic systems

## [1:13:00] Basic RRT vs Reachability-Guided RRT

Fuzzy eyeball vs smooth eyeball

## [1:17:00] Better Control (use traj opt. as inner loop for RRT to extend)