# Introduction

## Particle base VIO

I am trying to develop a simple visual aided odometry based on particle filter.
The algorithm will be simpler than MSCKF, but it follow MSCKF way to design the system.

## Roadmap
### using Julia
First of all I will trying finish it with CPU in x-y-z frame without any rotation, and trying to make it running in realtime, while this, a full stack of develop tools based on unreal (make test data) and Three.js (visual debugging) will be maintain

Second I will trying to make it work in 6d space which contain rotation.

### using OpenCL

Thirdly I will using GPU skills like thrust or CUDA programming to rewrite this code to make it work on iPad.

## Algorithm

### Particle

A particle remeber its own state and also a weight. A particle can present X_{i,j} and w_{i,j} where i means its generation and j is its id.

### Prediction
Time goes by,particles reproduce themselves with IMU data,w_{i,j} will be mix with IMU data and randomly create new particle with a random error add to IMU data follow normal distribution.

### Update
Once a feature point dropped from the screen, the update step start. It take the particle from the generation i which have the feature point by probability follow the particle weight w_{i,j}, and uses this all poses to calculate a best particle position. Note here, particle position should follow most constrain but not all.
After we know the position of the feature point and we shall also know the distribute of its position. And then we use the feature point to update the weight of each particle of each generate.
After that,we let some particle survive use their weight as survive probability.

Note that the resampler step for particle filter is in Update and prediction step.

## TODO
 - Fake data generator (feature point, IMU data)
 - PointCloud Visualizer can work with C (maybe using three.js?)
 - Gauss-Newton Minimization tools
