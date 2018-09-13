# **Model Predictive Control** 

---

**Model Predictive Control  Project**

The goals / steps of this project are the following:
* Implement a Model Predictive Controller that controls the steering of a car in the simulator
* Test that the controler successfully drives around the track without leaving the road
* Summarize the results with a written report

[//]: # (Image References)

[image1]: ./writeup/model.jpg "Model"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/896/view) individually and describe how I addressed each point in my implementation.  

---
### Compilation

#### 1. Code must compile without errors with `cmake` and `make`.

My project includes the following files:
* src/MPC.h header file for the MPC Controller class
* src/MPC.cpp source file for the MPC Controller class
* src/json.hpp library for handling json
* src/main.cpp main source file containig the main loop

I didn't change the CMakeFiles.txt so everything should compile fine.

### Implementation

#### 1. Student describes their model in detail. This includes the state, actuators and update equations.

My model is the same as described in the lessons:
![alt text][image1]

The state is made of:
* x
* y
* psi
* v
* cte (Cross Track Error)
* epsi (Psi error)

The actuators are:
* a (throttle)
* delta (steering angle)

For the update equations see the image.

#### 2. Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

I chose 8 steps, with a duration between timesteps of 0.1s. That spans a horizon of 0.8 Seconds. A shorter horizon either way tends to get instable in narrow bends.
To much steps on the other side lead to an oscillation of the trajectory which will get stronger over time resulting in leaving the track.

#### 3. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.

The waypoints are transformed into the car coordinate system.
The vehicle state is partly transformed 0.1 seconds in the future using the kinematic model. (See latency next point)

#### 4. The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.

The x, y, v, cte and epsi part of the initial mpc state (not psi) are predicted 100 milliseconds into the future using the actual speed and steering angle. This deals with the 100 millisecond latency.

### Simulation

#### 1. The vehicle must successfully drive a lap around the track.

On my machine the vehicle drives successfully around the lap.