# P2 - Follow Line

**Date:** 13/10/2024

**Author:** Andrés Galea Torrecilla

## Simple Model:

### Algorithm details:
This algorithm receives information from the camera, gets the position of the red line in case the line is being detected and computes angular and linear speeds that makes the car follow the line the best way possible.

#### Sensing Procedure:
To compute the image got from the camera I decided to use an HSV filter because I founded easier to get extract the red pixels. Once the iamge is filtered, I compute all the columns of 4 rows of the image (the begining row is obtained by dividing the number of rows by a division factor) saving the red pixels location, and I compute the mean of those values. Finally, I compare the new mean with the expected mean, and that is the error. As the error is in pixels the value of the PID constants are low.

#### Controller used:
The algorithm uses a PID to adjust the angular speed of the car, the linear speed controller is very simple.
I thougth that an easy but effective way to control the linear speed was to have an established maximum linear speed and adjust it by substracting the angular speed of the car. However, I saw that wasn't enough to control it in an appropiate way so I established a constant to increment the value of the substracting part. It worked pretty well.

To adjust the PID constants, I first set the KP value and then I add KD and KI by trying a lot of different values until the car beahved really close to the desired way. Increasing of decreasing those constant according to the behavior I observed in each case.

To reset the value of the integral cummulative part I decided to have an error accumulator whose maximum value is established, so that the When the accumulated error is higher, it is reset to zero value. I spent some time adjusting this value, until I check it worked properly.

#### Recovery system:
When the red line is not being detected, the car turns with no linear speed in the direction it had when he lost the line.

### Obtained results:
The car follows the line quite well in all the racing circuits. Obtaining in the simple circuit a lap time of 38 s aprox.

## Ackerman Model:

### Algorithm details:
This algorithm receives information from the camera, gets the position of the red line in case the line is being detected and computes angule and a linear speed that makes the car follow the line the best way possible.
To control the linear speed I finally decided to implement the same 

#### Sensing Procedure:
The same as in the simple model

#### Controller used:
The algorithm uses a PID to adjust the angular speed of the car, the linear speed controller is very simple.

To adjust the PID constants, I follow the same procedure as in the simple car model, setting the maximum linear speed with a lower value. Nevertheless, as the output provided by the PID was a big high I decided to multiply the output by a constant established value so that it regulates the output better.

To reset the value of the integral cummulative I did the same as in the other car model.

#### Recovery system:
When the red line is not being detected, the car turns with an established speed in the direction it had when he lost the line.

### Obtained results:
The car follows the line quite well if the maximum linear speed is low. With higher speeds it loses control.

### Idea:
I thought about implementing a more complex controller for the linear speed by computing the upper rows of the line so that the linear speed controller knows when a curve approaches and is able to gradually reduce the linear speed, so that the turn is softer and the car remains stable even at fast speeds. However, I run out of time before being able to have this working. So I implement a basic linear controller previouslly described.

## Difficulties:

While developing the algorithm I found some difficulties:
  - When executing the program in the simulator sometimes the same PID values obtained different results, probably due to the laptop.
  
  - The error in pixels i very big.

  - The ackerman model is really hard to control at high linear speeds.

## Execution videos:
**Simple simple circuit:** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EZaPHCOXCTdCoXS3O0tsSAkBJsHwVxadbUOg4f6COc4t3A?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=CXt8zF

**Simple Montmelo circuit (uses recovery system):** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EZeTJJ2fGrhDjSZov4lEgPABqmXbskP0Eq7sYTT3xoVzVg?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=YzIDqc

**Ackerman Simple:** https://urjc-my.sharepoint.com/:v:/g/personal/a_galea_2022_alumnos_urjc_es/EYbnaj1rF55EkSDPrJlAx3cBQ8Otp8xWC9sUVMsIXMYwQw?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D&e=TFRiDI
