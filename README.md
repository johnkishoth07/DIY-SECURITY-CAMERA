# DIY-SECURITY-CAMERA
this project is a basic real-time security system built using OpenCv and python. it uses a webcam to detect motion or a face and triggers a fast alarm using the winsound module. this simple setup demonstarates how computer vision can be applied in real-world security automatic systems
source-code:
import cv2 as cv
import numpy as np
import winsound
webcam = cv.VideoCapture(0)
while True:
    _,im1= webcam.read()
    _,im2=webcam.read()
    diff=cv.absdiff(im1,im2)
    gray= cv.cvtColor(diff, cv.COLOR_BGR2GRAY)
    _,thresh = cv.threshold(gray,20,255,cv.THRESH_BINARY)
    contours,_ = cv.findContours(thresh,cv.RETR_TREE,cv.CHAIN_APPROX_SIMPLE)
    for c in contours:
        if cv.contourArea(c) < 5000:
            continue
        winsound.Beep(900,100)
    cv.imshow("security camera", thresh)
    if cv.waitKey(10) == 27:
        break



webcam.release()
cv.destroyAllWindows()
