##Problems in n-body collision avoidance w.r.t drastic changes in environment (like water-to-air or air-to-water)

Berg et.al's paper regarding reciprocal n-body collision avoidance goes into details of a method for guaranteed local collision-free movement. That solution is however tailored for land based flat terrain environments (office environments). There is an opportunity here to generalize that method to cover cases where the terrain is not so flat and where the medium changes between water and land.

###Assumptions made by Berg's paper regarding the robot
- Simple shape (square,rectangle,triangle)
- Moves in 2 dimensions
- Movement in a single medium
- Robot has perfect sensing (can infer shape, position and velocity of all objects around it)

###Opportunities for improvement
- Generalizing the solution for
  * Complex shapes
  * 3 dimensional movement
  * Movement in different mediums. Especially under water the robots could encounter vastly differing conditions because of water currents or even aquatic life like fish! This would stress the simple shape and perfect sensing assumptions made by the paper.
