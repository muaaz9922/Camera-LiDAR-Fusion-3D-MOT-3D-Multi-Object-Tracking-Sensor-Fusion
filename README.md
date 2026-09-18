# 🚘 3D Multi-Object Tracking with Camera-LiDAR Fusion

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Open3D](https://img.shields.io/badge/Open3D-000000?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

A state-of-the-art perception framework designed for autonomous driving applications. This project fuses sparse 3D spatial data from LiDAR sensors with dense, high-resolution 2D semantic data from RGB cameras. By aligning these modalities, the system accurately detects, associates, and tracks multiple dynamic obstacles (vehicles, pedestrians, cyclists) across consecutive frames in 3D space.

---

## ✨ Key Features

* **Multi-Modal Sensor Fusion:** Accurately projects 3D LiDAR point clouds onto 2D camera planes using extrinsic and intrinsic calibration matrices to enrich bounding boxes with depth and semantic data.
* **3D Object Detection:** Utilizes modern detection backbones (`[e.g., PointPillars, SECOND, or Frustum PointNets]`) to generate initial 3D bounding box proposals.
* **Robust Data Association:** Implements a 3D extension of the SORT (Simple Online and Realtime Tracking) algorithm, utilizing 3D Kalman filtering for state estimation and the Hungarian algorithm for optimal bipartite matching.
* **Trajectory Management:** Handles track births, updates, and deaths seamlessly, maintaining consistent object IDs even during temporary occlusions.
* **Visualization Engine:** Includes custom rendering scripts using Open3D and OpenCV to visualize LiDAR point clouds, track trajectories, and camera projections simultaneously.

---

## 🏗️ Pipeline Architecture

```text
+----------------+      +----------------+
|  RGB Camera    |      |  LiDAR Sensor  |
|  (2D Images)   |      | (Point Clouds) |
+-------+--------+      +-------+--------+
        |                       |
        v                       v
+-------+--------+      +-------+--------+
|  2D Object     |      |  3D Object     |
|  Detector      |      |  Detector      |
+-------+--------+      +-------+--------+
        |                       |
        +-------> Fusion <------+
                  Module 
                    |
                    v
          +---------+---------+
          |  3D Kalman Filter | (State Estimation)
          +---------+---------+
                    |
                    v
          +---------+---------+
          | Hungarian Matcher | (Data Association)
          +---------+---------+
                    |
                    v
          +---------+---------+
          | 3D Tracked Output | (ID, Velocity, Pose)
          +-------------------+
