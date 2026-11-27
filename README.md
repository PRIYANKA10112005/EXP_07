# EXP_07
#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
image = cv2.imread('lan_img1.jpg.jpeg')
if image is None:
    raise FileNotFoundError("road.jpg was not found. Place road.jpg in the same folder as this notebook.")
```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(10,5))
plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis("off")

plt.tight_layout()
plt.show()
```

---

###  Step 5: Thresholding

```python
threshold = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)
```

---

###  Step 6: Region of Interest (ROI)

```python
height, width = threshold[1].shape

mask = np.zeros_like(threshold[1])

polygon = np.array([[
    (0, height),
    (width // 2 - 60, height // 2 + 60),
    (width // 2 + 60, height // 2 + 60),
    (width, height)
]], np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold[1], mask)
```

---

### Step 7: Edge Detection (Canny)

```python
edges = cv2.Canny(roi, 50, 150)
```

---

###  Step 8: Gaussian Blur

```python
blurred = cv2.GaussianBlur(edges, (5,5), 0)
```

---

###  Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(
    blurred,
    rho=1,
    theta=np.pi/180,
    threshold=50,
    minLineLength=50,
    maxLineGap=100
)
```

---

### Step 10: Lane Detection Logic

```python
line_image = np.zeros_like(image)

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line[0]
        cv2.line(line_image, (x1, y1), (x2, y2), (0, 255, 0), 5)

final_output = cv2.addWeighted(image, 0.8, line_image, 1.0, 0)
plt.figure(figsize=(16,10))

plt.subplot(2,4,1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(2,4,2)
plt.imshow(gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis("off")

plt.subplot(2,4,3)
plt.imshow(threshold[1], cmap='gray')
plt.title("Thresholded Image")
plt.axis("off")

plt.subplot(2,4,4)
plt.imshow(roi, cmap='gray')
plt.title("ROI Masked Image")
plt.axis("off")

plt.subplot(2,4,5)
plt.imshow(edges, cmap='gray')
plt.title("Edge Detected Image")
plt.axis("off")

plt.subplot(2,4,6)
plt.imshow(blurred, cmap='gray')
plt.title("Smoothed Image")
plt.axis("off")

plt.subplot(2,4,7)
plt.imshow(cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB))
plt.title("Detected Lines")
plt.axis("off")

plt.subplot(2,4,8)
plt.imshow(cv2.cvtColor(final_output, cv2.COLOR_BGR2RGB))
plt.title("Final Lane Detection Output")
plt.axis("off")

plt.tight_layout()
plt.show()
```

---

##  Expected Output

* Original image
* Grayscale image
* Thresholded image
* ROI masked image
* Edge detected image
* Smoothed image
* Detected lines
* Final lane detection output
<img width="1360" height="570" alt="image" src="https://github.com/user-attachments/assets/7ecd0a6b-29ba-48f2-9e2e-906701790a57" />


---

##  Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---

##  Developed By

* **Name:** ____________________________
* **Register No:** ______________________
