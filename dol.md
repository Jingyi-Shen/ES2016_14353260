# Description

> The **distributed operation layer (DOL)** is a software development framework to program parallel applications. 


<br>
##Example 1

### 如何修改
example1 包含三个部分，生产者、消费者和平方模块，还有两条通道c1，c2。<br>
原本的 example1 的工作是生产者产生 0~19 的整数(长度为20)，平方模块对输入信号进行平方操作，最后由消费者输出结果。<br>
为了实现使其输出三次方数，我们需要修改平方模块的 **square_fire** 信号处理函数，对参数i由 i\*i 修改为 i\*i\*i ，使得对生产者输入端的信号做立方操作后再写出到输出端。

### 实验截图

* 修改之前的 .dot 截图
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/V0zsI2eesNf3QFPbpO1y2VOkd0K4XXNUKkq5VRweMuE!/b/dAkBAAAAAAAA&bo=AgK8AAAAAAADAJk!&rf=viewer_4&t=5"></div>
* 修改之后的 .dot 截图 (待修改 sauqre->cubic)
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/V0zsI2eesNf3QFPbpO1y2VOkd0K4XXNUKkq5VRweMuE!/b/dAkBAAAAAAAA&bo=AgK8AAAAAAADAJk!&rf=viewer_4&t=5"></div>
* square.c，原始代码：
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/FCs8wpW0p3d4spd9Si.eUHddBPy0r3eG2t2HC7Xr0zg!/b/dHIBAAAAAAAA&bo=DQLhAQAAAAADAMo!&rf=viewer_4&t=5"></div>
* square.c，修改如下：
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/WdCRPQSvdtzxJQ2aXyAGv*AYbEW4IYYvVKF.KlLTyjc!/b/dHcBAAAAAAAA&bo=*wHrAQAAAAADADE!&rf=viewer_4&t=5"></div>
* 修改之前的结果截图
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/bIj.7sWARnKMaS00DgC*IPZnIN5C2K9AH6iNS1TcEFE!/b/dAoBAAAAAAAA&bo=LgIBAgAAAAADAAo!&rf=viewer_4&t=5"></div>
* 修改之后的结果截图 
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/SBhrlBDa0DVF1OfywC9H2i1eSUe7sO6u2PfyCFILgtM!/b/dHcBAAAAAAAA&bo=NQLJAQAAAAADANo!&rf=viewer_4&t=5"></div>

---
<br>
##Example 2

### 如何修改
example2 也是包含三个部分，生产者、消费者和平方模块，还有三条通道c2_0，c2_1，c2_2。<br>与 example1 不同的是，example2 架构中包含了三个 square 进程。生产者产生 0~19 的整数(长度为20)，三个平方模块对输入信号进行三次平方操作，最后由消费者输出结果。<br>
为了实现将三个 square 进程变为两个，我们需要在 **xml** 布局中修改产生平方模块的迭代次数 **iterator**，将迭代次数 (N的值) 由 3 修改为 2。

### 实验截图

* 修改之前的 .dot 截图
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/7HMrn7jiLTj5O97OxiHqvE5V.U4ZAih5Ih889RKpTJg!/b/dAwBAAAAAAAA&bo=jwJZAAAAAAADAPE!&rf=viewer_4&t=5"></div>
* 修改之后的 .dot 截图
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/KPkz8ARtVUneh7wyOaIWUAiCiIkBaYa5Rdv4gRdT0pQ!/b/dHcBAAAAAAAA&bo=.wFzAAAAAAADAKw!&rf=viewer_4&t=5"></div>
* xml，原始代码：
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/2h6nUzezNJvEC4nx6sxmpD8e5BAxUbIpoTpxjbV3Jko!/b/dAoBAAAAAAAA&bo=kAKIAQAAAAADAD4!&rf=viewer_4&t=5"></div>
* xml，修改如下：
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/ORbxLI6nqtdHE04ZTI41yzklF15U6dB6MRaek3M*08Q!/b/dAoBAAAAAAAA&bo=xQE7AQAAAAADANs!&rf=viewer_4&t=5"></div>
* 修改之前的 结果截图
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/bew*5O.Uizmg8zTz.0axYQjOEdm.*b1LpEvo5HDsC4w!/b/dOEAAAAAAAAA&bo=dwHEAQAAAAADAJY!&rf=viewer_4&t=5"></div>
* 修改之后的 结果截图
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/MSgqJUCve4r3CvTG.BkEwZQKEATpeQYWKgYJmXckobI!/b/dK4AAAAAAAAA&bo=wgG2AQAAAAADAFE!&rf=viewer_4&t=5"></div>
---

##实验感想
* 每次修改 example 的代码之后，需要再次运行之前，要将之前生成的文件夹删去。 <br> 比如下图，删去 ```/home/dol/build/bin/main``` 路径下的 example 文件夹。<br>
 <div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/AIpGYk7nWZnOw3JHgGrXjWZjwSirCZVMEaweBeqggT8!/b/dHwBAAAAAAAA&bo=YwLnAAAAAAADAKM!&rf=viewer_4&t=5"></div>

* 实验开始之前，要先理解代码中实现的各个模块的意义。<br>
xml 文件用于定义模块之间的连接方式。 process 是进程模块，sw_channel 是模块之间的通道，connection 把进程框和通道线连接起来。<br>
.c和.h文件是对模块的功能描述。生产者和消费者的 .c 文件首先包含一个 init 作为初始化函数，并在其中设置生产者或者消费者的长度。生产者还包含一个信号产生函数，如果当前位置小于生产长度，则将当前位置写入输出端，否则销毁进程。 消费者包含一个信号消费函数，要是当前位置小于消费长度，则读出并打印输入端信号，否则销毁进程。最后还有一个平方进程，属于信号处理函数，读入输入端信号，处理以后输出到输出端。
