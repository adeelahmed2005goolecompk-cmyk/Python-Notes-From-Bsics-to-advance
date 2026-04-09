# Python-Notes-From-Bsics-to-advance


## Here we starting the codes of python with outputs:


# 1st CODE-) WITH THEORY CODE:


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




# 2nd Code-) With Theory:


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


# THIS IS THE FULL CODE:


```Python Code:


import numpy as np
import cv2

# Read image (make sure file has extension like .jpg or .png.)
img = cv2.imread("A:/computer_Vision/602.jpg")

# Draw a rectangle.
cv2.rectangle(img, (50, 50), (200, 200), (0, 255, 0), -2)

# Draw a circle.
cv2.circle(img, (200, 200), 50, (255, 0, 0), -2)

# Draw a line.
cv2.line(img, (0, 0), (200, 200), (0, 0, 255), 2)

# DRAWING ARROWED LINE.
img = cv2.arrowedLine(img, (0, 125), (255, 255), (255, 0, 125), 3)

# Put text.
img = cv2.putText(img, "MR.SHAMEER", (20, img.shape[0]-20),
                  cv2.FONT_HERSHEY_SCRIPT_SIMPLEX, 1,
                  (0,125,255), 2, cv2.LINE_AA)

img = cv2.ellipse(img, (200, 200), (100, 50), 70, 70, 500, (155, 155, 155), -5)

#FOR FULL BLACK SCREEN.
# img = np.zeros([512, 512, 3], np.uint8)*255

# FOR FULL WHITE SCREEN.
img = np.ones([512, 512, 3], np.uint8)*255

# Show image.
cv2.imshow("Image", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```


# THIS IS THE OUTPUT IMAGE:


![Alt Text](602.jpg)



# 3rd CODE-) WITH THEORY:



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




# CODE NO 4-) WITH THEORY:


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









# CODE NO 5-) WITH THEORY:


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



# CODE NO 6-) WITH THEORY:


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





# CODE NO 7-) WITH THEORY:


## 4-IN-1 OpenCV CODE — THEORY:


***This program contains four different OpenCV codes. Each code demonstrates a different way of capturing, displaying, and saving video using Python and OpenCV.***


***CODE NO 1 — Video File Loading***


### Theory:


***This code is used to load and display a video file from your computer.
OpenCV reads the video frame by frame, resizes each frame, and shows it in a window.***


# How it works:


**cv2.VideoCapture() loads the video file
cap.read() reads frame by frame
cv2.resize() changes frame size
cv2.imshow() displays video
cv2.waitKey() controls playback speed
Press 'n' to exit**


# Purpose:


***This code teaches:***


**How to open a video file
How to process frames
How to display video using OpenCV**


# CODE NO 2 — Webcam Capture + Gray Conversion:


***Theory:***


***This code opens PC webcam and shows two frames:***


**Original color frame
Gray (black & white) frame.**


*It converts the webcam video into grayscale using OpenCV.*


***How it works:***


**VideoCapture(0) opens default webcam
cvtColor() converts color to gray
Two imshow() windows are created
Loop runs until user presses 'n'**


***Purpose:***


# This code teaches:


**How to open webcam
How to convert video to grayscale
How to show multiple windows:**


# CODE NO 3 — Mobile Camera Connection (IP Camera):


***Theory:***


**This code connects mobile camera to PC using IP address.
Both devices must be connected to same WiFi network.**


***Mobile camera streams video → PC receives → OpenCV displays and saves video.***


# How it works:


**Mobile IP camera URL used
cap.open(camera) connects mobile camera
VideoWriter() saves video
Frames resized and recorded
Press 'n' to stop recording.**


# Purpose:


## This code teaches:

**How to connect mobile camera
How to stream IP camera
How to record video to file**

# CODE NO 4 — YouTube Video Streaming:


***Theory:***


**This code is used to stream YouTube video using Python.
It uses pafy library to fetch YouTube stream and OpenCV to display it.**


# How it works:


**pafy.new(url) loads YouTube video
getbest() gets best video quality
OpenCV reads frames
Frames displayed and saved
Press 'n' to exit.**

# Purpose:


## This code teaches:


**How to stream YouTube video
How to capture online video
How to save streamed video
Overall Concept of All Codes**


***These four codes demonstrate:***


**Video file reading
Webcam capturing
Mobile camera streaming
YouTube video streaming**


# All codes use:


**OpenCV (cv2)
Frame processing
Video display
Video recording**



# THIS IS THE FULL CODE:


```Python Code:


# 4_in_1_code):-

# There we have 4 different code with a little bit of theory.

# SOME THEORY ABOUT THIS ALL CODE:


# CODE NO1):-

#IN THE FIRST CODEIS ABOUT VIDEO LOADING. 
#IN THIS CODE WRITTENED THAT HOW TO SHOW A VIDEO WITH CODING.


import cv2

cap = cv2.VideoCapture(r"A:\computer_Vision\2005.mp4")

while True:
    ret, frame = cap.read()
    if not ret:
        break
 
    frame = cv2.resize(frame, (700, 700))  # width, height
    # gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    cv2.imshow("frame", frame)
    # cv2.imshow("gray", gray)
    if cv2.waitKey(25) & 0xFF == ord('n'):
        break

cap.release()
cv2.destroyAllWindows()

# THIS CODE IS SHOWING THAT HOW TO OPEN THE PC'S WEB CAM AND 
# CONVERT IT INTO TWO DIFFERENT FRAMES 1 IS ORIGINAL AND 2 IS GRAY.

# CODE NO 2):-

import v2
cap = cv2.VideoCapture(0, cv2.CAP_DSHOW)
print(cap)

while cap.isOpened():
    ret, frame = cap.read()
    if ret:
        frame = cv2.resize(frame, (700, 600))
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

        cv2.imshow("frame", frame)
        cv2.imshow("gray", gray)

        if cv2.waitKey(1) & 0xFF == ord('n'):
            break
    else:
        break

cap.release()
cv2.destroyAllWindows()




# IN THIS CODE HAVE WRITTENED THAT HOW TO CONNECT YOUR PC WITH YOUR MOBILE PHONE.
# BUT THE MAIN POINT IS THAT YOUR PC AND MOBILE BOTH ARE CONNECTED WITH SAME NETWORK.
# FOR EXM:- WIFI OR PC CONNECT WITH MOBILE.

# connect your laptop and android device with the same network either wifi

# CODE NO 3):-
import cv2
camera = "http://192.168.100.4:8080/video"
cap = cv2.VideoCapture(0)
cap.open(camera)
print("check ===", cap.isOpened())

fourcc = cv2.VideoWriter_fourcc(*"XVID")
output = cv2.VideoWriter("A:\\KING.mp4", fourcc, 20.0, (700, 600))

while cap.isOpened():
    ret, frame = cap.read()
    if ret:
        frame = cv2.resize(frame, (700, 600))
        output.write(frame)
        cv2.imshow("color frame", frame)
        if cv2.waitKey(1) & 0xFF == ord('n'):
            break
    else:
        break

cap.release()
output.release()
cv2.destroyAllWindows()



# IN THIS CODE HAVE WRITTENED THAT HOW TO PLAY 
# LIVE VIDEO IN TO YOUTUBE WITH CODING.

# CODE NO 4):-

import cv2
import pafy

url = "https://www.youtube.com/watch?v=DIf8twwgDzw"

video = pafy.new(url)
best = video.getbest(preftype="mp4")

cap = cv2.VideoCapture(cv2.CAP_DSHOW)
print("check ===", cap.isOpened())

fourcc = cv2.VideoWriter_fourcc(*"XVID")
output = cv2.VideoWriter("A:\\KING.mp4", fourcc, 20.0, (700, 600))

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break

    frame = cv2.resize(frame, (700, 600))
    output.write(frame)
    cv2.imshow("color frame", frame)

    if cv2.waitKey(1) & 0xFF == ord('n'):
        break

cap.release()
output.release()
cv2.destroyAllWindows()

```



# CODE NO 8-) WITH THEORY:


## OFFLINE COLOR PICKER — SIMPLE THEORY:


***This code creates an offline color picker using Python, OpenCV, and NumPy.
It allows the user to select colors manually by adjusting R, G, and B trackbars.
The program shows a blank window, and when you move the sliders, the background color changes according to the selected values.***


# How This Code Works:


**1. Create Blank Image
img = np.zeros((300, 512, 3), np.uint8)
This creates a black image where colors will be displayed.**


# 2. Create Window:


**cv2.namedWindow("Color picker")
This Code creates a window named Color picker.**


# 3. Create ON/OFF Switch:


**cv2.createTrackbar(s1, "Color picker", 0, 1, cross)**


# This trackbar works like a switch:


**0 = OFF (black screen)
1 = ON (show selected color)
4. Create RGB Trackbars
cv2.createTrackbar("R", ...)
cv2.createTrackbar("G", ...)
cv2.createTrackbar("B", ...)**


# These trackbars control:


**Red color value
Green color value
Blue color value**


***Range: 0 to 255***


**5. Get Trackbar Values
r = cv2.getTrackbarPos("R", "Color picker")
g = cv2.getTrackbarPos("G", "Color picker")
b = cv2.getTrackbarPos("B", "Color picker")**


***This reads the slider values selected by user.***


**6. Apply Color to Image
img[:] = [b, g, r]**


**This fills the whole image with selected color.
OpenCV uses BGR format, not RGB.**


**7. Exit Condition
if k == 110:
    break**
    

*Press n key to close the window.*


***Purpose of This Code.***


# This code teaches:


**How to create trackbars in OpenCV
How to pick colors using sliders
How to create GUI in OpenCV
How RGB/BGR color system works**


***This is called Offline Color Picker because it works without camera or internet.***


# THIS IS THE FULL CODE:


# OFFLINE COLOR PICKER


```Python Code:


import cv2
import numpy as np

def cross(x):
    pass

# blank image
img = np.zeros((300, 512, 3), np.uint8)
cv2.namedWindow("Color picker")

# create switch
s1 = "0:OFF 1:ON"
cv2.createTrackbar(s1, "Color picker", 0, 1, cross)

# creating trackbars for colors
cv2.createTrackbar("R", "Color picker", 0, 255, cross)
cv2.createTrackbar("G", "Color picker", 0, 255, cross)
cv2.createTrackbar("B", "Color picker", 0, 255, cross)

while True:
    cv2.imshow("Color picker", img)
    k = cv2.waitKey(1) & 0xFF
    if k == 27:
        break

    # get trackbar positions
    s = cv2.getTrackbarPos(s1, "Color picker")
    r = cv2.getTrackbarPos("R", "Color picker")
    g = cv2.getTrackbarPos("G", "Color picker")
    b = cv2.getTrackbarPos("B", "Color picker")

    if s == 0:
        img[:] = 0
    else:
        img[:] = [b, g, r]   # OpenCV uses BGR

cv2.destroyAllWindows()
```

# THE UPPER CODE IS FOR CHOOSING OR CREATING  ANY TYPE OF COLOR, WHICH WOULD YOU WANT.






# CODE NO 9-) WITH THEORY:


# Detecting Everything by Webcam Using Trackbars:


***This code is used to detect objects by color using webcam.
It uses trackbars to adjust HSV color range and detect specific colored objects in real time.
The program captures webcam video, applies color filtering, and then draws contours around detected objects.***


# Step 1 — Webcam Capture:


***The code starts by opening the webcam using:***


**cap = cv2.VideoCapture(0)
It reads video frame by frame for processing.**


# Step 2 — Trackbars for Color Adjustment:


***Trackbars are created to control HSV color values.***


# Lower range trackbars:


**Lower_H → Hue minimum
Lower_S → Saturation minimum
Lower_V → Value minimum**


# Upper range trackbars:


**Upper_H → Hue maximum
Upper_S → Saturation maximum
Upper_V → Value maximum**


*These trackbars help select which color to detect.*


**Step 3 — Threshold Trackbar
cv2.createTrackbar("Thresh", ...)
This trackbar controls threshold value.
It helps remove noise and improve object detection.**


# Step 4 — Convert Frame to HSV:


**hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
The frame is converted from BGR to HSV because HSV makes color detection easier and more accurate.**


# Step 5 — Create Color Mask:


**mask = cv2.inRange(hsv, lower_bound, upper_bound)**


***This creates a binary mask:**


**White = detected color
Black = other colors
Step 6 — Filtered Image
filtr = cv2.bitwise_and(frame, frame, mask=mask)**


*This shows only the selected color from the frame.*


# Step 7 — Threshold and Dilation:


**Threshold removes noise
Dilation makes detected objects thicker**


**This improves contour detection accuracy.**


# Step 8 — Contour Detection:


**cv2.findContours()
Contours are detected around objects that match the selected color.**


# The code draws:


**Blue contour (object boundary)
Pink convex hull (smooth outer shape)
Step 9 — Output Windows**


# The program shows four windows:


**Mask → detected color only
Filtered → selected color from frame
Threshold → binary detection
Result → final contour detection
Purpose of This Code**


# This code teaches:


**Webcam color detection
HSV color filtering
Trackbars for real-time adjustment
Contour detection
Object detection by color**


# You can detect:


**red object
blue object
hand
ball
any colored object
Just adjust the trackbars.**


# THIS IS THE FULL CODE:


```Python Code:


DETECTING EVERYTING BY WEB CAM:


import cv2
import numpy as np

def nothing(x):
    pass

cap = cv2.VideoCapture(0)

cv2.namedWindow("Color Adjustments", cv2.WINDOW_NORMAL)
cv2.resizeWindow("Color Adjustments", 300, 300)

# Trackbars
cv2.createTrackbar("Lower_H", "Color Adjustments", 0, 179, nothing)
cv2.createTrackbar("Lower_S", "Color Adjustments", 48, 255, nothing)
cv2.createTrackbar("Lower_V", "Color Adjustments", 80, 255, nothing)

cv2.createTrackbar("Upper_H", "Color Adjustments", 20, 179, nothing)
cv2.createTrackbar("Upper_S", "Color Adjustments", 255, 255, nothing)
cv2.createTrackbar("Upper_V", "Color Adjustments", 255, 255, nothing)

cv2.createTrackbar("Thresh", "Color Adjustments", 200, 255, nothing)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    frame = cv2.resize(frame, (250, 250))
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

    # Trackbar values
    l_h = cv2.getTrackbarPos("Lower_H", "Color Adjustments")
    l_s = cv2.getTrackbarPos("Lower_S", "Color Adjustments")
    l_v = cv2.getTrackbarPos("Lower_V", "Color Adjustments")
    u_h = cv2.getTrackbarPos("Upper_H", "Color Adjustments")
    u_s = cv2.getTrackbarPos("Upper_S", "Color Adjustments")
    u_v = cv2.getTrackbarPos("Upper_V", "Color Adjustments")
    thresh_val = cv2.getTrackbarPos("Thresh", "Color Adjustments")

    lower_bound = np.array([l_h, l_s, l_v])
    upper_bound = np.array([u_h, u_s, u_v])

    # Mask and filtered image
    mask = cv2.inRange(hsv, lower_bound, upper_bound)
    filtr = cv2.bitwise_and(frame, frame, mask=mask)

    # Threshold and dilate
    mask_inv = cv2.bitwise_not(mask)
    _, thresh = cv2.threshold(mask_inv, thresh_val, 255, cv2.THRESH_BINARY)
    dilate = cv2.dilate(thresh, (3, 3), iterations=2)

    # Find contours
    cnts, _ = cv2.findContours(dilate, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
    result = frame.copy()

    # Draw contours and convex hulls
    for c in cnts:
        if cv2.contourArea(c) > 1000:
            epsilon = 0.0005 * cv2.arcLength(c, True)
            approx = cv2.approxPolyDP(c, epsilon, True)
            hull = cv2.convexHull(approx)

            # BLUE contours (thin)
            cv2.drawContours(result, [c], -1, (255, 0, 0), 1)

            # PINK convex hull (thin)
            cv2.drawContours(result, [hull], -1, (255, 0, 255), 1)

    # Show all windows
    cv2.imshow("Mask", cv2.resize(mask, (250, 250)))
    cv2.imshow("Filtered", cv2.resize(filtr, (250, 250)))
    cv2.imshow("Threshold", cv2.resize(thresh, (250, 250)))
    cv2.imshow("Result", cv2.resize(result, (250, 250)))

    key = cv2.waitKey(1) & 0xFF
    if key == 27:  # ESC key
        break

cap.release()
cv2.destroyAllWindows()
```


# IN THIS UPER CODE YOU HAVE DETECT ANYTHING BY WEBCAM LIVE.







# CODE NO 10-) WITH THEORY:


# Video Information Display (Date, Time, Width, Height):


***This code is used to play a video and display information on the screen.
It shows video width, height, current date, and time on each frame while the video is running.***


# Step 1 — Import Libraries:


**import cv2
import datetime
cv2 is used for video processing
datetime is used to get current date and time**


# Step 2 — Load Video File:


**cap = cv2.VideoCapture(r"A:\computer_Vision\2006.mp4")
This loads a video file from computer and prepares it for reading.**


# Step 3 — Get Video Width and Height:


**cap.get(3)  # width
cap.get(4)  # height**


***These functions return:***


**Width of video frame
Height of video frame
The values are printed in the console.**


# Step 4 — Read Video Frame by Frame:


**ret, frame = cap.read()
This reads the video frame by frame for processing and display.**


# Step 5 — Add Width and Height Text:


**cv2.putText(frame, text, (10, 30), font, 1, color, 2)
This displays video width and height on the frame using text.*


# Step 6 — Add Date and Time:


**datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
This gets the current system date and time and prints it on video.**


# Example:


***Date: 2026-04-09 12:35:20
Step 7 — Resize Frame
frame = cv2.resize(frame, (500, 600))
This resizes the video window to 500 × 600.***


# Step 8 — Display Video:


**cv2.imshow("frame", frame)
This shows the video with text overlay.**


# Step 9 — Exit Condition:


**if cv2.waitKey(10) & 0xFF == ord('n'):
Press 'enter' key to stop the video.**


*Purpose of This Code:*


# This code teaches:


**How to display video using OpenCV
How to show text on video
How to get video width and height
How to display date and time
How to resize video frames.**


# This is useful for:


***CCTV systems
Video monitoring
Video annotation
Computer vision projects.***


# THIS IS THE FULL CODE:


```Python Code:


import cv2
import datetime

cap = cv2.VideoCapture(r"A:\computer_Vision\2006.mp4")

print("Width====", cap.get(3))
print("Height====", cap.get(4))

while cap.isOpened():
    ret, frame = cap.read()
    if ret:
        font = cv2.FONT_HERSHEY_SCRIPT_COMPLEX
        
        text = 'Height: ' + str(int(cap.get(4))) + '  Width: ' + str(int(cap.get(3)))
        cv2.putText(frame, text, (10, 30), font, 1, (248, 117, 5), 2, cv2.LINE_AA)
        
        date_data = "Date: " + datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        cv2.putText(frame, date_data, (10, 70), font, 1, (247, 238, 5), 2, cv2.LINE_AA)
        
        frame = cv2.resize(frame, (500, 600))
        cv2.imshow("frame", frame)
        
        if cv2.waitKey(10) & 0xFF == ord('f'):
            break
    else:
        break

cap.release()
cv2.destroyAllWindows()
```
