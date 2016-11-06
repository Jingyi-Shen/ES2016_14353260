# Deadlock 
<br>

### 死锁
死锁就是两个或者多个进程，互相请求对方占有的资源而陷入相互等待的状态。

<br>
### 死锁产生的四个必要条件
互斥：一个资源每次只能被一个进程使用<br>
非抢占：进程已获得的资源，在末使用完之前，不能被别的进程强行剥夺<br>
占有并等待：一个进程因请求资源而被其他进程阻塞时，此阻塞进程已经获得的资源保持不放<br>
循环等待：若干进程之间形成一种头尾相接的循环等待资源关系<br>

<br>

### 实验代码
* Class Deadlock:
<div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/tIFQdgCPYX0TCQtuAqKt*9zmWePogTubJhYA6iDzQF0!/b/dHwBAAAAAAAA&bo=ggF8AQAAAAADANs!&rf=viewer_4&t=5"></div>
* Class A:
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/Hctt9SVdQYo5d8uBCBelOFXIRIYbBLEnK4Kj4LczfUY!/b/dOUAAAAAAAAA&bo=hAGRAAAAAAADADE!&rf=viewer_4&t=5"></div>
* Class B:
<div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/29kfyGX0LFSODkQiZWWuR6hUZw63fkMH2ZgM.hCtTHQ!/b/dOUAAAAAAAAA&bo=gAGaAAAAAAADAD4!&rf=viewer_4&t=5"></div>

<br>
### 实验结果(发生死锁)

* windows：
    <div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/aBk5JpPqxsSD7Gdw5LHGS4.yT1nK49vVm0ERil0Becg!/b/dLEAAAAAAAAA&bo=igKzAQAAAAADAB8!&rf=viewer_4&t=5"></div><br>
### 实验以及结果分析
* 在这个 JAVA 程序中，创建了一个 Deadlock 的类来模拟实现死锁。另外两个类 A、B 分别有两个 synchronized 的函数。method 函数的内容是调用另一个类的 synchronized 函数。last 函数输出内容。<br>

* 死锁如何发生：<br>
  Deadlock 的构造函数创建了一个线程 t，在等待一个延时以后执行类 A 的对象 a 的 method( ) 函数，这个函数会调用 b 的 last( ) 函数。与此同时，在 Runnable 函数运行时，run 函数被调用，函数内部是执行 b 的 method( ) 函数，这个函数里面调用 a 的 last( ) 函数。<br>因为在一个 synchronized 类中只能有一个线程在执行操作(满足互斥条件)，A 执行 a 的 method( ) 函数，需要 b 的 last( ) 资源，而 B 执行 b 的 method( ) 函数，需要 a 的 last( ) 资源，满足占有并等待和循环等待的条件，加上进程优先级相等，满足非抢占条件。死锁的四个条件都满足，发生死锁。

* 批处理：<br>
  由于两个进程创建时间的差别，所以需要多次执行这个程序，需要一个批处理<br>
   linux: 
     * 写一个后缀为 .sh 的 bash，如下：
     <div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/LCoIpr29l5Dc9hDF*ok5tot8.vvYhGsOzczHE8j4D7s!/b/dHcBAAAAAAAA&bo=PAGkAAAAAAADALw!&rf=viewer_4&t=5"></div>

	* 运行：
    <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/wApard*qW1YKReQF*LC5lEOZwVlHnw3iXKtHzy8hbfI!/b/dAkBAAAAAAAA&bo=zAEWAAAAAAADAP4!&rf=viewer_4&t=5"></div>

    windows：<br>
   * 写一个后缀为 .bat 的 批处理，如下：
    <div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/YN5yJIIFltr47Zfw1irKHlp85ST9ZgTAjQXRtMS7pFQ!/b/dK0AAAAAAAAA&bo=DgG4AAAAAAADAJI!&rf=viewer_4&t=5"></div>

   * 运行：
    <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/EgpJirx3*VJoDLA112lu7sLaeLDgwT6SQ9dejLRAIYo!/b/dLIAAAAAAAAA&bo=5gAjAAAAAAADAOA!&rf=viewer_4&t=5"></div>
<br>