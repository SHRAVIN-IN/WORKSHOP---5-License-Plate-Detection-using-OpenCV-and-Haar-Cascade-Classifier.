---

# WorkShop 5 - License Plate Detection and Blurring using OpenCV

## Name : JANA SHRAVIN S
## Regno : 212224243003
## Aim
To build a Python program that automatically detects license plates in images using Haar Cascade Classifiers, draws a bounding rectangle around the detected plate, and applies a median blur to anonymize the plate number.

---

## Software Required
* **Python 3.x**
* **Jupyter Notebook** or any Python IDE (VS Code, PyCharm, etc.)
* **OpenCV (`opencv-python`)**
* **Matplotlib**
* **NumPy**

### Installation
If the required libraries are not installed, run:
```bash
pip install opencv-python matplotlib numpy

```

---

## Algorithm (Step-by-Step Process)

1. **Environment Setup & Imports**: Import the necessary libraries (`cv2`, `matplotlib.pyplot`, `numpy`).
2. **Image Loading**: Read the input car image (`car_plate.jpg`) using OpenCV's `cv2.imread()`.
3. **Display Helper Function**: Create a custom function utilizing Matplotlib to convert the image from BGR to RGB format and render it clearly.
4. **Load Trained Classifier**: Load the pre-trained Haar Cascade model (`haarcascade_russian_plate_number.xml`) using `cv2.CascadeClassifier()`.
5. **Detection & Processing**:
* Pass the image to `detectMultiScale()` to get bounding coordinates `(x, y, w, h)` of any detected license plates.
* **Task A (Bounding Box)**: Draw a red rectangle over the detected coordinates using `cv2.rectangle()`.
* **Task B (Blurring & Box)**: Extract the Region of Interest (ROI) corresponding to the license plate, apply `cv2.medianBlur()`, replace the original area with the blurred ROI, and draw a bounding rectangle around it.
6. **Visualization**: Call the display function to plot and review the final output images.

---
## Program
```py
import matplotlib.pyplot as plt
import cv2
import numpy as np
```
```py
# Read the image using OpenCV
img = cv2.imread('car_plate.jpg')
def display(img, cmap=None):
    # Convert BGR (OpenCV format) to RGB (Matplotlib format)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    
    # Create a larger figure
    fig = plt.figure(figsize=(10, 8))
    ax = fig.add_subplot(111)
    
    # Display the image
    ax.imshow(img_rgb, cmap=cmap)
display(img)
```
```py
# Load the pre-trained Haar Cascade XML file for license plates
plate_cascade = cv2.CascadeClassifier('haarcascade_licence_plate_rus_16stages.xml')
```
```py
def detect_and_draw_rectangle(image):
    # Copy the image to avoid overwriting the original
    plate_img = image.copy()
    
    # Detect license plate coordinates
    plate_rects = plate_cascade.detectMultiScale(
        plate_img, 
        scaleFactor=1.3, 
        minNeighbors=3
    )
    
    # Draw rectangle around each detected plate
    for (x, y, w, h) in plate_rects:
        # cv2.rectangle(image, top_left, bottom_right, color_in_BGR, thickness)
        cv2.rectangle(plate_img, (x, y), (x + w, y + h), (0, 0, 255), 4)
        
    return plate_img
display(result)
```
```py
def detect_blur_and_draw_rectangle(image):
    # Copy the image to avoid overwriting the original
    plate_img = image.copy()
    
    # Detect license plate coordinates
    plate_rects = plate_cascade.detectMultiScale(
        plate_img, 
        scaleFactor=1.3, 
        minNeighbors=3
    )
    
    for (x, y, w, h) in plate_rects:
        # 1. Extract the Region of Interest (ROI)
        roi = plate_img[y:y+h, x:x+w]
        
        # 2. Apply median blur to the ROI
        blurred_roi = cv2.medianBlur(roi, 25)
        
        # 3. Paste the blurred region back onto the image
        plate_img[y:y+h, x:x+w] = blurred_roi
        
        # 4. Draw a red rectangle over the blurred area
        cv2.rectangle(plate_img, (x, y), (x + w, y + h), (0, 0, 255), 4)
        
    return plate_img
result = detect_and_blur_plate(img)
display(result)
```

## Output Images

### Original Image

<img width="1027" height="552" alt="image" src="https://github.com/user-attachments/assets/5d618236-8aef-431e-9522-41d8e0783891" />

### Task 1: Detected License Plate with Rectangle

<img width="727" height="417" alt="image" src="https://github.com/user-attachments/assets/144f5f6d-ad17-4683-a3e1-a1dcf651e36d" />

### Task 2: Detected License Plate with Blur and Rectangle

<img width="703" height="397" alt="image" src="https://github.com/user-attachments/assets/86d948b7-9869-4bac-b8f2-2a985c047ba0" />

---

## Result

The project has been executed properly. The license plate was successfully detected, framed with a bounding rectangle, and blurred to preserve vehicle privacy using OpenCV.


Would you like to add any specific project details, such as video stream processing or additional anonymization techniques?

```
