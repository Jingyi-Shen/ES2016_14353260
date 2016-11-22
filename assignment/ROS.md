# ROS的安装
<br>

### ROS (Robot Operation System)
> ROS 的前身是斯坦福人工智能实验室为了支持斯坦福智能机器人STAIR而建立的交换庭 (switchyard）项目。<br> <br>ROS提供一些标准操作系统服务，例如硬件抽象，底层设备控制，常用功能实现，进程间消息以及数据包管理。<br><br>ROS是基于一种图状架构，从而不同节点的进程能接受，发布，聚合各种信息（例如传感，控制，状态，规划等等）。目前ROS主要支持Ubuntu。<br><br>ROS可以分成两层，低层是上面描述的操作系统层，高层则是广大用户群贡献的实现不同功能的各种软件包，例如定位绘图，行动规划，感知，模拟等等。
我们主要需要用它的仿真功能。


<br>
## Ubuntu install of ROS Jade

### 1. Configure your Ubuntu repositories<br>
Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse." You can  [follow the Ubuntu guide][1] for instructions on doing this.
 
### 2. Setup your sources.list<br>
Setup your computer to accept software from packages.ros.org. ROS Jade ONLY supports Trusty (14.04), Utopic (14.10) and Vivid (15.04) for debian packages.

  ```$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list```<br>
  [Mirrors][2]

### 3. Set up your keys<br>
```$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116```

### 4. Installation
   First, make sure your Debian package index is up-to-date:<br>
```$ sudo apt-get update```
   
  Then, try installing just this to fix dependency issues:<br>
```$ sudo apt-get install libgl1-mesa-dev-lts-utopic```

  There are many different libraries and tools in ROS. Provided four default configurations to get you started:

+ <strong>Desktop-Full Install (Recommended) :</strong> ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception<br>
	 ```$ sudo apt-get install ros-jade-desktop-full```

+ <strong>Desktop Install :</strong> ROS, rqt, rviz, and robot-generic libraries<br>
	 ```$ sudo apt-get install ros-jade-desktop```

+ <strong>ROS-Base (Bare Bones) :</strong> ROS package, build, and communication libraries. No GUI tools.<br>
	 ```$ sudo apt-get install ros-jade-ros-base```

+ <strong>Individual Package: </strong> You can also install a specific ROS package (replace underscores with dashes of the package name)<br>
	 ```$ sudo apt-get install ros-jade-PACKAGE```

To find available packages :<br>
    ```$ apt-cache search ros-jade```
<br>
 <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/dXy8esJ.zVNPx.smyK0rFCNOhCt*7725Dd1X1aHRv.g!/b/dAkBAAAAAAAA&bo=1gLOAQAAAAADAD4!&rf=viewer_4&t=5"></div>

### 5. Initialize rosdep
  Before you can use ROS, you will need to initialize *rosdep*. *rosdep* enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS.

  ```$ sudo rosdep init```<br>
  ```$ rosdep update```

### 6. Environment setup
  It's convenient if the ROS environment variables are automatically added to bash session every time a new shell is launched:

  ```$ echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc```<br>
  ```$ source ~/.bashrc```

  If you have more than one ROS distribution installed, ```~/.bashrc``` must only source the ```setup.bash``` for the version you are currently using.

  ps:If just want to change the environment of your current shell, then type:

  ```$ source /opt/ros/jade/setup.bash```

<br>
## Catographer安装:

### 1.安装所有依赖项
   ```$ sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev ``` 
   ```liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler``` 
   ```python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev```

### 2.安装ceres-solver
这里直接使用 hitcm 的代码，先在 home 目录下新建文件夹，命名为 catkin_ws ,打开终端进入该文件的目录下：<br>
   ```$ mkdir catkin_ws```<br>
   ```$ cd catkin_ws```

执行以下代码:<br>
   ```$ git clone https://github.com/hitcm/ceres-solver-1.11.0.git  ```

之后，打开 catkin_ws 文件夹，可以看到名字为 ceres-solver-1.11.0 的文件夹，进入 ceres-solver-1.11.0 ，新建文件夹 build ,在终端进入到该目录下：<br>
   ```$ ls catkin_ws```<br>
   ```$ cd  ceres-solver-1.11.0```<br>
   ```$ mkdir build```
   ```$ cd build```

在该目录下执行:<br>
   ```$ cmake ..```<br>
   ```$ make -j3```<br>
   ```$ sudo make install```<br>

安装ceres-solver截图：
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/g1Mr5WRk7lNgNumZUTN5k*6nf1dVM.4z0EeydZVXsQ4!/b/dAwBAAAAAAAA&bo=jAJLAgAAAAADAOI!&rf=viewer_4&t=5"></div>

### 3.安装cartographer
在catkin_ws下新建文件夹 cartographer，在终端进入该目录下，执行:<br>
   ```$ git clone https://github.com/hitcm/cartographer.git```

执行结束后可以看到一个 cartographer 文件夹,在里面新建 build 文件夹，并进入该路径下：<br>
   ```$ cd cartographer/build```			

进入后，依次执行:<br>
   ```$ cmake ..```<br>
   ```$ make```<br>
   ```$ sudo make install```<br>

安装 cartographer 结束截图：<br>
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/GCoYpU7AOwRFRm663QNR.k5GZi9hTGgcSdRN4X1MgWw!/b/dHwBAAAAAAAA&bo=9QJYAgAAAAADAIg!&rf=viewer_4&t=5"></div>

### 4.安装cartographer_ros
在catkin_ws新建src文件夹，进入此文件夹：<br>
   ```$ mkdir src```<br>
   ```$ cd src```

在src文件夹执行：<br>
   ```$ git clone https://github.com/hitcm/cartographer_ros.git```

最后，在catkin_ws下执行：<br>
   ```$ catkin_make```<br>

安装结束截图：<br>
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/GM41*EEFyH9fARsUsx2d*R7VGwZSG*y.3E2vu5f6LoU!/b/dHcBAAAAAAAA&bo=AANAAgAAAAADAGQ!&rf=viewer_4&t=5"></div>

<br>

## Catographer安装出现的问题以及解决：
错误的主要原因是 ros 的 catkin_ws 配置问题，出现问题如下：<br>
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/zmv4k9VCL3VzogQmdSPMQaHh2Q28*nqF2ZaIg7sjthM!/b/dNwAAAAAAAAA&bo=7AKVAAAAAAADAF4!&rf=viewer_4&t=5"></div>
<br>
第一种解决办法：（这个办法我失败了）<br>
   ```$ rospack profile```
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/ki5WlWWrH2UutYXQrGqo2gWEgXcPnJaMzegyu5Z4rEQ!/b/dHwBAAAAAAAA&bo=6AIcAQAAAAADANI!&rf=viewer_4&t=5"></div>
<br>
第二种解决办法：（还是失败）<br>
   ```$ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc```
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/eeyQz3e8ofcD7ZJxE8GjNm6wP*lscQD3EpHcMWdc6hc!/b/dAoBAAAAAAAA&bo=6AInAAAAAAADAOg!&rf=viewer_4&t=5"></div>
<br>
第三种解决办法：（成功解决）<br>
   ```$ source ~/catkin_ws/devel/setup.bash```
   ```$ rospack profile```
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/YuB2X5AAgt6X8*7SqxR8t0EjxLsCy9ddrehhG.uCyqY!/b/dAoBAAAAAAAA&bo=FAO3AQAAAAADAIQ!&rf=viewer_4&t=5"></div>
<br>
### 运行2D结果：

<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/H.9.URuX4L402vp19AvLtOBAUBMgBhc5WTuA7lLlb*U!/b/dHcBAAAAAAAA&bo=MwNIAgAAAAADAF8!&rf=viewer_4&t=5"></div>


[1]: https://help.ubuntu.com/community/Repositories/Ubuntu
[2]: http://wiki.ros.org/ROS/Installation/UbuntuMirrors