# video-to-image-using-opencv
Video to image conversion using python and OpenCV
## Install Python 
[Download Python](https://www.python.org/downloads/)

## Install Open CV
``pip3 install opencv-python``

### Create a script to convert images from video frames

```
import cv2
vidcap = cv2.VideoCapture('video.mp4')
def getFrame(sec):
    vidcap.set(cv2.CAP_PROP_POS_MSEC,sec*1000)
    hasFrames,image = vidcap.read()
    if hasFrames:
        cv2.imwrite("./images/image"+str(count)+".jpg", image)
    return hasFrames
sec = 0
frameRate = 0.5 #//it will capture image in each 0.5 second
count=1
success = getFrame(sec)
while success:
    count = count + 1
    sec = sec + frameRate
    sec = round(sec, 2)
    success = getFrame(sec)
```
Thde images will save in the ``./images/`` direcotry


### Let's create a script which convert images into video with each images per frame

```
import cv2
import numpy as np
import os
from os.path import isfile, join
pathIn= './images/'
pathOut = './videos/newvideo.avi'
fps = 0.5
frame_array = []
files = [f for f in os.listdir(pathIn) if isfile(join(pathIn, f))]
#for sorting the file names properly
files.sort(key = lambda x: x[5:-4])
files.sort()
frame_array = []
files = [f for f in os.listdir(pathIn) if isfile(join(pathIn, f))]
files.sort(key = lambda x: x[5:-4])
for i in range(len(files)):
    filename=pathIn + files[i]
    img = cv2.imread(filename)
    height, width, layers = img.shape
    size = (width,height)
    frame_array.append(img)
out = cv2.VideoWriter(pathOut,cv2.VideoWriter_fourcc(*'DIVX'), fps, size)
for i in range(len(frame_array)):
    out.write(frame_array[i])
out.release()
```
Thde out put video will save in the ``./videos/`` direcotry


