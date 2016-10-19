# Description

> The **distributed operation layer (DOL)** is a software development framework to program parallel applications. 

</br>

# How to install

###开发环境配置
----
*  安装准备   

    安装VMware虚拟</br>
    下面是一些必要的环境安装：

    ```$ sudo apt-get update```</br>
```$	sudo apt-get install ant```</br>
```$ 	sudo apt-get install openjdk-7-jdk```</br>
```$	sudo apt-get install unzip``` 

    下载所需文件 [systemc-2.3.1.tgz][1] 和 [dol_ethz.zip][2] 或者拷贝到虚拟机。

------

*  解压文件
     1. 新建 dol 文件夹
     
        ```$ mkdir dol```  
     * 将 dolethz.zip 解压到 dol 文件夹中

        ```$ unzip dol_ethz.zip -d dol```
     * 解压 systemc
     
        ```$ tar -zxvf systemc-2.3.1.tgz```

----- 
*  编译 systemc
     1. 解压后进入 systemc-2.3.1 的目录下
     
        ```$ cd systemc-2.3.1```  
     * 新建一个临时文件夹 objdir
     
        ```$ mkdir objdir```
     * 进入该文件夹 objdir
     
        ```$ cd objdir```
     * 解压后进入 systemc-2.3.1 的目录下
     
        ```$ cd systemc-2.3.1```  
     * 运行 configure (根据系统的环境设置参数，用于编译)
     
        ```$ ../configure CXX=g++ --disable-async-updates```
	  <br> 这一步结果截图：
      <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/cmFzIDZnsi0l2Z3V*Hqr.6Tyb7FzdwKIVbO6Uynp3ME!/b/dAkBAAAAAAAA&bo=LgKjAQAAAAADAKs!&rf=viewer_4&t=5/2.jpg">
      </div></br>
     * 编译
     
        ```$ sudo make install```
     * 进入编译完后的当前目录
     
        ```$ cd ..```        
        ```$ ls```
     * 记录当前的工作路径
     
        ```$ pwd```  
	    此时我的路径为：
<div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/Zll0CIXIeCzo3zmc4y7X5dVEvUB1pVM5kl.FIaCGTrQ!/b/dMYAAAAAAAAA&bo=IgI.AAAAAAADADs!&rf=viewer_4&t=5">
      </div></br>

-----
* 编译dol
     1. 进入刚刚 dol 的文件夹

        ```$ cd ../dol```  
     * 修改 build_zip.xml 文件。</br>
       找到下面这段话，(上面编译的 systemc 位置)
     
        ```<property name="systemc.inc" value="YYY/include"/>```<br>
        ```<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>```

        把 YYY 改成上页 pwd 的结果
     * 编译
     
        ```$ ant -f build_zip.xml all```

          成功会显示build successful!
      <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/h6vbYwp*QHkdzSrSP7ADMHJGPUA.Q4s13XblpPi9Ixw!/b/dNwAAAAAAAAA&bo=LgKjAQAAAAADAKs!&rf=viewer_4&t=5/4.jpg">
      </div></br>
----
* 运行第一个例子
     1. 进入build/bin/mian路径下
     
        ```$ cd build/bin/main```
     * 运行第一个例子
     
        ```$ sudo ant -f runexample.xml -Dnumber=1```
      <div align="center"><img src="http://a3.qpic.cn/psb?/V13tPyF42OAeS3/bIj.7sWARnKMaS00DgC*IPZnIN5C2K9AH6iNS1TcEFE!/b/dAoBAAAAAAAA&bo=LgIBAgAAAAADAAo!&rf=viewer_4&t=5/5.jpg">
      </div></br>
----
 
</br>
# Experimental experience
*   之前已经写好了README.md，这次在加入 lab3 实验报告时不小心用了 rm 指令，坑掉了之前的实验。小白还是慎用 rm [哭泣脸]。<br><br>
*   在编译 dol，执行 ```$ ant -f build_zip.xml all``` 时，copy 第一个文件就失败。提示显示是权限的问题，permission denied。错误截图如下：
    <div align="center"><img src="http://a2.qpic.cn/psb?/V13tPyF42OAeS3/2Yhh3jByTK*UdUEzknSRaNtbjczTD3PdDGSPKPHpe84!/b/dOUAAAAAAAAA&bo=5AKdAAAAAAADAF4!&rf=viewer_4&t=5">
      </div>
解决方法是修改 dol 和 systmc 文件夹的权限，具体操作如下：
    <div align="center"><img src="http://a1.qpic.cn/psb?/V13tPyF42OAeS3/WfUwdjxSVNcFZWtpoITLOaVPrCh4NWE4ifgaxYjP.00!/b/dLEAAAAAAAAA&bo=3AJKAAAAAAADALE!&rf=viewer_4&t=5">
    </div>
修改好后就可以正常编译了。<br><br>
*   关于 ant 的安装:
首先可以直接用 ```$ sudo apt-get install ant``` 直接安装，但是这种方法不好，推荐手动安装。
	1. 到 Apache 官网下载最新版本的 [ant][5]。

    2. 解压下载下来的 .tar.gz 文件：<br> ```$ tar -xf apache-ant-1.9.7-bin.tar.gz``` 
    
    3. 在 /usr/ 文件夹里面新建文件夹  /usr/ant :
      <br> ```$ cd /usr/```<br>
           ```$ mkdir ant```
    4. 将解压出来的文件移动到  /usr/ant 下：<br>
    ```$ sudo mv apache-ant-1.9.7 /usr/ant ``` 

    4. 配置环境变量,  ```$ sudo gedit /etc/profile``` ，添加以下：
    
        ```$ export ANT_HOME=/usr/ant/apache-ant-1.9.7```<br>
     ```$ export PATH=$JAVA_HOME/bin:$PATH:$ANT_HOME/bin```

    5.验证是否安装成功： ```$ ant -version```<br><br>

   
*   关于图片怎么加入。查了一下，有很多方法。
    1. 比如说可以先找一个图片分享网站，比如CloudApp，[七牛空间][3]，把图片放进去，生成一个网址；最后把网址复制到markdown的代码中。
    2. 将Markdown需要用的图片放到git仓库中，发布到[github][4]上，访问github仓库图片拷贝链接地址，再在Markdown中引用。
    3. 我最后用了，最接地气的，放到qq相册里面。    
    </br>
*   html可以用于Markdown
    1. 图片的放入就可以用 div 和 img 标签。

  [1]: http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
  [2]: http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
  [3]:http://www.qiniu.com/
  [4]:https://github.com/
  [5]:http://ant.apache.org/bindownload.cgi