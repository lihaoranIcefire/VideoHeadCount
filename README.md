# Lauretta ML Engineer Take-Home Test (Haoran Li)

## Problem Description

Giving a short video, we need roughly to count number of people showed up in the video.

## Methodology
1. We use **YOLOv7** for detecting people.
2. We use **DeepSort** realtime tracking people moving.

## Implementation

We implement this on Google Colab.

First we import relevant packages:
- `yolov7`
- `deep_sort_realtime`

and the dataset
- `bridge_photo.jpg`. A sample photo from the the video.
- `bridge_cut.mp4`. A cut of first and last few frames from the original video `bridge.mp4`.
- `bridge_cut_result.mp4`. is the processed video that contains bounding boxes

We then implement a single class `HeadCounter`, which has following methods
- initializer: initialize parameters, and initialize a tracker.
- process: build a yolo7 model that generates bounding boxes with confidence scores of objects. Return a list of bounding boxes with confidence scores and labels, a list of frames decorated by bounding boxes is returned, and a decorated video is exported to `runs/detect`.
- count_heads: gradually updating a tracker that only keeps track of people in real time, and finally return the total number of people ever showed up in the video.