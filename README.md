# Video Head Count

## Problem Description

Giving a short video, we need roughly to count number of people showed up in the video.

## Methodology
1. We use **YOLOv7** for detecting people. YOLOv7 is a popular tool for object detecting, it is known for being efficient and accurate.
2. We use **DeepSort** realtime tracking people moving. DeepSort uses Kalman filters, which is powerful in predicting and estimating the motion of an object.

## Implementation

We implement this on Google Colab. Which is often most convenient for a relative small project like this.

First we import relevant packages:
- `yolov7`
- `deep_sort_realtime`

and the dataset
- `bridge_photo.jpg`. A sample photo from the the video.
- `bridge_cut.mp4`. A cut of first and last few frames from the original video `bridge.mp4`.
- `bridge_cut_result.mp4`. is the processed video that contains bounding boxes

We then implement a single class `HeadCounter`, so that everything is more streamlined. It has following methods
- `__init__`: initialize parameters, and initialize a tracker.
- `process`: build a yolo7 model that generates bounding boxes with confidence scores of objects. Return a list of bounding boxes with confidence scores and labels, a list of frames decorated by bounding boxes is returned, and a decorated video is exported to `runs/detect`.
- `count_heads`: gradually updating a tracker that only keeps track of people in real time, and finally return the total number of people ever showed up in the video.

I also tried a simple RCNN model, it is not as good as the yolov7. There could be some simplifications and customizations for the problem if given more time and data. For example, the model could be better trained with more specific footages, et.c.
