# Facial-Body-Dual-Recognition-System

I have implemented a system for detecting and tracking multiple faces and bodies from live video. It uses the Computer Vision System Toolbox and the Webcam Support Package. The system detects faces using the Viola-Jones algorithm, detects min-eigen corners within each face's bounding box, and tracks the corners using the Kanade-Lucas-Tomasi (KLT) algorithm. It re-detects the objects every 10 frames in order to correct the tracker and replenish the points.
