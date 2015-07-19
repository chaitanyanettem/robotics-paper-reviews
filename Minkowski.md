#Collison detection with Minkowski sum

##Introduction

One of the most important ways of doing collision detection is the Minkowski sum approach. The basic idea is that you add two shapes and get a new shape and if the zero vector of your base shape is inside the new shape then the two shapes are colliding (if that makes sense?).

##How to sum

You can represent a shape by a set of all the points within that shape. That set can of course be of infinite size. For example you can define a triangle as the set of all points within that triangle. You can also define it as the set of its 3 vertices.

##References

I went through a lot of reading material in order to thoroughly understand minkowski sums. Here are some of the more useful ones:

http://resources.mpi-inf.mpg.de/departments/d1/teaching/ss10/Seminar_CGGC/Slides/07_Bock_MS.pdf
http://doc.cgal.org/latest/Minkowski_sum_3/index.html
http://twistedoakstudios.com/blog/Post554_minkowski-sums-and-differences
https://en.wikipedia.org/wiki/Minkowski_addition
