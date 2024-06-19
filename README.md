# Visual-Sensor-Fusion
Low-level and Mid-Level Visual Fusion of 3D LiDAR points with the 2D Object detection


* LiDAR Fusion with Vision
* Data taken from [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) Dataset
* Download Yolov4 model weights from [here](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights)

## Low-Level Fusion
### Yolo Detections
![vsf_1](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/5ad678f3-0cb4-4d05-9187-73af270d731f)


### Visualizing 3D LiDAR points in Open3D

![visualising_lildar](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/b444d058-b6f1-4811-b0bd-1ceb9b77387e)

### 3D Lidar Points Projected on the image plane
![33 (1)](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/0c174278-d194-412c-b92e-461dc39ec304)


### LiDAR points Fused with YOLO detections 
![vsf4](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/dcd53491-3943-4056-96d4-b3d7d824eeeb)




* LiDAR points are projected on the image using the camera intrinsic and extrinsic matrix.
* The points that lie within the detected 2D Bounding Box by YOLO are stored and the rest are ignored.
* There are some outliers inside bboxes that do not belong to that category, to reject these outliers there are several ways.
* One way is to shrink the bounding box size so that the points that absolutely belong to the desired objects are only considered.
* Another way is to use the Sigma Rule, i.e. include the points that are within 1 sigma or 2 sigma away from Gaussian mean, based on the distance of points.



## Mid-Level Fusion
### Yolo Detections
![vsf_5](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/72e3ce12-5f67-453c-935c-63032bc8ecad)



### LiDAR Points projected on Image
![vsf6](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/b18e0108-8403-4804-af95-84f3b580237f)


### 3D Bounding Boxes From LiDAR
![vsf8](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/d896e1ba-0437-4066-a74b-b95f0b1f7377)

### 3D BBox converted to 2D BBox

![lidar_2d](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/adba75cd-67b8-4713-87d6-b0ff56cdd1f6)


### LiDAR 2D BBox Fused with YOLO 2D BBox using Intersection Over Union

![vsf10](https://github.com/AnoushkaBaidya/Visual-Sensor-Fusion/assets/115124698/656a511f-db38-4da4-a1fc-9a1879c5b184)



* 2D Bboxes from LiDAR are associated with YOLO 2D Bboxes using [Hungarian](https://en.wikipedia.org/wiki/Hungarian_algorithm) Algorithm.
* Green Bounding Boxes are detected by YOLO whereas Blue Bounding Boxes are calculated using LiDAR points.
* YOLO missed 1 vehicle, whereas 2 vehicles are missed by LiDAR, one of which is half out of frame, at the bottom right side.

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


