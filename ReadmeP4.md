# P4 - Global Navigation
**Date:** 23/11/2024

**Author:** Andrés Galea Torrecilla

## Algorithm details:
The goal is to program a global navigation algorithm based on **"Gradient Path Planning" (GPP)** for a taxi in a city. Once the target has been selected the taxi must reach it by the *shortest* route.

### Wave Front Algorithm:

There is an inicialization part where I define all the needed elements before starting to expand:
  - A **cost map** that will store the cost of every singe expanded cell and an obstacle array. The default value of every position of the array is *float(inf)* therefore obstacles will have a *float(inf)* cost.
  
  - An **obstacle array** that will store the coordinates of every detected obstacle.

  - The **frontier** (queue) that will store the corrdinates relative to the grid of all cells with **assigned cost** pending expansion. I 

Once all these elements have been defined, while the frontier is not empty, or the position of the car (plus the extra expansion) has not been reached I implemented the following procedure:



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
