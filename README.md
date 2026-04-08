# Python-Notes-From-Bsics-to-advance


# Python Codes With Bsics To Advance.


## Here we starting the codes of python with outputs:



# ADAPTIVE THRESHOLDING
#We use it because simple thresholding is not able to handl. 
# differrent type of low luminous pixels.
# this is algorithm calculate the threshold for a small regions in same image.
#so we get multiple threshold for diff regions in same image. 

#Adaptive methode: it decides how thresholding value is calculated. 
# cv2.ADAPTIVE_THRESH_MEAN_C :
# cv2.ADAPTIVE_THRESH_GAUSSIAN_C :
# threshold(img,pixels_thresh,_max_thresh_pixel,method,style,no._of_pixel,contact_mean)


***lets start:***


***1st Code:***


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


***Mathematical Theory:***


For each pixel (x, y):


Binary image is computed as:


if I(x,y) > T(x,y) → pixel = 255


else → pixel = 0


Where:


I(x,y) = pixel intensity


T(x,y) = local threshold calculated from neighborhood


***Two Common Methods:***


**1. Mean Adaptive Threshold**


Threshold is the mean of neighboring pixels:


T(x,y) = mean(neighborhood) − C


Where:


neighborhood = block around pixel


C = constant (tuning value)


2. Gaussian Adaptive Threshold


Threshold is weighted sum (Gaussian) of neighbors:


T(x,y) = gaussian_weighted_sum − C


This gives more importance to nearby pixels.


***Advantages:***


Works with uneven lighting


Better edge detection


Good for real-world images


Useful for pedestrian detection preprocessing
***Disadvantages:***



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


![Alt Text](images/534.jpg)



