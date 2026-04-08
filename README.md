# Python-Notes-From-Bsics-to-advance


## Here we starting the codes of python with outputs:


# 1st WITH THEORY CODE:


# ADAPTIVE THRESHOLDING:


#We use it because simple thresholding is not able to handl. 
# differrent type of low luminous pixels.
# this is algorithm calculate the threshold for a small regions in same image.
#so we get multiple threshold for diff regions in same image. 

# Adaptive methode: it decides how thresholding value is calculated. 


***cv2.ADAPTIVE_THRESH_MEAN_C :
cv2.ADAPTIVE_THRESH_GAUSSIAN_C :
threshold(img,pixels_thresh,_max_thresh_pixel,method,style,no._of_pixel,contact_mean)***


***lets start:***


**Theory:**


Adaptive thresholding is an image processing technique used to convert a grayscale image into


a binary image by calculating different threshold values for different regions of the image instead of using one global value.


It’s widely used in computer vision tasks like text detection, pedestrian detection, and object segmentation.


# Basic Idea:


In normal (global) thresholding:


One single threshold value is applied to the entire image.


In adaptive thresholding:


The threshold is computed locally for each pixel using nearby pixels.


This works better when lighting is uneven.


# Why Adaptive Threshold is Needed?


Adaptive thresholding is useful when:


Lighting is not uniform
Shadows exist
Background brightness changes
Objects are partially illuminated


Global threshold fails in these cases, but adaptive threshold works well.


# Mathematical Theory:


For each pixel (x, y):


Binary image is computed as:


if I(x,y) > T(x,y) → pixel = 255


else → pixel = 0


I(x,y) = pixel intensity


T(x,y) = local threshold calculated from neighborhood


# Two Common Methods:


# ***1. Mean Adaptive Threshold:***


Threshold is the mean of neighboring pixels:


T(x,y) = mean(neighborhood) − C


neighborhood = block around pixel


C = constant (tuning value)


# ***2. Gaussian Adaptive Threshold:***


Threshold is weighted sum (Gaussian) of neighbors:


T(x,y) = gaussian_weighted_sum − C


This gives more importance to nearby pixels.


# Advantages:


Works with uneven lighting


Better edge detection


Good for real-world images


Useful for pedestrian detection preprocessing
# Disadvantages:



Slower than global threshold


Needs parameter tuning (block size, C)


Sensitive to noise


# Example Use Cases:


Document text extraction


License plate detection


Pedestrian silhouette detection


Medical image segmentation


***CODE SAMPLE:***

```Python Code:


import cv2
import numpy as np

img = cv2.imread(r"A:\computer_Vision\534.jpg", cv2.IMREAD_GRAYSCALE)

th1 = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)[1]

th2 = cv2.adaptiveThreshold(
    img,
    255,
    cv2.ADAPTIVE_THRESH_MEAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)

th3 = cv2.adaptiveThreshold(
    img,
    255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    11,
    2
)



cv2.imshow("image", img)
cv2.imshow("THRESH_BINARY", th1)
cv2.imshow("adaptive 1==", th2)
cv2.imshow("adaptive 2==", th3)



cv2.waitKey(0)
cv2.destroyAllWindows()
```


# THIS IS THE OUTPUT IMAGE:


![Alt Text](534.jpg)




# 2nd Code With Theory:


# Theory: Drawing Shapes and Text Using OpenCV in Python:


This program demonstrates how to draw geometric shapes and text on an image using the OpenCV library in Python. OpenCV provides built-in functions to draw primitives such as rectangles, circles, lines, arrows, ellipses, and text. These drawing operations are commonly used in computer vision for annotation, object detection visualization, and debugging.
The program first imports NumPy and OpenCV, which are required for image creation and manipulation.


***CODE WITH EVERY LINES INTRO:***


# codes intro:


import numpy as np
import cv2

*NumPy is used to create blank images, while OpenCV functions are used to draw shapes.*


***1. Reading an Image:***


**img = cv2.imread("A:/computer_Vision/602.jpg")**


**This function loads an image from disk into memory. The image is stored as a NumPy array where:
Height × Width × Channels
Channels represent BGR color format (Blue, Green, Red):**


# 2. Drawing Rectangle:


**cv2.rectangle(img, (50, 50), (200, 200), (0, 255, 0), -2)**


***Rectangle is drawn using:***


***Start point → (50, 50)
End point → (200, 200)
Color → (0,255,0) → Green
Thickness → -2 (filled rectangle)***


**The upper function is useful for bounding boxes in object detection.**


# 3. Drawing Circle:


**cv2.circle(img, (200, 200), 50, (255, 0, 0), -2)**


***Parameters:***


**Center → (200,200)
Radius → 50
Color → Blue (BGR format)
Thickness → -2 (filled circle
Circles are used for feature visualization and tracking points.**


# 4. Drawing Line:


**cv2.line(img, (0, 0), (200, 200), (0, 0, 255), 2)**


***Draws a line:***

***Start → top-left corner
End → (200,200)
Color → Red
Thickness → 2 pixels***

Lines are used for trajectory visualization.

# 5. Arrowed Line:


**img = cv2.arrowedLine(img, (0, 125), (255, 255), (255, 0, 125), 3)**

**This draws a directional arrow. It is commonly used to:**

**Show motion direction
Indicate object movement
Visualize vectors**


# 6. Putting Text:


**img = cv2.putText(img, "MR.SHAMEER", (20, img.shape[0]-20),
                  cv2.FONT_HERSHEY_SCRIPT_SIMPLEX, 1,
                  (0,125,255), 2, cv2.LINE_AA)**

**This upper function writes text on image:**


**Text → "MR.SHAMEER"
Position → bottom-left
Font → Script style
Font size → 1
Color → orange-like
Thickness → 2
LINE_AA → smooth text.**

**Used for:**

**labeling objects
watermarking
displaying info**


# 7. Drawing Ellipse:


**img = cv2.ellipse(img, (200, 200), (100, 50), 70, 70, 500, (155, 155, 155), -5)**


***Ellipse parameters:***


***Center → (200,200)
Axis lengths → (100,50)
Rotation → 70 degrees
Start angle → 70
End angle → 500
Color → gray
Thickness → filled
Ellipse is useful for object contour approximation.***


# 8. Creating Blank Image (Black)


**img = np.zeros([512, 512, 3], np.uint8)*255**


# This Function Creates black image:

**Size → 512 × 512
3 channels → color image
zeros → black background**


# 9. Creating Blank Image (White)


**img = np.ones([512, 512, 3], np.uint8)*255**


***This Code Has Creates white image:***


**ones × 255 → white background
Used for drawing shapes on blank canvas**


***THIS IS THE DISPLAY SIDE:***


# 10. Displaying Image:


cv2.imshow("Image", img)


# THIS IS THE LAST AND IMPORTTANT LINES OF EVERY CODE:


cv2.waitKey(0)
cv2.destroyAllWindows()

***These functions:***

**Show image window
Wait for key press
Close all windows**



# THIS IS THE OUTPUT IMAGE:


![Alt Text](602.jpg)



# 3rd CODE WITH THEORY:



# Theory: Background Removal Using Histogram Back Projection in OpenCV:


***This program demonstrates background removal using HSV color space, ROI histogram, and back projection. The goal is to extract objects that have similar color distribution as the selected ROI (Region of Interest) and remove the rest of the background.
This technique is widely used in object tracking, segmentation, and foreground extraction.***


# 1. Importing Libraries:


**import cv2
import numpy as np**


**OpenCV (cv2) is used for image processing
NumPy is used for matrix operations.**


# 2. Reading the Image:


**img = cv2.imread(r"A:\computer_Vision\920.jpg")
This loads the original image from disk. The image is stored in BGR color format.**


# 3. Resizing the Image:


**img = cv2.resize(img, (400, 400))**


***The image is resized to:
Width = 400
Height = 400
Resizing ensures consistent processing speed and reduces computation.***


# 4. Converting Image to HSV:


**hsv_original = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)**


***The image is converted from BGR to HSV color space.
HSV is preferred because:
Hue represents color
Saturation represents purity
Value represents brightness
HSV makes color-based segmentation more robust than RGB.***

# 5. Creating Region of Interest (ROI):
**roi = cv2.imread(r"A:\computer_Vision\bgr.jpg")
roi = cv2.resize(roi, (100, 100))
hsv_roi = cv2.cvtColor(roi, cv2.COLOR_BGR2HSV)**


**ROI is a small image containing the object color to be extracted.
This ROI acts as a reference for background removal.
Steps:
Load ROI image
Resize ROI
Convert ROI to HSV**


# 6. Creating Histogram of ROI:


**roi_hist = cv2.calcHist([hsv_roi], [0, 1], None, [180, 256],
                        [0, 180, 0, 256])**


***This calculates a 2D histogram using:
Channel 0 → Hue
Channel 1 → Saturation
The histogram represents color distribution of the object.***


# 7. Normalizing Histogram:


**cv2.normalize(roi_hist, roi_hist, 0, 255, cv2.NORM_MINMAX)**


***Histogram normalization:
Scales values between 0 and 255
Improves detection accuracy
Makes matching more stable
This step is important for better segmentation.***


# 8. Back Projection:


**mask = cv2.calcBackProject([hsv_original], [0, 1], roi_hist,
                           [0, 180, 0, 256], 1)**
                           

**Back projection finds pixels in original image that match ROI colors.**


# Output:


***Bright pixels → match ROI
Dark pixels → background
This produces a probability mask.***

# 9. Noise Filtering:


**kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
mask = cv2.filter2D(mask, -1, kernel)**


# Filtering:


**Removes small noise
Smooths mask
Improves segmentation
Elliptical kernel preserves object shape.**


# 10. Binary Thresholding:


**_, mask = cv2.threshold(mask, 200, 255, cv2.THRESH_BINARY)**


***Threshold converts mask to binary image:
White → objectBlack → background
This step removes weak matches.***


# 11. Merging Mask Channels:


**mask_3ch = cv2.merge([mask, mask, mask])**


***The mask is converted from:
1 channel → 3 channel
This is required for bitwise operation.***


# 12. Removing Background:


**result = cv2.bitwise_and(img, mask_3ch)**


***Bitwise AND keeps:
Object pixels → preserved
Background pixels → removed
This produces the final foreground image.***


# 13. Displaying Results:


**cv2.imshow("ORIGINAL IMAGE (BGR):", img)
cv2.imshow("HSV ORIGINAL IMAGE:", hsv_original)
cv2.imshow("ROI IMAGE (BGR):", roi)
cv2.imshow("HSV ROI IMAGE:", hsv_roi)
cv2.imshow("MASK IMAGE", mask)
cv2.imshow("RESULT IMAGE", result)**


# Displays:

***Original image
HSV image
ROI image
HSV ROI
Mask image
Final result
Conclusion***

*This program removes background using HSV histogram back projection. The ROI histogram is used to detect similar colors in the original image, and thresholding creates a mask that isolates the foreground object. This method is effective for color-based object extraction and tracking.*



# THIS IS THE FULL CODE


```Python:


            Removing the back ground in image


import cv2
import numpy as np

# READING THE IMAGE):-
img = cv2.imread(r"A:\computer_Vision\920.jpg")

# RESIZING THE IMAGE):-
img = cv2.resize(img, (400, 400))

# CONVERTING THE IMAGE INTO HSV):-
hsv_original = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# CREATING THE ROI):-
roi = cv2.imread(r"A:\computer_Vision\bgr.jpg")
roi = cv2.resize(roi, (100, 100))
hsv_roi = cv2.cvtColor(roi, cv2.COLOR_BGR2HSV)

# CREATING THE HISTOGRAM ROI):-
roi_hist = cv2.calcHist([hsv_roi], [0, 1], None, [180, 256],
                        [0, 180, 0, 256])

# NORMALIZE HISTOGRAM (IMPORTANT for better result)
cv2.normalize(roi_hist, roi_hist, 0, 255, cv2.NORM_MINMAX)

mask = cv2.calcBackProject([hsv_original], [0, 1], roi_hist,
                           [0, 180, 0, 256], 1)

# FILTERING AND REMOVING THE NOISE):-
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
mask = cv2.filter2D(mask, -1, kernel)

_, mask = cv2.threshold(mask, 200, 255, cv2.THRESH_BINARY)

# MERGING THE IMAGES):-
mask_3ch = cv2.merge([mask, mask, mask])
result = cv2.bitwise_and(img, mask_3ch)

# -----:(DISPLAY SIDE):-----

cv2.imshow("ORIGINAL IMAGE (BGR):", img)
cv2.imshow("HSV ORIGINAL IMAGE:", hsv_original)

cv2.imshow("ROI IMAGE (BGR):", roi)
cv2.imshow("HSV ROI IMAGE:", hsv_roi)

cv2.imshow("MASK IMAGE", mask)
cv2.imshow("RESULT IMAGE", result)

cv2.waitKey(0)
cv2.destroyAllWindows()
 
```


# THIS IS THE OUTPUT IMAGE:


![Alt Text](920.jpg)




# CODE NO 4 WITH THEORY:


# Theory: Bitwise Operations in OpenCV (AND, OR, NOT, XOR):



***Operations includes AND, OR, NOT, XOR.
It is more important and used for various purposes like making
and finding ROI (Region of Interest)***


***This program demonstrates bitwise operations in OpenCV. Bitwise operations are used to manipulate images at the pixel level. These operations are very important in image masking, background removal, and Region of Interest (ROI) extraction.
The basic bitwise operations used in image processing are:
AND
OR
NOT
XOR***


# 1. Importing Libraries:


***import cv2
import numpy as np
OpenCV (cv2) is used for image processing
NumPy is used to create blank images***


# 2. Creating Blank Images:


**img1 = np.zeros((250, 500, 3), np.uint8)
img2 = np.zeros((250, 500, 3), np.uint8)**


# Two black images are created:


***Height = 250 pixels
Width = 500 pixels
Channels = 3 (color image)
np.zeros() creates completely black images.***


# 3. Drawing Rectangles:


**img1 = cv2.rectangle(img1, (150, 100), (200, 250), (255, 255, 255), -1)
img2 = cv2.rectangle(img2, (10, 10), (170, 190), (255, 255, 255), -1)**


# Two white rectangles are drawn:

***White color → (255,255,255)
Thickness → -1 (filled)
These rectangles act as binary shapes for bitwise operations.***

# 4. Displaying Images:


**cv2.imshow("img1", img1)
cv2.imshow("img2", img2)**


***Displays both images before applying operations.
Bitwise Operations
Bitwise operations compare pixel values of two images.
White = 255
Black = 0***


# 5. Bitwise AND Operation:


**bitAnd = cv2.bitwise_and(img1,img2)**


# Logic:

***White + White → White
White + Black → Black
Black + White → Black
Black + Black → Black***


# Result:


**Only overlapping region remains white.**


# Used for:

***extracting common area
masking
ROI extraction***


# 6. Bitwise OR Operation:


**bitOr = cv2.bitwise_or(img1,img2)**


# Logic:


***White + White → White
White + Black → White
Black + White → White
Black + Black → Black***


# Result:


**Combined shapes appear.**


# Used for:


**merging masks
combining objects**


# 7. Bitwise NOT Operation:


**bitNot1 = cv2.bitwise_not(img1)
bitNot2 = cv2.bitwise_not(img2)**


# Logic:


**White → Black
Black → White**


# Result:


*Image colors are inverted.*

# Used for:

**background inversion
mask reversal**


# 8. Bitwise XOR Operation:


**bitXor = cv2.bitwise_xor(img1, img2)**


# Logic:

**White + White → Black
White + Black → White
Black + White → White
Black + Black → Black**


# Result:


**Only non-overlapping areas remain white.
This removes the common region and keeps different parts.**


# 9. Displaying XOR Result:


**cv2.imshow('bitXor', bitXor)**


*Shows XOR output image.*


# 10. Closing Windows


**cv2.waitKey(0)
cv2.destroyAllWindows()
waitKey(0) waits for key press
destroyAllWindows() closes windows**


# Conclusion:

***This program demonstrates how bitwise operations work on binary images. These operations are essential in computer vision for masking, ROI extraction, object segmentation, and image blending***



# THIS IS THE FULL CODE:


```Python Code:


import cv2
import numpy as np

# create blank images
img1 = np.zeros((250, 500, 3), np.uint8)
img2 = np.zeros((250, 500, 3), np.uint8)

# draw rectangles
img1 = cv2.rectangle(img1, (150, 100), (200, 250), (255, 255, 255), -1)
img2 = cv2.rectangle(img2, (10, 10), (170, 190), (255, 255, 255), -1)

# show images
cv2.imshow("img1", img1)
cv2.imshow("img2", img2)

# bitAnd operation

# bitAnd = cv2.bitwise_and(img1,img2)

# cv2.imshow('bitAnd',bitAnd)


# OR operation

# bitOr = cv2.bitwise_or(img1,img2)
# cv2.imshow('bitOr',bitOr)

# NOT operation

# bitNot1 = cv2.bitwise_not(img1)
# bitNot2 = cv2.bitwise_not(img2)

# cv2.imshow('bitNot1',bitNot1)
# cv2.imshow('bitNot2',bitNot2)

# XOR operation
bitXor = cv2.bitwise_xor(img1, img2)
cv2.imshow('bitXor', bitXor)


cv2.waitKey(0)
cv2.destroyAllWindows()
```


# THIS UPPER CODE HAS NO USES THE ANY TYPE OF IMAGE.









# CODE NO 5 WITH THEORY:


# ***Theory: Canny Edge Detection Using OpenCV (Two Methods)***


***This program demonstrates Canny Edge Detection using OpenCV. Canny edge detection is a widely used algorithm for detecting edges in an image. It detects sharp intensity changes and highlights object boundaries.
The algorithm was developed by John F. Canny (1986) and works using a multi-stage process.
Canny Edge Detection Steps***


# The Canny algorithm consists of the following stages:

# ***1. Noise Reduction:***


**Gaussian filter is applied
Removes noise from image
Prevents false edges.**


# 2. Gradient Calculation:


**Finds intensity change in image
Detects strong edges
Uses Sobel operators**


# 3. Non-Maximum Suppression:


**Removes unwanted thick edges
Keeps only thin edge lines**


# 4. Double Threshold:


**Uses two thresholds:
Low threshold
High threshold
Classifies edges as:
Strong edges
Weak edges
Non edges**


# 5. Edge Tracking by Hysteresis:


***Weak edges connected to strong edges are kept
Others are removed
This produces clean and accurate edge detection.***


# Method 1: Static Threshold Canny Edge Detection:


**img = cv2.imread(r"A:\computer_Vision\43.jpg")
img = cv2.resize(img, (250, 250))
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
canny = cv2.Canny(img_gray, 50, 150)**


# Explanation:


***Image is loaded and resized
Converted to grayscale
Canny edge detection applied with:
Threshold1 = 50
Threshold2 = 150
These thresholds are fixed values.
Edges are detected based on these constant limits.***


# Output Windows:


**cv2.imshow("Original Image:", img)
cv2.imshow("Gray Image:", img_gray)
cv2.imshow("Canny:", canny)**


# Displays:

**Original image
Grayscale image
Edge detected image**


# Method 2: Dynamic Threshold Using Trackbar:


*This method allows interactive threshold adjustment.*


# Creating Trackbars:


**cv2.namedWindow("Canny")
cv2.createTrackbar("Threshold", "Canny", 0, 255, nothing)**


**Trackbar is created to control threshold value.**


# Reading Trackbar Value:


**a = cv2.getTrackbarPos("Threshold", "Canny")**


***This reads current slider position.
Applying Canny Dynamically
res = cv2.Canny(img_gray, a, 255)
Lower threshold = trackbar value
Upper threshold = 255
This allows real-time edge tuning.
Loop for Continuous Update
while True:
The loop continuously:
Reads trackbar value
Applies Canny
Displays result
Exit Condition
k = cv2.waitKey(1) & 0xFF
if k == 110:
    break**


# Press n key to stop program:


***Difference Between Two Methods
Method	Threshold	Control	Use
Method 1	Fixed	No	Simple detection
Method 2	Dynamic	Yes	Interactive tuning
Applications of Canny Edge Detection
Object detection
Lane detection
Shape detection
Image segmentation
Medical image analysis
Feature extraction***


# Conclusion:


***This program demonstrates two methods of Canny edge detection. The first method uses fixed thresholds, while the second method uses a trackbar for interactive adjustment. Canny edge detection is an effective technique for detecting object boundaries and important image features.***


# THIS IS THE FULL CODE:


```Pthon Code:


                  # ----Canny edge detection----
# Cannye edge detection using open cv

# Canny edge detection is a popular edge detection approach.
# It is use multi-stage algorithm to detect a edge.
# It was developed by Jhon f. Canny in 1986.
# This approach combine with 5 steps.
# step no1):-Noise reduction (gauss,2) and (Gradient clacilation).
# step no2):-None maximum supperson,4) and (Double Threshold).
# step no3):-Edge tracking by Hystresis.
'''
import cv2
import numpy as np

img = cv2.imread(r"A:\computer_Vision\43.jpg")
img = cv2.resize(img, (250, 250))

# convert to grayscale
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Canny(img, threshold1, threshold2)
canny = cv2.Canny(img_gray, 50, 150)

cv2.imshow("Original Image:", img)
cv2.imshow("Gray Image:", img_gray)
cv2.imshow("Canny:", canny)
'''


import cv2
import numpy as np

img = cv2.imread(r"A:\computer_Vision\54.jpg")
img = cv2.resize(img, (250, 250))

# convert to grayscale
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

def nothing(x):
    pass

cv2.namedWindow("Canny")
cv2.createTrackbar("Threshold", "Canny", 0, 255, nothing)

while True:
    a = cv2.getTrackbarPos("Threshold", "Canny")
    res = cv2.Canny(img_gray, a, 255)

    cv2.imshow("Canny", res)

    k = cv2.waitKey(1) & 0xFF
    if k == 110:  # n key
        break

cv2.destroyAllWindows()
```

***THIS CODE HAS USES 2 IAMGES***


# THIS IS THE IMAGE NO 1:


![Alt Text](43.jpg)


# THIS IS THE IMAGE NO 2:


![Alt Text](54.jpg)



# CODE NO 6 WITH THEORY:


# Simple Theory: Contours and Its Functions (Two Methods):


***This program demonstrates contours and their functions in OpenCV. Contours are curves that join all continuous points having the same intensity. They are used for shape detection, object detection, and boundary extraction.***


# The code shows two methods:

*Method 1 → Contour Moments (Center detection)
Method 2 → Approximation and Convex Hull.*


# Step 1: Reading and Preprocessing Image:


***img = cv2.imread("shapes.png")
img = cv2.resize(img,(250, 250))
img1 = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
ret, thresh = cv2.threshold(img1, 250, 255, cv2.THRESH_BINARY_INV)***


# Steps:

*Read image
Resize image
Convert to grayscale
Apply binary threshold*


**Threshold converts image into black and white so contours can be detected easily.**


# Finding Contours:


***cnts, hier = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
cnts → list of contours
hier → hierarchy information
Each contour contains boundary points (x,y)
Contours represent object boundaries.***


# Method 1: Contour Moments (Center Detection):


**This method finds center of each contour using image moments.**


**M = cv2.moments(c)
cX = int(M["m10"] / M["m00"])
cY = int(M["m01"] / M["m00"])**


# Moment formula:

**m00 → area
m10, m01 → centroid calculation**


# Center is calculated as:

**cX = m10 / m00
cY = m01 / m00**


# Then center is drawn:


**cv2.circle(img,(cX,cY),3,(222,222,22),-1)**


# This method is used for:


**object center detection
tracking
shape analysis**


# Method 2: Approximation and Convex Hull:


**This method simplifies contour shape and finds bounding region.**

# 1. Contour Area:


***area = cv2.contourArea(c)
Calculates area of contour.**


# 2. Contour Approximation:


**epsilon = 0.01*cv2.arcLength(c,True)
data = cv2.approxPolyDP(c,epsilon,True)**

# Approximation:

**Reduces contour points
Simplifies shape
Helps identify shapes (triangle, square, etc.)**


# 3. Convex Hull:


**hull = cv2.convexHull(data)**


# Convex hull:

**Creates outer boundary
Removes concave parts
Makes contour smooth**


# Used for:


**shape correction
object detection
contour smoothing**


# 4. Bounding Rectangle:


**x,y,w,h = cv2.boundingRect(hull)
img = cv2.rectangle(img,(x,y),(x+w,y+h),(125, 10, 20), 1)**


# Draws rectangle around object


***Display Images:***


**cv2.imshow("original image:", img)
cv2.imshow("gray image:", img1)
cv2.imshow("thresh image:", thresh)**


# Shows:


**original image with contours
grayscale image
threshold image**


# Conclusion:


***This code demonstrates two contour methods. The first method uses moments to find the center of objects. The second method uses approximation and convex hull to simplify contours and draw bounding boxes. Contours are important for shape detection, object localization, and image analysis.***



# This Code Uses The Same Image Twice:


# THIS IS THE FULL CODE:


```Python Code:


Contours and its functoins:


#no1-) Moment. 
#no2-) Approximation.
#no3-) Convexhull


import cv2
import numpy as np

img = cv2.imread(r"A:\computer_Vision\shapes.png")
img = cv2.resize(img,(250, 250))
img1 = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
ret, thresh = cv2.threshold(img1, 250, 255, cv2.THRESH_BINARY_INV)

cnts, hier = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Here cnts is a list of contours and each contour is an array with x,y.
# hier variable is called hierarchy and it contains image information.
print("Number of contours:", len(cnts))
print("Contours:", cnts)
print("Hierarchy:", hier)

# draw contours):-
# img = cv2.drawContours(img, cnts, -1, (255, 20, 100), 2)

# loop over the contours):-
for c in cnts:
    # Compute the center of the center.
    # An image moment is a certain paticular wheighted average (moment) of the image.
    M = cv2.moments(c)
    if M["m00"] != 0:
        cX = int(M["m10"] / M["m00"])
        cY = int(M["m01"] / M["m00"])

        cv2.circle(img, (cX, cY), 3, (222, 222, 22), -1)
        cv2.putText(img, "Center", (cX - 20, cY - 10),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.3, (0, 255, 0), 1)

# DISPLAY SIDE):-

cv2.imshow("original image:", img)
cv2.imshow("gray image:", img1)
cv2.imshow("thresh image:", thresh)

cv2.waitKey(0)
cv2.destroyAllWindows()
```


# THIS IS THE 1ST OUTPUT OF IAMGE:


![Alt Text](shapes.png)





***now we read the Approximation and Convexhull.***


# THIS IS THE 2ND CODE:


```Python Code:


import cv2
import numpy as np

img = cv2.imread(r"A:\computer_Vision\shapes.png")
img = cv2.resize(img,(250, 250))
img1 = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
ret, thresh = cv2.threshold(img1, 250, 255, cv2.THRESH_BINARY_INV)

cnts, hier = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Here cnts is a list of contours and each contour is an array with x,y.
# hier variable is called hierarchy and it contains image information.
print("Number of contours:", len(cnts))
print("Contours:", cnts)
print("Hierarchy:", hier)

# draw contours):-
area1 = []
# img = cv2.drawContours(img, cnts, -1, (255, 20, 100), 2)
# loop over the contours):-
for c in cnts:
    # Compute the center of the center.
    # An image moment is a certain paticular wheighted average (moment) of the image.
    M = cv2.moments(c)
    if M["m00"] != 0:
        cX = int(M["m10"] / M["m00"])
        cY = int(M["m01"] / M["m00"])
        # find area of contour):-
        area = cv2.contourArea(c)
        area1.append(area)
            
# Contour Approx):-
        epsilon = 0.01*cv2.arcLength(c,True)
        data = cv2.approxPolyDP(c,epsilon,True)
# Convexhull is used to provide proper contours convexity.
        hull = cv2.convexHull(data)
        x,y,w,h = cv2.boundingRect(hull)
        img = cv2.rectangle(img,(x,y),(x+w,y+h),(125, 10, 20), 1)

        cv2.circle(img, (cX, cY), 3, (222, 222, 22), -1)
        cv2.putText(img, "Center", (cX - 20, cY - 10),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.3, (0, 255, 0), 1)

# DISPLAY SIDE):-

cv2.imshow("original image:", img)
cv2.imshow("gray image:", img1)
cv2.imshow("thresh image:", thresh)

cv2.waitKey(0)
cv2.destroyAllWindows()
```





