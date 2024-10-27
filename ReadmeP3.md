# P3 - Obstacle Avoidance
**Date:** 27/10/2024

**Author:** Andrés Galea Torrecilla

## Algorithm details:
The goal is to program a local navigation algorithm based on "Virtual Force Field" (VFF) for a formula 1 car that advances through the center of the circuit avoiding any obstacle that is along the way.

### Attractive Force:
To calculate the attractive force, first I get the **attractive vector** whose coordinates are the current target coordinates relative to the F1. Once I have the **attractive vector** I obtain the **attractive force** by regulating the module of the attractive vector to an established maximum value, because if not, the attractive force will make the repulsive force be insignificant.

### Repulsive Force:
Repulsive force is calculated as the *weighted* sum of all repulsive vectors.
To calculate each repulsive vector, the first thing to do is to transform the information of every single measure of the laser that is closer than an established distance into a vector.
Once the vector is calculated in polar coordiantes, I apply a kind of *filter* through which I increase or decrease the importance of that vector taking into account **how far** is it from F1 and if it is located in **the front or on the sides**.
I first thought about calculating the repulsive force as the mean of all repulsive vector however, that system that system was not capable of avoiding obstacles in front of it, so I realize that if I wanted the F1 to be reactive I needed to calculate a more reliable repulsive vector.
On the other hand I also thought about regulating the module of the repulsive force but as I want the F1 to be able to reach a relatively high speed, a big repulsive vector is needed when obstacles are too close.

#### Final/Resultant Force:
Once both attractive and repulsive forces are calculated I use formula: **(alpha x attractive_force) + (betha x repulsive_force)**.
I used the force obtained from there to calculate linear and angular speeds the following way:
  - **linear_speed:** To calculate it, I decided not to use the module of the force vector since as I said previously I decided not to regulate the module of the repulsive vector. Instead of that I use the **Y** coordinate by calculating it's *cos* and multiplying it by an established maximum linear speed. So that, when values are low it's almost 1 and as values increase, final linear speed decreases. In other words, the bigger turn the F1 has to make, less linear speed it will have.
  
  - **angular_speed:** The angular speed is calculated as the *tan* of the cartesian coordinates of the final force vector.

### Obtained results:
The reach the targets and avoid obstacles with a lap time of 1 minute and 10 s aprox.

## Difficulties:

While developing the algorithm I found some difficulties:
  - Obtain angular and linear speeds from a final force vector.
  
  - Finding the correct way to calculate the weight of each laser measure.

  - Identifying when it was better to use polar coordinates and when cartesian coordinates, specially when trying to find a way of calculating linear and angular speeds.

## Execution video:
https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/ESdwrjtiBuVAthbL4VyLQW4BhT3hlkHhW4PI272gK0U2Dg?e=Cj1UXQ

