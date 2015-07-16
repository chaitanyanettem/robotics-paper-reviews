#Finding optimal solutions to cooperative path finding

##Background
For single agent - solve with A*

for multiple agents **problem is** - must avoid collision/conflicts.

Silver (2005) Describes LRA* - path computed independently. Any conflicts will be discovered when executing. LRA* often results in  deadlocks and cycles. 

HCA* avoids this by using reservation table. Solutions significantly shorter than LRA* but still suboptimal. In a few cases agents don't reach destination.

Other algos assign directions to grid positions thus setting traffic rules but this means that results will always be suboptimal. Also can result in deadlocks and agents may never reach dest.

##Problem Formulation

Many variants of problem. Here we see 8x8 grid.

Each agent in one cell of grid. in each timestep agent may move or wait. Cell can be free or occupied. Diagonal moves possible. Cost of path is number of timesteps to reach goal/dest. Cost of entire solution is sum of all path costs. In additions paths should never intersect (Why?)

##Standard algo

The standard algorithm is A*. Each agent has 9 operations it can perform: {N, NE, E, SE, S, SW, W, NW, wait}. So at each timestep there are 9^n possible operations.

The cost of each operator is the number of agents not stopped at their goals. This method is always coupled with a heuristic.

Each node expansion can add 59k nodes (given  9 agents) so this method only useful for trivial problems.

##Operator decomposition

**This is the most important part of the new method.**

In standard algorithm every operator will change position of every agent in a given state. 

The new representation of state space allows timestep to be divided in a way such that agents are considered independently and a state requires n operators for each of the n agents to reach next timestep compared to one operator per timestep previously.

##The Heuristic and the algorithm

A* uses the sum of distance of the goal from the agents as a heuristic. Using this the algorithm will only search in the subspace of solutions that will reduce this distance. In the case of a cooperative pathfinding algorithm a possible heuristic is sum of costs of optimal single agent paths.

These paths can be obtained by running a BFS from agent's goal to every free grid position. The heuristic needs to be updated following every move made by an agent because move assignment is made for a single agent in the operator decomposition approach. The change is the difference between the entry for the post-move position and the pre-move position of each agent. RRA* is a possible approach for filling the table values but the benefit received is not very large.

The algorithm built for this approach makes use of simple independence detection (SID) to partition the agents into disjoint sets in a manner that the optimal paths computed for every set do not interfere with all the other sets.

