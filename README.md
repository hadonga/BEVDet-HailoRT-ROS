
# BEVDet for HailoRT, C++, ROS2

This repository contains source code and models for BEVDet Lite version inference using HailoRT, ROS2 & C++.
Reference:
- [Yolo-HailoRT-ROS2](https://github.com/Ar-Ray-code/YOLO-HailoRT-ROS2)
- [bevdet-tensorrt-ros](https://github.com/linClubs/BEVDet-ROS-TensorRT)
- [bevdet-tensorrt-cpp](https://github.com/LCH1238/bevdet-tensorrt-cpp)
- [BEVDet](https://github.com/HuangJunJie2017/BEVDet)
- [mmdetection3d](https://github.com/open-mmlab/mmdetection3d)
- [nuScenes](https://www.nuscenes.org/)

<p align="center">
  <img src="./doc/1.gif" width="375" height="338" />
</p>

## BEVDet lite ver. 
  - Only Front-view image as input
  - Modify LSS 


# 1 Envornment setup

## 1.1 Automatic setup using docker (Recommended)
We provide the docker image including necessary dependcies.
  ~~~python
docker compose build
docker compose up
~~~
Requirements
HailoRT 4.17.0
ROS-Jazzy

## 1.2 Custom setup
- **ubuntu-20.04;CUDA-11.3; cuDNN-8.6.0; TensorRT-8.5.2.2; ROS1 Melodic**
- **yaml-cpp; Eigen3; libjpeg**

---

# 2 Build

~~~python
mkdir -p bev_ws/src
cd bev_ws/src
git clone https://github.com/linClubs/BEVDet-ROS-TensorRT.git
cd ..
catkin_make
source devel/setup.bash
~~~
---

# 3 Run
- **Generate TensorRT engine**

  Generate the onnx TensorRT engine 

  ~~~python
  python tools/export_engine.py cfgs/bevdet_lt_depth.yaml model/img_stage_lt_d.onnx model/bev_stage_lt_d.engine --postfix="_lt_d_fp16" --fp16=True
  ~~~

  Export engine in the path as follows.

  ~~~python
  # engine path
  BEVDet-ROS-TensorRT
      └──ckpts
          ├── bev_stage_lt_d.engine
          ├── img_stage_lt_d.engine
          └── lt_d.yaml
  ~~~

- **Data preparation**

  The rosbag folder can be downloaded from [Baidu Netdisk](https://pan.baidu.com/s/1f3nUnHa_4cd6FsRTV8YhkA?pwd=rjim)

- **Demo test**

  ~~~python

  # 1. start bevdet_node
  roslaunch bevdet bevdet_node.launch

  # 2  play data
  rosbag play nus.bag
  ~~~
---

# References


---
