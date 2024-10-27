# P3 - Obstacle Avoidance
**Date:** 13/10/2024

**Author:** Andrés Galea Torrecilla

## Simple Model:

### Algorithm details:
The goal is to program a local navigation algorithm based on "Virtual Force Field" (VFF) for a formula 1 car that advances through the center of the circuit avoiding any obstacle that is along the way

#### Attractive Force:
To calculate the attractive force, first I get the **attractive vector** whose coordinates are the current target coordinates relative to the F1. Once I have the **attractive vector** I obtain the **attractive force** by regulating the module of the attractive vector to a maximum value of 3, because if not, the attractive force will make the repulsive force be insignificant.

#### Repulsive Force:
Repulsive force is calculated as the *weighted* sum of all repulsive vectors.
To calculate each repulsive vector, the first thing to do is to transform the information of every single measure of the laser into a vector.
Once the vector is calculated in polar coordiantes, I apply a kind of *filter* through which I increase or decrease the importance of that vector taking into account the **how far** is it from F1 and if it is located in **the front or on the sides**.
The final repulsive vector is calculated as the sum of all repulsive vectors in *cartesian coordinates*.




#### Final/Resultant Force:

### Obtained results:
The reach the targets and avoid obstacles with a lap time of 1 minute and 10 s aprox.

## Difficulties:

While developing the algorithm I found some difficulties:
  - 
  
  - 

  - 

## Execution video:
https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/ESdwrjtiBuVAthbL4VyLQW4BhT3hlkHhW4PI272gK0U2Dg?e=Cj1UXQ

