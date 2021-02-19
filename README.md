# CLion environment for AU203

# 控制导论CLion环境配置教程

## 下载与安装

### 打包下载
​	这个Repository整理了所有不需要注册的、小于100M的东西，有Github使用经验的可以自行Clone。如果没有使用经验，按照下方步骤操作。
​	首先点击Star
![Star](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Star.png)
​	然后下载zip
![Download](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Download.png)

### MinGW

​	MinGW(Minimalist [GNU](https://baike.baidu.com/item/GNU)for Windows)，一个GNU工具集导入库的集合，包括gcc、g++、gdb等。
​	年代久远，之前使用的安装包和资源包中的版本不同。双击安装，记住安装路径，后面会考。
​	下一步是添加环境变量，搜索栏搜索或者此电脑–右键属性–高级系统设置–环境变量–系统变量中PATH–编辑，添加刚刚的安装路径\bin
![Environment](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Environment.png)
![Variable](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Variable.png)

### CLion
​	涉及到JetBrain教育账号注册，所以这里不提供安装包。学生创新中心软件授权中心	[JetBrains all in one](http://lic.si.sjtu.edu.cn/Default/softshow/tag/MDAwMDAwMDAwMLGedqE)

![Settings](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Settings.png)

​	打开File-Settings(Ctrl+Alt+S)，在Build,Execution,Deployment-Toolchains如图配置(忽略STM32)

![Toolchain](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Toolchain.png)

### OpenCV源码
​	在交大校园网下点击下载	[OpenCV Release](https://opencv.org/releases/)

![OpenCV](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/OpenCV.png)

​	build文件夹下的内容就可以给VS用了。但是CLion+MinGW下需要对源码重新编译。

### CMake-gui

​	一个图形化的CMake配置工具。资源包已提供，双击安装。

### 重启
​	字面意思。


## OpenCV编译

### CMake
​	选中两个路径，第一个是source文件夹路径，第二个是需要新建的目标文件夹(可以随便起名字，不要像我这么随意，可以叫x86mingw)。红色部分理论上应该是不存在的。
![CMake](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/CMake.png)

​	点击Configure，选项如图，等好长时间，这个阶段缺什么会自动补什么。

![Configure](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Configure.png)

![Configure2](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Configure2.png)

​	过程完成后就可以选编译选项了，如果有心情可以选一些Boost、Eigen、CUDA，没心情就算了。为了简化步骤，省略了OpenCV-Contrib的编译。之后Generate即可。

### 正式编译

不同于CMD，这里打开Windows PowerShell，输入
```Linux
cd E:\OpenCV\4.5.1\newBuild
```
其中后面的路径需要根据实际情况改成自己的。回车执行。
![Shell](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Shell.png)

## Reference
​	https://blog.csdn.net/lwplwf/article/details/77369930
​	https://blog.csdn.net/xiangxianghehe/article/details/70880762
​	https://blog.csdn.net/weixin_40448140/article/details/104720134


作者 ： 席望
邮箱 ： bddwyx@sjtu.edu.cn