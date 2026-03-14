# Autonomous Vision-Guided Line Following Robot

This project implements an autonomous robot capable of **precision line following, obstacle avoidance, and real-time object detection** using a hybrid architecture combining **Arduino for control** and **Raspberry Pi for AI vision processing**.

The system integrates PID-based navigation, ultrasonic obstacle detection, and a live monitoring dashboard powered by computer vision.

---

## System Overview

The robot uses two processing units:

**Arduino Uno**

* Handles real-time motor control
* Implements PID line following
* Processes ultrasonic obstacle detection

**Raspberry Pi 4**

* Performs real-time object detection using YOLO
* Streams camera feed to a web dashboard
* Maintains a list of detected objects

---

## Key Features

### Precision Line Following

* 5-channel **CTR5000 IR sensor array**
* **Weighted error calculation** for accurate tracking
* PID controller dynamically adjusts motor speed

PID constants used:

Kp = 1.0
Ki = 0.0
Kd = 14.0

Additional capabilities:

* Automatic **line recovery** when the robot loses the track
* **All-black detection** for finish line stopping

---

### Intelligent Obstacle Avoidance

* Triple ultrasonic sensors:

  * Front
  * Left
  * Right

These allow the robot to scan the environment and avoid collisions autonomously.

---

### AI Vision System

The Raspberry Pi camera performs real-time object detection using:

* **YOLO (Ultralytics)**
* **NCNN optimized inference**
* **OpenCV image processing**

Capabilities:

* Detects predefined card classes
* Tracks detected objects
* Draws bounding boxes on the video stream
* Maintains a unique list of detected objects

---

### Web Monitoring Dashboard

A **Flask-based web interface** provides real-time monitoring.

Dashboard displays:

* Live camera feed
* Number of detected cards
* List of detected objects
* Mission timer
* Reset memory control

The dashboard can be accessed from any device connected to the same network.

---

## Project Structure

Bot_Design
│
├── line_following_obstacle_avoidance.ino  (Arduino firmware)
├── app.py  (Flask server + vision processing)
├── web_interface.html  (Dashboard UI)
├── models/  (YOLO NCNN model files)
└── README.md

---

## Hardware Components

* Arduino Uno
* Raspberry Pi 4
* Raspberry Pi Camera Module
* 5-Channel IR Sensor Array (CTR5000)
* Ultrasonic Sensors (Front / Left / Right)
* L298N Motor Driver
* Servo Motor
* DC Motors + Chassis

---

## System Architecture

Raspberry Pi 4
│
├── Camera → YOLO Object Detection
├── OpenCV Processing
└── Flask Web Server
│
└── Web Dashboard (Laptop / Phone)

Arduino Uno
│
├── IR Sensor Array → Line Detection
├── Ultrasonic Sensors → Obstacle Avoidance
├── Motor Driver (L298N)
└── Controls Robot Movement

---

## Setup Instructions

### Arduino Setup

1. Install the **Servo library** in Arduino IDE.
2. Connect sensors and motor driver according to the pin definitions in the firmware.
3. Disconnect the **RX pin** of the right ultrasonic sensor while uploading to avoid serial conflicts.
4. Upload the firmware to the Arduino.

---

### Raspberry Pi Setup

1. Install dependencies:

   * Python
   * OpenCV
   * Flask
   * Ultralytics YOLO

2. Place the YOLO model files in the **models/** directory.

3. Run the web server:

python app.py

4. Open the dashboard in a browser using the Raspberry Pi's IP address.

