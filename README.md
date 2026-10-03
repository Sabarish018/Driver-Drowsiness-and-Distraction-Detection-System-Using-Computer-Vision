# Driver Drowsiness and Distraction Detection System Using Computer Vision

A real-time, non-invasive driver monitoring system developed in Python using OpenCV, MediaPipe Face Mesh, and YOLOv8. The application continuously tracks driver alertness, detects fatigue and distraction cues, triggers audio-visual alarms, captures evidence screenshots, and logs event metrics with timestamps.

---

## Project Overview

Driver fatigue and distraction remain critical factors in road accidents. This project provides a low-cost, software-driven Driver Monitoring System (DMS) running on live video from a standard HD webcam. It processes facial landmarks and object detections concurrently to classify driver states into **Alert**, **Drowsy**, **Yawning**, or **Distracted**.

### Key Features
* **Eye Aspect Ratio (EAR) Analysis**: Identifies prolonged eye closure for reliable drowsiness detection.
* **Mouth Aspect Ratio (MAR) Calculation**: Tracks mouth opening movements to detect yawning.
* **Head Pose & Orientation Tracking**: Monitors directional orientation (Forward, Left, Right, Up, Down) to flag distraction from the road.
* **Mobile Phone Detection**: Utilizes a YOLOv8 deep learning model to spot mobile phone usage in the camera frame.
* **Real-Time Dashboard & Warnings**: Displays live EAR/MAR metrics, orientation, and driver status with visual warning banners.
* **Audio Alerts & Automated Logging**: Sounds a software-driven buzzer upon safety violations, automatically saves event screenshots, and writes records to a CSV log with date and time stamps.

---

## System Architecture & Workflow

```text
               +---------------------------+
               |  Webcam Video Acquisition |
               +-------------+-------------+
                             |
                   [ OpenCV Preprocessing ]
                             |
             +---------------+---------------+
             |                               |
             v                               v
+--------------------------+    +--------------------------+
|   MediaPipe Face Mesh    |    |   YOLOv8 Object Model    |
| (468 Facial Landmarks)   |    | (Phone Usage Detection)  |
+------------+-------------+    +------------+-------------+
             |                               |
  +----------+----------+                    |
  |          |          |                    |
  v          v          v                    |
[ EAR ]   [ MAR ]   [ Head Pose ]            |
  |          |          |                    |
  +----------+----------+                    |
             |                               |
             +---------------+---------------+
                             |
                             v
               +---------------------------+
               |  Driver State Classifier  |
               | (Alert/Drowsy/Yawn/Distr) |
               +-------------+-------------+
                             |
           +-----------------+-----------------+
           |                                   |
    [ Unsafe State ]                     [ Safe State ]
           |                                   |
           v                                   v
+--------------------------+            +--------------+
| - Visual Warning Banner  |            | Status: ALERT|
| - Software Buzzer Alert  |            +--------------+
| - Screenshot Captured    |
| - Event Logged to CSV    |
+--------------------------+
