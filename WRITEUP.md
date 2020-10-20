# Building an Estimator Project

This is the writeup for my project submission. I will discuss each point in the rubric below.

## Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf.

This is the file!

## Determine the standard deviation of the measurement noise of both GPS X data and Accelerometer X data.

For this point I created a jupyter notebook (not included in the repo) to study the logs
created by the `06_NoisySensors` scenario. I used the `numpy.std` function to compute the
standard deviation of the data. I however ended up rounding these standard deviations to
a single decimal as this was still working.

## Implement a better rate gyro attitude integration scheme in the `UpdateFromIMU()` function.

For this point I implemented two improvements over the original code:

1. I used quaternions to update the angle as suggested in the task description.
2. I implemented a different integrator: a [midpoint integrator](https://en.wikipedia.org/wiki/Midpoint_method).

Each method has reduced the error in scenario `07_AttitudeEstimation` by about one order of 
magnitude.

## Implement all of the elements of the prediction step for the estimator.

For this point I mostly copied the formulas contained in
the [Estimation for Quadrotors](https://www.overleaf.com/read/vymfngphcccj) 
document and completed the `PredictState`, `GerRbgPrime` and `Predict` 
member functions of `QuadEstimatorEKF` class.

## Implement the magnetometer update.

For this task I implemented the `UpdateFromMag` member function using the
formulas in the [Estimation for Quadrotors](https://www.overleaf.com/read/vymfngphcccj) 
document as well as changed the `QYawStd` to pass the scenario `10_MagUpdate`.

## Implement the GPS update.

For this task I implemented the `UpdateFromGPS` member function of `QuadEstimatorEKF`.

## Meet the performance criteria of each step.

The controller/estimator pair meet all performance criterias in the scenarios.

## De-tune your controller to successfully fly the final desired box trajectory with your estimator and realistic sensors.

I reduced the control parameters from

    kpPosXY = 35
    kpPosZ = 25
    KiPosZ = 30
    kpVelXY = 15
    kpVelZ = 10
    kpBank = 8
    kpPQR = 85, 85, 6

to the following

    kpPosXY = 25
    kpPosZ = 15
    KiPosZ = 20
    kpVelXY = 10
    kpVelZ = 7
    kpBank = 6
    kpPQR = 70, 70, 5
