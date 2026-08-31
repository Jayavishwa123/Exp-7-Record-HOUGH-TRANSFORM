# Exp-7-Record-HOUGH-TRANSFORM
# Name: Jaya Vishwa S
# Reg.No: 212224240120
# Aim
To detect lines in an image using the Hough Line Transform algorithm (cv2.HoughLinesP) and Canny Edge Detection in OpenCV, and to visualize the extracted lines on the original image.

# Requirements
Language: Python 3

Libraries:

opencv-python (cv2)

numpy

matplotlib

Input Data: A valid image file (e.g., rose.jpg).

# Procedure:
1.Import Libraries: Load OpenCV (cv2), NumPy (numpy), and Matplotlib (matplotlib.pyplot).
2.Load Image: Read the target image in BGR format using cv2.imread().
3.Pre-processing: Convert the BGR image to grayscale using cv2.cvtColor() for edge processing.
4.Edge Detection: Apply the Canny Edge Detector (cv2.Canny()) with appropriate upper and lower thresholds to extract edges.
5.Hough Line Transform: Apply cv2.HoughLinesP() on the binary edge image to detect line segments using probabilistic Hough transform parameters (resolution, threshold, minLineLength, maxLineGap).
6.Draw Lines: Verify line detection, iterate through the resulting endpoints
, and draw green lines onto the original image using cv2.line().
# Program:
```
# Step 1: Import required libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Load the image
image = cv2.imread('private.jpg')

# Step 3: Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Step 4: Display Input Image and Grayscale Image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Input Image")
plt.axis('off')
plt.show()

plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
plt.show()

# Step 5: Detect edges using Canny operator
edges = cv2.Canny(gray_image, 50, 150)

# Display Canny Edge Detector output
plt.imshow(edges, cmap='gray')
plt.title("Canny Edge Detector")
plt.axis('off')
plt.show()

# Step 6: Detect line coordinates using HoughLinesP
lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 100, minLineLength=50, maxLineGap=10)

# Step 7: Draw the lines on the original image
if lines is not None:
    for line in lines:
        if len(line.shape) > 1:
            x1, y1, x2, y2 = line[0]
        else:
            x1, y1, x2, y2 = line
        cv2.line(image, (int(x1), int(y1)), (int(x2), int(y2)), (0, 255, 0), 2)
else:
    print("No lines detected.")

# Step 8: Display the final result
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Result of Hough Transform")
plt.axis('off')
plt.show()
```
Output:
