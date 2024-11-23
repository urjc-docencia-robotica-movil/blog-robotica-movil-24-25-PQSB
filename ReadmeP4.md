# P4 - Global Navigation
**Date:** 23/11/2024

**Author:** Andrés Galea Torrecilla

## Algorithm details:
The goal is to program a global navigation algorithm based on **"Gradient Path Planning" (GPP)** for a taxi in a city. Once the target has been selected the taxi must reach it by the *shortest* route.

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
