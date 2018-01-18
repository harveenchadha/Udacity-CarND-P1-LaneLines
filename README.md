# **Finding Lane Lines on the Road** 

## Pipeline Description
1. Convert the image to GrayScale
2. Apply Gaussian Filter to remove unwanted noise
3. Use Canny Edge Detection Algo to detect edges in the image
4. Clip the Region of Interest. Instead of using a triangle i preferred using a polygon.
5. Apply probalistic Hough Lines to get the set of points in your ROI that might create an edge according to the parameters specified
6. After getting the points we need to join the disconnected points using draw_line function. The function does the following steps:
      * Find the slope of all the points to distinguish between the left lane and right lane
      * To filter out horizontal looking points we will ignore points with slope less than 0.3
      * If the slope is negative the point belongs to left lane line
      * If the slope is positive the point belongs to right lane line
      * Once we have distinguished for left and right lane, we can find the line parameters using np.polyfit() method
      * Once we get the slope and intercept of the left and right lane we can find the X values in the equation y=mx+c
      * We are finding the X values because we already know the Y values
      * y_max is the bottom edge of ROI polygon
      * y_min is the top edge of ROI polygon
7. Performing Step 6 we will get the 2 points for both left and right lane
8. Draw line between two points on an empty image using cv2.line()
9. Merge the image obtained in Step 8 with the original Image.

## Shortcomings
1. May not work for curved lines
2. May not perform well if the road has bumps and the camera changes its position

## Possible Improvements
1. Will make it work for Challenge Video
2. Reduce Slight Flickering Effect.
