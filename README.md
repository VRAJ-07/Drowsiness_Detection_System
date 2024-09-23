# Drowsiness Detection System

## Overview
The **Drowsiness Detection System** is a computer vision project aimed at detecting whether a person is drowsy or alert based on the eye aspect ratio (EAR) calculated from facial landmarks. The system captures real-time video from the webcam, detects faces and landmarks, calculates EAR, and determines whether the person is drowsy based on a threshold value. If the EAR falls below a predefined threshold, the system flags the user as "Drowsy" and displays a red box around the face. If the EAR is above the threshold, the system labels the user as "Awake" with a green box.

## How It Works
1. The program captures video using a webcam.
2. A pre-trained facial landmark detector from `dlib` is used to detect facial landmarks for each frame.
3. The eye aspect ratio (EAR) is computed based on the coordinates of the eye landmarks.
4. If the EAR falls below a defined threshold (0.25 in this case), the person is marked as "Drowsy"; otherwise, they are marked as "Awake."
5. The system continuously processes video frames until the user quits the application.

## Dependencies

Ensure you have the following Python packages and files installed:

- **OpenCV** (`cv2`) - For video capture and frame processing.
- **dlib** - For face detection and facial landmarks prediction.
- **shape_predictor_68_face_landmarks.dat** - Pre-trained model for detecting 68 facial landmarks (can be downloaded from the dlib website).

## Installation

### Step 1: Clone the repository
```bash
git clone https://github.com/VRAJ-07/Drowsiness_Detection_System.git
cd Drowsiness_Detection_System
```

### Step 2: Install required libraries
You can install the dependencies using `pip`:

```bash
pip install opencv-python dlib
```

### Step 3: Download the shape predictor model
You need the `shape_predictor_68_face_landmarks.dat` file for landmark detection. You can download it from [dlib's GitHub page](http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2). After downloading, extract the file and place it in the project directory.

### Step 4: Run the script
After setting up the environment and downloading the required model, you can run the detection system using:

```bash
python drowsiness_detection.py
```

## Code Explanation

### `get_eye_aspect_ratio(eye)`
This function calculates the eye aspect ratio (EAR) for a given set of eye landmarks. It takes in six (x, y) coordinates representing an eye and calculates the EAR using the following formula:
```python
EAR = (|p2 - p6| + |p3 - p5|) / (2 * |p1 - p4|)
```
The EAR is used to determine whether the eye is open or closed.

### `check_drowsiness(landmarks)`
This function extracts the coordinates for both the left and right eye from the facial landmarks and calculates the EAR for both. It then computes the average EAR and checks if it falls below a certain threshold (0.25). If yes, it returns `True` indicating drowsiness; otherwise, it returns `False`.

### Main Script
1. **Face Detection**: Uses `dlib.get_frontal_face_detector()` to detect faces in the frame.
2. **Facial Landmark Detection**: For each detected face, the `predictor` extracts 68 facial landmarks, including those for the eyes.
3. **EAR Calculation**: EAR is calculated for both eyes, and the average is taken to check for drowsiness.
4. **Bounding Box**: A colored bounding box is drawn around the face to indicate the drowsiness state—red for "Drowsy" and green for "Awake."

### User Input
Press `q` to exit the application.

## Future Improvements
- **Alarm system**: An audio alarm could be added to alert the user when drowsiness is detected.
- **Multi-person detection**: Extend the system to handle multiple faces in the frame.
- **Better thresholds**: Dynamically adjust the EAR threshold based on individual calibration.
