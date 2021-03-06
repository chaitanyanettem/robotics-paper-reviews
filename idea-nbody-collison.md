##Problems in n-body collision avoidance w.r.t drastic changes in environment (like water-to-air or air-to-water)

Berg et.al's paper regarding reciprocal n-body collision avoidance goes into details of a method for guaranteed local collision-free movement. That solution is however tailored for land based flat terrain environments (office environments). There is an opportunity here to build on the work from this paper and generalize it to cover cases where the terrain is not so flat or where the medium changes between water and land.

###Assumptions made by Berg's paper regarding the robot
- Simple shape (square,rectangle,triangle)
- Moves in 2 dimensions
- Movement in a single medium
- Has perfect sensing (can infer shape, position and velocity of all objects around it)
- Robots are not allowed to communicate with each other

###Opportunities for creating a generalized solution

- Making concessions for complex shapes with regard to robot construction
- 3 dimensional movement
- Movement in different mediums. Especially under water the robots could encounter vastly differing conditions because of water currents or even aquatic life like fish! This would stress the simple shape and perfect sensing assumptions made by the paper.
- A number of new possibilities would open up on removing the restriction of the robots being unable to communicate with one another

A good starting point might be to take the linear programming and physics framework that the paper has created for 2 movement in dimensions and expand it to include situations where the bots might encounter pools of water.

####I spoke with Zakieh and Ali regarding this idea and they had a couple of comments which I'm summarizing here:
Expanding this idea to cover 3 dimensional movement is a lot more difficult than it may seem because the entire framework would have to be adapted for an extra dimension. It might or might not be possible to do it so a better idea would be to first adapt the linear program for the possibility of the bots encountering "water puddles" which would probably not take as much adjusting since the linear program is already in 3 dimensions.

Just as an update - I'm talking with Zakieh now and working on understanding the physics and the linear program involved more thoroughly to see how it can be adapted to our situation.
