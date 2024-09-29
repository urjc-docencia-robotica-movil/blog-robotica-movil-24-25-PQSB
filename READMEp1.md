# P1 - Vacuum Cleaner

**Date:** 29/09/2024

**Author:** Andrés Galea Torrecilla

**FSM state diagram:** https://urjc-my.sharepoint.com/:i:/g/personal/a_galea_2022_alumnos_urjc_es/EQsDVcf6nKVNu4jCtFLJ99cBmrUZzL2etKEK3WI-PCxabA?e=GNHmM2

**Execution video:**

## Algorithm details

The algorithm has the following states: *SPIRAL_MOTION*, *MOVING_BACKWARD*, *TURNING* and *MOVING_FORWARD*. It uses the information received from the laser and bumper sensors and decides how to move and turn in each situtation.

### Key states:
  - **SPIRAL_MOTION:** The robot follows a spiral pattern, so that, at the begining it covers the greatest area possible.

  - **MOVING_BACKWARD:** When the bumper detects a collision (on the left, right or front), the robot moves backward for a set amount of time. This gives it some space to avoid the obstacle detected.
  
  - **TURNING:** After moving backward, the robot turns in the direction set by the bumper zone that detected the obstacle. Moreover, depending on the laser measures at 0º, 90º and 180º it decides whether it's too close to a wall or obstacle. Depending on those meausres there are two possible turn types:
       - Normal turn: If it has enough space in front and around the robot, it performs a normal turn with random parameters.
       - Wall turn: If it too close to a wall or obstacle it turns at a smaller angular speed to try to follow the wall or to go around the obstacle.
         
      To avoid getting stuck if the robot detects that the wall turn type has been used more times than the maximum established, it makes a big turn.
  
  - **MOVING_FORWARD:** After the turn, the robot moves forward with a constant linear speed until the bumper is hit. Furthermore, if the robot detects that the turn direction has been the same more times than the maximum established, it adds a constant angular speed until another turn direction is choosen.






## Dificulties
