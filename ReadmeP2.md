# P2 - Follow Line

**Date:** 13/10/2024

**Author:** Andrés Galea Torrecilla

## Simple Model:

### Algorithm details:
This algorithm receives information from the camera, gets the position of the red line in case the line is being detected and computes angular and linear speeds that makes the car follow the line the best way possible.

#### Sensing Procedure:
To compute the image got from the camera I decided to use an HSV filter because I founded easier to get extract the red pixels. Once the iamge is filtered, I compute all the columns of 4 rows of the image (the begining row is obtained by dividing the number of rows by a division factor) saving the red pixels location, and I compute the mean of those values. Finally, I compare the new mean with the expected mean, and that is the error. As the error is in pixels the value of the PID constants are low.

#### Controller used:
The algorithm uses a PID to adjust the angular speed of the car, the linear speed controller is very simple. I thougth that an easy but effective way to control the linear speed was to have an established maximum linear speed and adjust it by substracting the angular speed of the car. However, I saw that wasn't enough to control it in an appropiate way so I established a constant to increment the value of the substracting part. It worked pretty well.

To adjust the PID constants, I first set the KP value and then I add KD and KI by trying a lot of different values until the car beahved really close to the desired way. Increasing of decreasing those constant according to the behavior I observed in each case.

To reset the value of the integral cummulative part I decided to have an error accumulator whose maximum value is established, so that the When the accumulated error is higher, it is reset to zero value. I spent some time adjusting this value, until I check it worked properly.

#### Recovery system:
When the red line is not being detected, the car turns with no linear speed in the direction it had when he lost the line.

### Obtained results:
The car follows the line quite well in all the racing circuits. Obtaining in the simple circuit a lap time of 38 s aprox.

## Ackerman Model:


## Difficulties:

While developing the algorithm I found some difficulties:
  - 
  
  - 

  -
### Tests:
