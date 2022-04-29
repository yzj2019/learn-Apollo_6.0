# Apollo/perception/camera部分

## 1、架构

### 1.1、整体架构

Apollo3.5~6.0，架构图好像就没有变过。。。

![perception_architecture](..\figs\architecture.png)

### 1.2、文件结构

```bash
D:\YZJ\APOLLO-6.0.0\MODULES\PERCEPTION\CAMERA
├─app
│  └─proto
├─common
│  └─proto
├─lib
│  ├─calibration_service
│  │  └─online_calibration_service
│  ├─calibrator
│  │  ├─common
│  │  └─laneline
│  ├─dummy
│      ├─proto
│      └─tracker
│          └─proto
├─test
└─tools
    ├─lane_detection
    ├─obstacle_detection
    │  ├─conf
    │  ├─data
    │  │  └─yolo
    │  └─params
    └─offline
```



### 1.3、根据架构设计的抽象接口类（类中方法为虚函数）：

camera/lib/interface

![perception_api](.\figs\api.png)

图片上的：

- 

图片以外的：

- base_init_options用于派生输入参数的接口
- base_camera_perception用于派生APP的接口
- base_inference_engine接口预留了，但未使用
- 接口预留但功能未开发：
  - base_landmark_detector
  - base_scene_parser(语义分割)
  - base_lane_tracker

## 2、具体实现

每个lib的具体实现（通过继承接口类设计的派生类）

架构图镇楼

![perception_implementation](.\figs\implementation.png)

## 3、APP类：将lib中的类组合成基本的功能类

camera/app

![perception_app](.\figs\app.png)



## 参考

- 架构：http://www.javashuo.com/article/p-ceqitjvz-st.html
- 感知部分，写的挺详细：https://blog.csdn.net/briblue/category_10670867.html

