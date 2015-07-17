#Push and Swap: Cooperative path finding with completeness guarantees

##Introduction

This paper deals with the issue of computing paths which don't collide between start and end positions. Push and Swap is an alternative to the Operator Decomposition approach to cooperative path finding put forth by Standley[1].

This algorithm provides completeness guarantees i.e it can find a solution for any instance with n-2 agents in a graph of size n given that a solution exists.

The author defines 2 primitives:

* Push - agents move towards destination until no more progress maybe made

* Swap - allows agents to interchange positions without affecting positions of other agents

It is claimed that the algorithm can scale to instances involving hundreds of agents.

##Background

There are two ways of solving the problem:

* Coupled approach - The configuration space of individual robots is combined into one composite whole. Paths are searched for in the whole composite system. When integrated with search approaches like A* these methods provide completeness and optimality. However this has exponential dependence on n and hence is impractical for use in larger systems.

* Decoupled Approach - Paths are computed sequentially and conflicts are resolved when they arise. A lot of different decoupled approaches are discussed including: Prioritization - certain agents have higher priority (lower priority agents will treat higher priority ones as moving obstacles); Dynamic Prioritization; Flow Networks and a few others.

##Main Idea

In easy instances the problem can be solved by the agent moving along the shortest path to its destination and the agent would use the push primitive for such activities.

Harder problems will however need the use of swap primitive when an agent can no longer move towards its goal on the shortest path. This might involve the movement of all agents in the graph but eventually all the agents except the swapped agents should be returned to their original position. **The author claims that if this (the swap operation) is not executable then the problem is not solvable.**

##Algorithm
Before covering the algorithm I'll go over some of the notations used:

* Consider a graph G(V,E) and n agents R, where n ≤ |V|−2.
* An assignment A : [1,n] → V places all the agents in unique vertices: **∀i, j∈[1,n], j!=i : A[i] ∈ V, A[i] != A[j]**.
* The starting assignment will be denoted as S, while the target assignment will be denoted as T.
* An action π(Aa,Ab) is a change between two assignments Aa and Ab so that only one agent moves between neighboring nodes in the two assignments, i.e., ∃i ∈ [1,n] and ∀j ∈ [1,n], j != i: **Aa[i] = Ab[i], (Aa[i], Ab[i]) ∈ E, Aa[ j ] = Ab[ j ]**

A path Π = {A0 , . . . , Ak } is a sequence of assignments, so that for any two consecutive assignments Ai and Ai+1 in Π there is an action π(Ai , Ai+1 ). The objective of cooperative path-finding is to compute a path Π∗ = {S, . . . , T }, which is a similar sequence initiated with S and finishing with T.

###Push

The Push operation computes the shortest path p* between the current position and target position of an agent r. The method will iterate till r has not reached the target. If the vertices along p* aren't occupied then r is moved along it. If the agent hasn't reached target and it can't move along p* then the algorithm checks if it is possible to move the obstacles on p* towards the target. If it is then that is done. If not, then the swap operation is initiated.

###Swap
Overall, SWAP selects the agent s adjacent to the input agent r along r’s path p* to its destination and switches their positions leaving agents already at
their target positions intact. Swap can use an operation called *multipush* which involves pushing multiple agents at the same time to their adjacent positions.

There are a couple other operations described namely *Clear* and *Resolve* which are helper functions used in accomplishing Push and Swap. Not going into details of those here.


##References
[1 - Cooperative Path Finding](coop-path-finding.md)
