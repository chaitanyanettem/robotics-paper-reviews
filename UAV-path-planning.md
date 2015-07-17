#Comparison of Parallel Genetic Algorithm and Particle Swarm Optimization for Real-Time UAV Path Planning

##Background
Path planner algorithms in the past used to have more relaxed conditions for success. The best path was the shortest aerial path between source and destination. In the recent past that has begun to change. Now there are more conditions placed when determining the best path including wind speed, altitude, velocity, trajectory and overall distance travelled. This has caused a drastic change in algorithms used to determine the best paths from predominantly deterministic to predominantly non-deterministic algorithms being used.

In this paper 2 non-deterministic algorithms are devised and compared for path planning for fixed-wind aircrafts. Along with this a comprehensive cost-function is proposed. The two algorithms used are the GA approach and particle swarm optimization. Both of these algorithms are being widely used for similar applications. It should be noted that in some cases the algorithm would need to be run a second time in order to produce better solutions. The paper doesn't go into how to determine whether or not the first solution is good.
