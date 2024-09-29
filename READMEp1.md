# P1 - Vacuum Cleaner

**Date:** 29/09/2024

**Author:** Andrés Galea Torrecilla

**FSM state diagram:** https://urjc-my.sharepoint.com/:i:/g/personal/a_galea_2022_alumnos_urjc_es/EQsDVcf6nKVNu4jCtFLJ99cBmrUZzL2etKEK3WI-PCxabA?e=GNHmM2

**Execution video:** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/ESQ0Z-PZGQREt7hPXXMuixIB6p1fMlhyOOHcUDrQJW8sKg?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=7Mn3VZ

## Algorithm details

The algorithm has the following states: *SPIRAL_MOTION*, *MOVING_BACKWARD*, *TURNING* and *MOVING_FORWARD*. It uses the information received from the laser and bumper sensors and decides how to move and turn in each situtation.

### Key states:
  - **SPIRAL_MOTION:** The robot follows a spiral pattern, so that, at the begining it covers the greatest area possible.

  - **MOVING_BACKWARD:** When the bumper detects a collision (on the left, right or front), the robot moves backward for a set amount of time. This gives it some space to avoid the obstacle detected.
  
  - **TURNING:** After moving backward, the robot turns in the direction set by the bumper zone that detected the obstacle. Moreover, depending on the laser measures at 0º, 90º and 180º it decides whether it's too close to a wall or obstacle. Depending on those meausres there are two possible turn types:
       - Normal turn: If it has enough space in front and around the robot, it performs a normal turn with random parameters.
       - Wall turn: If it is too close to a wall or obstacle it turns at a smaller angular speed to try to follow the wall or to go around the obstacle.
         
      To avoid getting stuck if the robot detects that the wall turn type has been used more times than the maximum established, it makes a big turn.
  
  - **MOVING_FORWARD:** After the turn, the robot moves forward with a constant linear speed until the bumper is hit. Furthermore, if the robot detects that the turn direction has been the same more times than the maximum established, it adds a constant angular speed until another turn direction is choosen.

## Difficulties

While developing the algorithm I found some difficulties:
  - The robot getting stuck in certain places of the map. I try to solve it by including conditions that check if the robot has been a lot of time close to the wall.
  
  - The robot being unable to get out of rooms with hard access, I try to solve it by adding angular speed to the movement while following the wall so that it makes easier for the robot to rotate himself the correct way to make his way out of the room.
  
  - The robot not convering enough sapce of the house. To solve this I try to find a solution that combines some random elements with some established elements, such as having established turn directions depending on the bumper zone hit but turning during a random period of time (in the normal case).

  - Not being able to make the robot turn a concrete angle as long as the robot turns must be calculated by substraction of times. To solve this I decided to get the laser data only of three concrete angles and to make the turns based more on the bumper that on the laser sensor. Using the laser sensor only to estimate the freedom of the area around the robot.

## Tests
I simulated the algorithm a lot of times while triying to improve it and I realised that:
  - Adding angular speed to get out of rooms decreased a lot the time needed by the robot to get out of the room.

  - Following the wall and having established turning directions depending on the bumper zone hit increased a lot the explored area of the house.
