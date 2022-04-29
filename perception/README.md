# Apollo/modules/perception部分

## 1、逻辑层级结构

从上到下

- Apollo/modules/perception所在层级：

  Apollo源码的文件结构是按照功能来组织的，比如perception部分代表的就是感知功能，而感知功能对应了好几个cyberRT-module

  perception目录结构如下：

  ```bash
  .
  ├── BUILD
  ├── base           // 整个感知部分公用的基础类，比如表示感知目标的Object
  ├── camera         // 相机相关            --- 子模块流程
  ├── common         // 公共目录，整个感知模块公用的一些基础操作定义，如点云预处理、图像预处理等；
  ├── data           // 感知模块用到的数据，目前只有相机的标定参数yaml文件；
  ├── fusion         // 传感器融合
  ├── inference      // 深度学习推理模块
  ├── lib            // 整个感知部分公用的算法库定义，如线程、时间、config_manager参数配置操作等
  ├── lidar          // 激光雷达相关         --- 子模块流程
  ├── map            // 高精度地图的一些操作，主要在感知模块中用于提取感兴趣区域；
  ├── model          // 深度学习模型
  ├── onboard        // 各个子模块的入口     --- 子模块入口
  ├── production     // 感知模块入口（深度学习模型也存放在这里）
                        --- 通过cyber启动子模块
  ├── proto          // 数据格式，protobuf
  ├── radar          // 毫米波               --- 子模块流程
  ├── testdata       // 上述几个模块的测试数据
  └── tool           // 离线测试工具
  ```

  下面介绍几个重要的目录结构:

  - production：感知部分各个cyberRT-module模块的入口在production目录，通过lanuch加载对应的dag，启动对应模块；感知模块包括多个cyberRT-module，在onboard目录中定义。
  - onboard：定义了多个component，分别用来处理不同的传感器信息（Lidar,Radar,Camera）；以及定义了各个component如何编译构建成各个cyberRT-module的。
  - inference：深度学习推理app，我们知道深度学习模型训练好了之后需要部署，而推理则是深度学习部署的过程，实际上部署的过程会对模型做加速，主要实现了caffe，TensorRT和paddlepaddle 3种模型部署。训练好的深度模型放在"modules\perception\production\data"目录中，然后通过推理app进行加载部署和在线计算。
  - camera：主要实现车道线识别，红绿灯检测，以及障碍物识别和追踪。
  - radar：主要实现障碍物识别和追踪（由于毫米波雷达上报的就是障碍物信息，这里主要是对障碍物做追踪）。
  - lidar：主要实现障碍物识别和追踪（对点云做分割，分类，识别等）。
  - fusion：对上述传感器的感知结果做融合。

  

- cyberRT-module层级，类似于ros-module：

  在perception/production中launch，一个launch文件可能会启动多个cyberRT-module；

  一个cyberRT-module对应一个`*.so`动态链接库，而一个`*.so`可能由多个component编译而成；

  perception/onboard中定义多个component，以及各个component如何编译构建成`*.so`的。

  

- component层级，可以理解为子模块：

  几个component可合并构建成一个cyberRT-module，也可能一个component构建一个cyberRT-module；

  component理解为编译前的源文件，主要是写数据流（数据的收发、各个app如何使用数据）：

  - header (*.h)：常量,结构,类型定义,函数,变量申明；
  - source (*.cc)：变量定义, 函数定义。
  - 是将不同app组合起来（include各个app的header，然后编译的时候链接各个app编译好的cc_library）

  

- app层级，功能类：

  到这一层就是源文件的编译时的结构了，再往下没必要分的那么细，最终都是作为header供component来include、cc_library共component编译时链接。

  - 有的app，如perception/msg_buffer，本身不复杂，就只有\*.cc、\*.h、BUILD三个文件；

  - 有的app，如perception/camera，构建比较复杂，有更进一步的结构：

    ```bash
    ├── app      	// zui'shang
    ├── common      // 
    ├── lib       	// 
    ├── test		// 
    ├── tools		// 
    ```

    











## 2、功能架构 / work flow

Apollo3.5~6.0，架构图好像就没有变过。。。

![perception_architecture](.\figs\architecture.png)



