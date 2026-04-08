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


# THIS IS THE OUTPUT:


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



# THIS IS THE OUTPUT IAGE:


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


# THIS IS THE OUTPUT:


![Alt Text](290.jpg)


