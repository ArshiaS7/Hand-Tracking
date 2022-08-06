<!-- PROJECT LOGO -->
<div align="center">

  <img src=https://user-images.githubusercontent.com/54024838/183256056-79fb0350-400e-4f54-b96f-df6587719304.png alt="Logo" width="200">

  <h1 align="center">Hand-Tracking</h1>

  <p align="center">
    Hand-Tracking Project with Python: Using OpenCV &amp; MediaPipe
    <br />
    <br />
    <a href="#"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="#">View Demo</a>
    .
    <a href="#">Report Bug</a>
    .
    <a href="#">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
    </li>
    <li>
      <a href="#coding">Coding</a>
      <ul>
        <li><a href="#step1">Step 1 - Importations and initializations</a></li>
      </ul>
      <ul>
        <li><a href="#step2">Image Capturing and Processing </a></li>
      </ul>
      <ul>
        <li><a href="#step3">Step 3 - Working with Each Hand</a></li>
      </ul>
    </li>
  </ol>
</details>


<!-- ABOUT THE PROJECT -->
## About The Project

<div align = "justify">
  
  Hand tracking is the process in which a computer uses computer vision to detect a hand from an input   image and keeps focus on the hand’s movement and orientation. Hand tracking allows us to develop numerous programs that use hand movement and orientation as their input.
  
</div>



## Getting Started

<div align = "justify">

To create the program that will perform hand tracking, we will need two Python libraries. These are openCV and MediaPipe.

We will use openCV to perform operations associated with computer vision. We will use MediaPipe to perform the actual hand detection and tracking on our input image. 
  
</div>

- #### OpenCV
To install openCV, use the following command:
```python
pip install opencv-python
```

- #### MediaPipe
Type the following command in the terminal to install MediaPipe:
```python
pip install mediapipe
```

## Hand-Tracking Program

Hand tracking using MediaPipe involves two stages:

- <b> Palm detection: </b> MediaPipe works on the complete input image and provides a cropped image of the hand.
- <b> Hand landmarks identification: </b> MediaPipe finds the 21 hand landmarks on the cropped image of the hand.

The 21 hand points that MediaPipe identifies are shown in the image below:

<div align = "center"> 
  <img src = "https://user-images.githubusercontent.com/54024838/183256800-32f786e0-1b57-4ff1-b9b2-f9bd86ba9774.png" width = "500">
</div>

## Coding
### Step 1 - Importations and initializations

<div align = "justify">

We start by importing the two libraries we discussed. Importing the libraries enables us to use its dependencies.

We will then create an object cap for video capturing. We require the other three objects to manipulate our input using MediaPipe:
  
</div>

```python
import cv2
import mediapipe as mp

cap = cv2.VideoCapture(0)
mpHands = mp.solutions.hands
hands = mpHands.Hands()
mpDraw = mp.solutions.drawing_utils
```

### Step 2 - Image Capturing and Processing 

<div align = "justify">

The code below takes the image input from the webcam. It then converts the image from BGR to RGB. This is because MediaPipe only works with RGB images, not BGR.

It then processes the RGB image to identify the hands in the image:
  
</div>

```python
while True:
    success, image = cap.read()
    imageRGB = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    results = hands.process(imageRGB)
```

### Step 3 - Working with Each Hand

```python
    if results.multi_hand_landmarks:
        for handLms in results.multi_hand_landmarks:
            mpDraw.draw_landmarks(img, handLms, mpHands.HAND_CONNECTIONS)

    cv2.imshow("Image", img)

    if cv2.waitKey(1) == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()
```

<div align = "justify">

In the code above, we use the if statement to check whether a hand is detected. We then use the first for loop to enable us work with one hand at a time.

The second for loop helps us get the hand landmark information which will give us the x and y coordinates of each listed point in the hand landmark diagram.
  
</div>



