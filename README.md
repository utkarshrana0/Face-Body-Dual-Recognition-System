# Facial-Body-Dual-Recognition-System

I have implemented a system for detecting and tracking multiple faces and bodies from live video. It uses the Computer Vision System Toolbox and the Webcam Support Package. The system detects faces using the Viola-Jones algorithm, detects min-eigen corners within each face's bounding box, and tracks the corners using the Kanade-Lucas-Tomasi (KLT) algorithm. It re-detects the objects every 10 frames in order to correct the tracker and replenish the points.

## Methodology

`Detect an object`

First, we must detect the object. We use the “vision.CascadeObjectDetector” system object to detect the location of a face/body in a video frame. The cascade object detector uses the Viola-Jones detection algorithm and a trained classification model for detection. By default, the detector is configured to detect faces, but it can be used to detect other types of objects and hence we use it for full body as well.

To track the face over time, this example uses the Kanade-Lucas-Tomasi (KLT) algorithm. While it is possible to use the cascade object detector on every frame, it is computationally expensive. It may also fail to detect the face, when the subject turns or tilts his head. This limitation comes from the type of trained classification model used for detection. The example detects the face only once, and then the KLT algorithm tracks the face across the video frames.

`Identify facial features to track`

The KLT algorithm tracks a set of feature points across the video frames. Once the detection locates the face, the next step in the example identifies feature points that can be reliably tracked. This example uses the standard, "good features to track" proposed by Shi and Tomasi.

`Initialize a tracker to track the points`

With the feature points identified, we can now use the vision.PointTracker System object to track them. For each point in the previous frame, the point tracker attempts to find the corresponding point in the current frame. Then the estimateGeometricTransform function is used to estimate the translation, rotation, and scale between the old points and the new points. This transformation is applied to the bounding box around the face.

`Initialize a video player to display the results`

We create a video player object for displaying video frames.

`Track the face`

The program tracks the points from frame to frame, and use estimateGeometricTransform function to estimate the motion of the face.

`For full body detection segment`

We follow the same methodology for the full body detection except we replace “faceDetector = vision.CascadeObjectDetector();” with “peopleDetector = vision.PeopleDetector();”.
