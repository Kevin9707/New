This code is a program that uses OpenCV to read footage from a camera, apply sketch effects in real time, and save the sketched image.

Let's take a look at the code line by line.
It loads the Open Source Computer Vision Library (OpenCV) and numpy.The sketch function takes an image as input, converts it to grayscale, applies Gaussian blur, and performs canny edge detection. It then applies binarization (thresholding) to return an image consisting of black and white.Open a webcam and create a cam object.Use a while statement to make it repeat until the program ends.Use cam.read() to read a frame from the camera, and then input that frame into the sketch function to get an image with sketching effects.After that, use cv2.imshow() to show the image in a window called Live Sketch.

We use the cv2.waitKey() function to wait for keyboard input. Pressing the ESC key exits the while statement and exits the program. Pressing Enter saves the currently sketched image to a file and prints the message "Image Saved!!!" message to the cam object and closes all windows.

This code is a program that uses OpenCV to display an image from a webcam with sketch effects applied in real time, which can be saved as needed.



import cv2
import numpy as np
def sketch(image):
    gray = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
    blur_gray = cv2.GaussianBlur(gray,(5,5),900)
    edges = cv2.Canny(blur_gray,45,90)
    ret,thre = cv2.threshold(edges,70,255,cv2.THRESH_BINARY_INV)
    return thre
cam = cv2.VideoCapture(0)
while 1:
    ret,frame = cam.read()
    cv2.imshow('Live Sketch', sketch(frame))
    if cv2.waitKey(1)==27:
        break
    if cv2.waitKey(1)==13:
        cv2.imwrite('sketch.jpg',sketch(frame))
        print('Image Saved!!!')
cam.release()
cv2.destroyAllWindows()
