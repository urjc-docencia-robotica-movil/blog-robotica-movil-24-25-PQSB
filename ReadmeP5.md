# P5 - Montecarlo Laser Localization
**Date:** 22/12/2024

**Author:** Andrés Galea Torrecilla

**Execution video:** 

## Algorithm details:
The goal is to program a localisation algorithm based on the **Monte Carlo algorithm**. The developed algorithm shall estimate the position of the robot on the map.

The parameters used in the algorithm are the following:
- PARTICLES NUMBER = 600
- LASER BEAMS NUMBER = 15
- RAYTRACING SKIP STEPS = 2

### Particle initialization:
To initialize the set of samples I follow the next procedure:
- Store in a **numpy** array all the free zones indexes of the map.
- Randomly choose *NPARTICLES* indexes of that array.
- For *NPARTICLES* to create, create a particle with the coordinates stored in that index of the array but in world coordinates format and add to the particle a randomly chosen orientation between 0 and 2pi.
- Assign the initial probability **1 / NPARTICLES** to every particle

This is are examples of the result (assigning 1 probability to all particles so that they can be seen):
#### 500 particles
![500 particles initialization result](500particles.png)
#### 600 particles
![600 particles initialization result](600particles.png)

### Particle propagation:
The propagation of particles is made using the function **HAL.getOdom()**. The idea is to use the odometry to estimate the displacement that the robot has made to apply it to all particles.
This is calculated by subtracting the odometry in **t** minus the robot odometry in **t^-1** and adding some **noise** to the result. This is due to some reasons:
- To simulate an appropiate movement since the robot movement is neither exact nor deterministic.
- To prevent particles from staying always in the same area, which may result in the particles not being able to localise properly.

### Particle weight assingment:
For particle weight assignment I follow the next procedure for each particle in the particles array:
- Get the virtual laser values of the particle.
- Calculate the difference of between the real laser and the virtual laser of that particle for **every laser beam**.
- Calculate the mean of the square of all the differences **(MSE)**.
- Calculate the final weight as **np.exp(-1 * square_mean_diff)**

**Improvement:** before assigning the weight to the particle I check if the particle is in an obstacle or out of the map boundaries in which case I give **zero probability** without raytracing that particle.

### Particle resampling:
For particle resampling I follow the next procedure:
- Create an empty array with *NPARTICLES* dimensions.
- Creta a weight array that stores the weights of all particles.
- Normalize the weight array.
- Use the function **np.random.choice** with the replace option set to **TRUE** and with the weight array as reference to calculate *NPARTICLES* indexes of the array. These idexes represent the new set of particles, most of them generated near the ones who had a bigger weight in the last iteration.

**Improvement:** as to normalize I have to check that the sum of the array of probabilities is not zero, in which case I re-initialise the particles, I have also added that if the sum of probabilities is too small, I also re-initialise the particles as they will be too badly located.

### Optimisation techniques:
Before starting to implement optimisation techniques I measured the execution time of each part of the main loop obtaining the following results:
- **Particle propagation time:** between 0.00007 and 0.0001 (aprox).
- **Weight assingning (with raytracing):** between 0.38 and 1.01 (aprox).
- **Particle resampling:** between 0.0002 and 0.0015 (aprox).

Given the previous results, I used the following techniques to reduce it:
- **Multiprocessing:** the use of raytracing is the part with highest computational cost, so I used multiprocessing to calculate the weight of every particle. This increased a lot the frecuency the algorithm could execute at.
- **Raytracing skip steps:** to reduce the computational cost of the raytracing part, every laser beam will just sample half of the times.

After applying them and under the same conditions, these are the results:
- **Bump and go + Particle propagation time:** between 0.0002 and 0.005 (aprox).
- **Weight assingning (with raytracing):** between 0.07 and 0.16 (aprox).
- **Particle resampling:** between 0.0005 and 0.0019 (aprox).

## Obtained results:


## Difficulties:

  - 

  - 

  -

  -
