# P4 - Global Navigation
**Date:** 23/11/2024

**Author:** Andrés Galea Torrecilla

## Algorithm details:
The goal is to program a global navigation algorithm based on **"Gradient Path Planning" (GPP)** for a taxi in a city. Once the target has been selected the taxi must reach it by the *shortest* route.

### Wave Front Algorithm:

There is an inicialization part where I define all the needed elements before starting to expand:
  - A **cost map** that will store the cost of every singe expanded cell and an obstacle array. The default value of every position of the array is *float(inf)* therefore the default weight of every cell is *float(inf)*.
  
  - An **obstacle array** that will store the coordinates of every detected obstacle.

  - The **frontier** (queue) that will store the corrdinates relative to the grid of all cells with **assigned cost** pending expansion.

  - The **car location coordinates** relative to the map. Neccesary to know when to end the expansion.

  - An **expanded map** which will be used to check when a node has already been expanded and assigned a cost.

Once all these elements have been defined, I get the coordinates of the current target relative to the grid, set it cost in the cost map to zero so that the target has zero cost and add it to the frontier.

After that, while the frontier is not empty, or the position of the car (plus the extra expansion) has not been reached the following procedure is executed:

- Get one node from the frontier.
- Check if that node has already been expanded.
- Check if the position of the car (plus the extra expansion) has been reached.
- Check if the node is an obstacle and add it to the **obstacle array** in case it is.
- Expand, add to frontier and assign cost to the neighbors of the current node.
- Normalize and show the current **cost map** to see how the expansion evolves.

### Obstacle expansion:
Once the **cost map** is completed and all the detected obstacles have been added to the **obstacle array** I create an **obstacle map** which will store all obstacles plus an extra expansion to prevent the car from driving too close to the walls.
This expansion is made the following way:
  - For every obstacle in **obstacle array** I assign a cost to the cells around the obstacle.

### Gradient navigation:

I used the force obtained from there to calculate linear and angular speeds the following way:
  - **linear_speed:**
  
  - **angular_speed:**

### Obtained results:
The taxi is able to navigate through the map to reach the chosen target. If the target is modified during the taxi navigation to the target, the taxi stops, create a new **final cost map** and starts to navigate to the new target. The **final cost map** creating proccess cannot be interrupted.

## Difficulties: 
  - 
  
  - 

  - 

## Execution video:
