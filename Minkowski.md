#Collison detection with Minkowski sum

##Introduction

One of the most important ways of doing collision detection is the Minkowski sum approach. The basic idea is that you add two shapes and get a new shape and if the zero vector of your base shape is inside the new shape then the two shapes are colliding (if that makes sense?).

##How to sum

You can represent a shape by a set of all the points within that shape. That set can of course be of infinite size. For example you can define a triangle as the set of all points within that triangle. You can also define it as the set of its 3 vertices.
