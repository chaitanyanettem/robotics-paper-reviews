## Reciprocal n-Body Collision Avoidance

Collision Avoidance Problem - multiple robots need to avoid collisions with each other while moving in a common workspace.

Paper presents a **formal** approach. Formal methods are techniques used to model complex systems as mathematical entities. By building a mathematically rigorous model of a complex system, it is possible to verify the system's properties in a more thorough fashion than empirical testing. [1]

### Problem Formulation

* Each robot acts fully independently
* no communication between robots

There are 'N' robots sharing an environment. Each robot A has:

External State (observable by other robots continuously)

* current position P
* current velocity V
* radius R

Each robot also has Internal state:

* maximum speed V-max
* preferred velocity V-pref (this is velocity robot assumes had no other robots been on its way)

ques: if there's no communication b/w robots, how do they observe other guy's external state?

Give these states, Task for each robot 'A' is to:

* Independently (and simultaneously) select a new velocity V-new for itself such that
**all** robots are **guaranteed** to be collision free for atleast the next delta time (t), which is preset and fixed. During this time t, each robot continue to move at their new velocity.

* the new velocity V-new should be **as close as possible** to their preferred velocity.

* Again, robots are now allowed to communicate with each other, and can only
observe each others' external state.

**BUT!!!** Each robot may assume that the other robots use the same strategy as itself to select the new velocity.

The authors call this reciprocal n-body collision avoidance.

### 2 Body Collision Avoidance

Authors consider 2 robots A and B, with their internal and external state. And derive
(with plenty of math and physics) and optimal reciprocal collision avoidance algorithm.

Reciprocal - the two agents are reciprocating to each other their external state (but not
  communicating!!), and then choosing their new velocities for the next time internal t.

The authors note that this problem cannot be solved using central coordinate (in the way it has been formulated), because each robot does not share its internal state with anybody.

```
But what's stopping them from changing the formulation a little bit?
```

Authors claim to present a "sufficient" condition for each robot to select a velocity that is collision free for the present time t.
And then they show how to use this principle in a continuous cycle for multi-robot navigation.

```
ques: where are all these robots navigating to? All robots have the same destination?
```

### n-Body

Authors then generalize this to n-bodies.

This is the oldest trick in the book.

```
For robot in Robots:
  Instead of looking at only 1 other robot, sense
  ***every other robot's*** external state.
  # Remember, every robot uses the same strategy (so it's the same code running on each robot)
  # So it's important to choose this strategy. This is the "juice" of the algorithm.
  Use a bad-ass Linear Programming approach to select the new velocity
  Apply this new velocity, and move with this velocity for the time interval t.
```

Note that the iterations of the above loop are taking place in parallel on every robot.

```
Ques - clock skew? time drift? authors conveniently ignore this!

Note - I can already see several of these assumptions breaking down in a real
environment.

1. How is time (t) enforced?
2. How will the robots observe others' state?
3. How much time for each robot to calculate new velocity and start acting on it? since there's no central co-ordinator.
4. What if one robot goes bonkers and doesn't follow the same
strategy as others because of a bug?
```

Anyhow, after this authors spend use math / physics to derive optimal Reciprocal velocity to
avoid collision.

#### Static vs Dynamic Obstacles

Note that until now we were only talking about avoiding bumping into other robots,
**BUT** there can be static obstacles.

These are assumed to be line segments.

The authors then show an approach.

Fascinating Graphs, simulation pictures and Experimental Data follows. The paper does
with ~1000 robot simulations.

**Authors don't talk about dynamic obstacles**

Performance Results

```
This section seems flawed
```

quote from paper
```
Because each agent makes independent decisions, we are able to efficiently parallelize
the simulation by distributing the computations for agents across multiple processors.
We used OpenMP multi-threading to parallelize key computations across
eight Intel Xeon 2.66GHz (Clovertown) cores
```

ofourse, each robot computes on its own in parallel! We saw the loop above already. The
running time of sequential algorithm is useless. Also OpenMP will also scale to the number
of cores in each machine, so the multi-threading Intel stuff is bull crap.

I think a scala / Akka  or any async Actor based programming model would be ideal for simulating this setup.

the Actors will 'message' their external state to every other actor in the system (we can treat this as a way of approximating the fact that each robot senses the position of every other robot after every time interval t)


### References
[1] http://users.ece.cmu.edu/~koopman/des_s99/formal_methods/
