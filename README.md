# Visual-Sensor-Fusion
Low-level and Mid-Level Visual Fusion of 3D LiDAR points with the 2D Object detection


* LiDAR Fusion with Vision
* Data taken from [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) Dataset
* Download Yolov4 model weights from [here](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights)

## Low-Level Fusion
### Yolo Detections


### Visualizing 3D LiDAR points in Open3D


### 3D Lidar Points Projected on the image plane


### LiDAR points Fused with YOLO detections 




* LiDAR points are projected on the image using camera instrinsic and extrinsic matrix
* The points that lie within the detected 2D Bounding Box by YOLO are stored and rest are ignored
* There are some outliers inside bboxes that do not belong to that category, to reject these outliers there are several ways.
* One way is to shrink the bounding box size so that the points that absolutely belong to the desired objects are only considered.
* Another way is to use the Sigma Rule, i.e include the points that are within 1 sigma or 2 sigma away from gaussian mean, based on the distance of points



## Mid-Level Fusion
### Yolo Detections


### LiDAR Points projected on Image





### 3D BBox converted to 2D BBox





### LiDAR 2D BBox Fused with YOLO 2D BBox using Intersection Over Union




* 2D Bboxes from LiDAR are associated with YOLO 2D Bboxes using [Hungarian](https://en.wikipedia.org/wiki/Hungarian_algorithm) Algorithm
* Green Bounding Boxes are detected by YOlO whereas Blue Bounding Boxes are calculated using LiDAR points
* YOLO missed 1 vehicle, whereas 2 vehicles are missed by LiDAR, one of which is half out of frame, at the bottom right side

## File Structure
    .
    ├── Code
    |  ├── main.py
    |  ├── Fusion.py
    |  ├── Lidar2Camera.py
    |  ├── YoloDetector.py
    |  ├── Utils.py
    |  ├── FusionUtils.py
    |  ├── LidarUtils.py
    |  ├── YoloUtils.py
    ├── Data
       ├── calibs
       |  ├── 000031.txt
       |  ├── 000035.txt
       |  ├── ...
       ├── images
       |  ├── 000031.png
       |  ├── 000035.png 
       |  ├── ...
       ├── labels
       |  ├── 000031.txt
       |  ├── 000035.txt 
       |  ├── ...
       ├── models
          ├── yolov4
          |  ├── yolov4.cfg
          |  ├── coco.names
       ├── output
          ├── images
          ├── videos
       ├── points
       |  ├── 000031.pcd
       |  ├── 000035.pcd 
       |  ├── ...

### TODO
- [ ] Add Run Instructions
- [ ] Add Dependencies
- [ ] Add References
- [ ] High-Level Fusion
