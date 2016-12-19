# Keil调试器的使用

<br><br>
## 打开工程

#### 1. 解压 FunctionalDebugging.zip<br>

#### 2. 打开文件
   点击 Project->Open Project，选择解压好的路径下FunctionalDebugging 文件夹中的 .uvproj 文件<br>

#### 3. 两个.s文件，Startup.s和main.s<br>
   Startup.s：完成基本的CPU初始化，如果有必要，这里也对外围的设备进行初始化<br>main.s：我们的主体程序， 执行完Startup.s后，跳转到Start
<br><br>

## 开始调试器:

#### 1.启动调试器
   点击Debug->Start/Stop Debug Session

#### 2.基本调试操作
 单步跟踪运行，全速运行，观察／修改存储器的数据，复位 ，设置断点 ，带断点的全速运行 ，退出仿真 
<br><br>

## 实验练习程序简介：
  main.s 程序有两个缓冲区 HappyBuf 和 SadBuf，程序将 sad 和 happy 两个8位变量赋为随机数，再将这两个变量转存到数组中。Cnt 保存数组偏移量，Cnt 被初始化为 0，转存时先判断 Cnt 是否越界，若否，则将变量转存再将 Cnt 加 1。
<br>
#### 最终值
中间截图：<br>
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/MJBOsy9uRw23sy0qU4ctsovW6LQy2MksnyrktsAUHnA!/b/dMYAAAAAAAAA&bo=rgI9AAAAAAADALQ!&rf=viewer_4&t=5"></div>
红色框的是happy，绿色框的是sad，蓝色框的是Cnt。<br><br>
程序解释： 从原程序中可以看出，为 HappyBuf 和 SadBuf 分别分配了连续 20 字节的存储单元并初始化为 0，而为 Cnt 和 M 分别分配了 4 字节的存储空间。
<br>整个程序所做的工作就是分别取随机数，然后把随机数低八位存到 happy 和 sad，然后通过基地址 + 偏移量 (Cnt) 将 happy 和 sad 分别存到 HappyBuf 和 SadBuf缓存中，直到 Cnt=SIZE，空间存满，程序会跳过 Save 中的用于保存的代码 (跳到done)。<br><br>
最终截图：<br>
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/FRnt2Q7ZNXmkZR8iw*hf6R2..*Oq0sdx9Bd1txoQvVw!/b/dAYBAAAAAAAA&bo=pQJaAAAAAAADANg!&rf=viewer_4&t=5"></div>
绿色框的是 HappyBuf 的最终值，红色框的是 SadBuf 的最终值，蓝色框的是 Cnt 的最终值 (Cnt) 最终为 0x00000014。<br>
