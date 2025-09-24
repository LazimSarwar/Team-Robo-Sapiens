Future Engineers – Obstacle Avoiding Robot Car
1. Introduction

This project was developed for the World Robot Olympiad (WRO) Future Engineers category. The objective is to design, build, and program an autonomous vehicle that can navigate an environment while avoiding obstacles, demonstrating concepts of self-driving cars and intelligent robotics.

Our solution is based on a rear-wheel drive system with steering control through a servo motor, and obstacle detection using three ultrasonic sensors placed in the front, left, and right sides of the vehicle. The robot continuously evaluates distances to obstacles, makes decisions about which direction is safest, and navigates accordingly.

This repository contains the source code, wiring documentation, and design notes required to replicate our vehicle. All elements are open-source so that new teams can learn from and expand upon this design.

2. Hardware Components

The vehicle was built using widely available components to keep costs low and ensure reproducibility. The key hardware modules are:

Controller Board: Arduino Uno R3

Motor Driver: L293D Motor Shield

Drive Motor: 1x TT Geared DC Motor (rear axle)

Steering Mechanism: 1x Micro Servo Motor (front axle steering)

Sensors: 3x HC-SR04 Ultrasonic Sensors (front, left, right)

Wheels & Chassis: Acrylic or 3D-printed chassis with two rear wheels and a front steering system

Power Supply: 9–12V Li-ion battery pack (a 9V block battery is insufficient for sustained current draw)

Additional Components: Jump wires, screws, mounts, and headers

3. Software Architecture

The software was written in Arduino IDE (C++), using the following libraries:

Servo.h → for steering control

AFMotor.h → for motor driver control

NewPing.h (optional) → for reliable ultrasonic readings

The program is divided into logical modules:

Motor Control Module – controls rear DC motor (forward, backward, stop).

Servo Control Module – positions the steering servo (left, center, right).

Ultrasonic Sensor Module – reads distances from the front, left, and right sensors.

Navigation Logic Module – makes decisions (go forward, turn left, turn right, reverse).

Safety Module – ensures the vehicle stops if an obstacle is too close.

4. System Workflow

The front ultrasonic sensor measures distance directly ahead.

If no obstacle is detected within the safe distance, the vehicle moves forward.

If an obstacle is detected:

The left and right sensors measure distances.

The vehicle compares which side has more free space.

Based on sensor input:

If left is clear → turn left.

If right is clear → turn right.

If both blocked → reverse briefly, then turn around.

Steering adjustments are made by rotating the servo motor to the corresponding angle.

5. How Hardware and Software Interact

The ultrasonic sensors are mounted at fixed angles. Their digital signals are processed by the Arduino, which calculates distance based on pulse timing.

The navigation module uses thresholds (stopDist, maxDist) to determine whether movement is safe.

The rear DC motor is powered through the L293D motor driver shield and responds to forward/backward commands.

The servo motor receives PWM signals to set the steering angle (center, left, right).

This creates a feedback loop:
Sensors → Arduino logic → Motor + Servo actuation → Vehicle movement.

6. Build, Compile & Upload Process

Open Arduino IDE on your computer.

Connect the Arduino Uno with a USB cable.

Install the required libraries (Servo.h, AFMotor.h, NewPing.h).

Load the source code (main.ino) from the /code/ folder.

Select Board: Arduino Uno and the correct COM port.

Click Upload to flash the code.

Disconnect USB and power the system using a Li-ion battery pack.

7. Challenges and Solutions

Servo Centering Issue: Our servo’s neutral position was not 90° but 155°. We adjusted this in code to ensure straight-line movement.

Vehicle Circling: Initially, the vehicle moved in circles because of misaligned steering. Calibration of servo angles solved this.

Power Limitations: A standard 9V battery could not deliver enough current, causing resets. Switching to a Li-ion battery pack solved the issue.

Sensor Accuracy: Ultrasonic sensors sometimes gave false readings. Adding a timeout and averaging multiple readings improved stability.

8. Conclusion

Our project demonstrates a simple but effective autonomous obstacle avoidance robot using affordable hardware and modular software design. By integrating rear-motor drive, servo-based steering, and three ultrasonic sensors, the robot can make intelligent navigation decisions in real time.

This repository was created not only to document our solution for WRO but also to support other teams. The Future Engineers category encourages open sharing of ideas, and we hope that our design and documentation inspire improvements and innovation.
