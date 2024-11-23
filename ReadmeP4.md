# P4 - Global Navigation
**Date:** 23/11/2024

**Author:** Andrés Galea Torrecilla

## Algorithm details:
The goal is to program a local navigation algorithm based on "Virtual Force Field" (VFF) for a formula 1 car that advances through the center of the circuit avoiding any obstacle that is along the way.

### Wave Front Algorithm:
To calculate the attractive force, first I get the **attractive vector** whose coordinates are the current target coordinates relative to the F1. Once I have the **attractive vector** I obtain the **attractive force** by regulating the module of the attractive vector to an established maximum value, because if not, the attractive force will make the repulsive force be insignificant.

### Obstacle expansion:

### Gradient navigation:

I used the force obtained from there to calculate linear and angular speeds the following way:
  - **linear_speed:**
  
  - **angular_speed:**

### Obtained results:


## Difficulties: 
  - 
  
  - 

  - 

## Execution video:
