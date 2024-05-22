# PoseControl
This project, named PoseControl ,  allows you to control a game using your body movements! It uses real-time pose estimation to translate your physical actions into gameplay commands.

This Python code control a game using real-time pose estimation. Here's a breakdown of the functionality:

Imports:

Necessary libraries for computer vision, image processing, and keyboard/mouse control are imported including OpenCV (cv2), MediaPipe (mp), NumPy (np), and pyautogui.
Functions:

detectPose - This function takes an image and a MediaPipe pose object as input. It processes the image using MediaPipe to detect poses and returns the processed image with keypoints and a list of detected landmarks.
calculateAngle - This function calculates the angle between three given keypoints.
classifyPose - This function analyzes the angles between various body parts (shoulders, elbows, knees) to classify the pose (e.g., Warrior II Pose, T Pose, Tree Pose). It returns a labeled image with the detected pose.
checkHandsJoined - This function checks if the user's wrists are close together based on a distance threshold. It returns an image with text indicating whether the hands are joined or not.
checkLeftRight - This function determines the user's horizontal position (left, right, or center) based on the shoulder keypoints. It returns an image with text indicating the position.
checkJumpCrouch - This function estimates the user's posture (jumping, crouching, or standing) based on the shoulder keypoint height relative to a midline. It returns an image with text indicating the posture.
Main Script:

Initializes a MediaPipe pose object and a webcam capture object.
Sets the game_started flag to False initially.
Enters a loop that continuously captures video frames.
Processes the frame using detectPose to get the image with keypoints and landmarks.
If a pose is detected:
If the game has started:
Uses checkLeftRight to determine the user's horizontal position and sends "left" or "right" keystrokes based on the position.
If the hands are joined (using checkHandsJoined), a counter is incremented. If the counter reaches a certain value (indicating sustained pose), the game is considered started, and the center of the shoulders is used to set a reference midline.
Uses checkJumpCrouch to determine the user's posture (jumping, crouching, or standing) and sends corresponding keystrokes ("up", "down")
