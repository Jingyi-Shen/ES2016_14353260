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


### ROS:
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/*o9FZncBXC0xiO.FvthpG7dBiHJHJWNnVJlgEFWfuck!/b/dHABAAAAAAAA&bo=KAKbAAAAAAADAJQ!&rf=viewer_4&t=5"></div>


[1]: https://help.ubuntu.com/community/Repositories/Ubuntu
[2]: http://wiki.ros.org/ROS/Installation/UbuntuMirrors