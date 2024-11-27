# P4 - Global Navigation
**Date:** 27/11/2024

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

Once the **cost map** is completed and all the detected obstacles have been added to the **obstacle array** I create an **obstacle map** which will store an extra cost assigned to the cells near the obstacles stored in the **obstacle array** so that the taxi does not navigate too close to the obstacles or collides with them.

This proccess follows the next structure, for every obstacle in **obstacle array** assing an extra cost to all the cells that forms an aXa square around the obstacle. The cost of each cell is determined by the layer the cell is located at. The closer the layer is to the obstacle the grater the cost of the cell. The dimensions of the square (number of layers) have been previously established.

Before assigning the cost to the cell, some conditions are checked: *that cell is not an obstacle and that cell is not the target*.

### Gradient navigation:

Once the **cost map** and the **obstacle map** are calculated the **final cost map** is obtained as the sum of both maps, so that, the cost of the cells near to the obstacles is incremented. Therefore, the **final cost map** will be the one used by the taxi to navigate.
The navigation part follows the next structure:
- Get the position of the car relative to the map.
- Run through all the cells that form an aXa square around the taxi and get the coordinates relative to the map of the cell with less cost. The dimensions of the square (number of layers) have been previously established.
- Once the cell with less cost is founded, check if the target is reached (with some tolerance) and end navigation in case it is.
- Convert cell coordinates with minimum cost to world coordinates relative to the taxi and calculate speeds the following way:
  - **angular_speed:** is calculated as the atan2 of these coordinates.

  - **linear_speed:** is calculated as the **MAX SPEED** constant minus the **angular speed** icreased by a *LIMIT FACTOR* so that the greater the angle to turn the smaller linear speed.

### Obtained results:
The taxi is able to navigate through the map to reach the chosen target. If the target is modified during the taxi navigation to the target, the taxi stops, create a new **final cost map** and starts to navigate to the new target. The **final cost map** creating proccess cannot be interrupted.

## Difficulties:

  - Find an appropiate **extra cost** for each layer of the square around the obstacle so that it is relevant but does not prevent the taxi from being able to pass through some streets in addition to determining appropiate dimensions for the square.

  - Find the dimensions of the square to expand around the taxi to get the cell with less cost.

  - Find a way to calculate angular and linear speeds so that the car moves securely.

  - When the target is behind the initial position of the taxi there are some cases in which when it starts to turn around it collides with the wall. I tried to solve it by making **zero or near-zero** linear speed at large turns **big turns (high angular speed)**. I did this by increasing the *LIMIT FACTOR*. I leave commented the previous *LIMIT FACTOR* value with which the taxi had linear speed also in big turns.

## Execution video:
- **New limit factor:** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EW7heM5ZT-pEklbeVxAAKnEBD3d49uveMm2FyqsQumwrWg?e=PrjEFZ

- **Old limit factor (with some linear speed in big turns):** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EXG3H0HaiUpLreEEVb4B6vMB0Zp0dcsXDANTrfv8FRaIyA?e=PZ3prf

- **New limit factor changing target during navigation:** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EaLhN20SqB5JtemLoTMbWNgBmaM_gY7zKHzmB4y1SjAopw?e=gHQ6Wq
