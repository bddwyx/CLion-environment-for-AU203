# CLion environment for AU203

# 控制导论CLion环境配置教程

## 折腾这一大堆的好处

* 跨平台
* JetBrain近年来的表现越来越好
* ~~信仰~~

## 下载与安装
​	下文中存在基于MinGW与MSVC（32位编译）两种方法的配置方式，根据需求选择一种配置即可。

### 打包下载
​	这个Repository整理了所有不需要注册的、小于100M的东西，有Github使用经验的可以自行Clone。如果没有使用经验，按照下方步骤操作。

​	首先点击Star
![Star](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Star.png)

​	然后下载zip
![Download](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Download.png)

### MinGW（目前还没成功，现阶段还是基于MSVC）

​	MinGW(Minimalist [GNU](https://baike.baidu.com/item/GNU) for Windows)，一个GNU工具集导入库的集合，包括gcc、g++、gdb等。

​	年代久远，之前使用的安装包和资源包中的版本不同。双击安装，记住安装路径，后面会考。

​	下一步是添加环境变量，搜索栏搜索或者此电脑–右键属性–高级系统设置–环境变量–系统变量中PATH–编辑，添加刚刚的安装路径\bin
![Environment](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Environment.png)
![Variable](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Variable.png)

### CLion
​	涉及到JetBrain教育账号注册，所以这里不提供安装包。学生创新中心软件授权中心	[JetBrains all in one](http://lic.si.sjtu.edu.cn/Default/softshow/tag/MDAwMDAwMDAwMLGedqE)

​	打开File-Settings(Ctrl+Alt+S)，在Build,Execution,Deployment-Toolchains如图配置(忽略STM32)

![Settings](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Settings.png)

#### MinGW

![Toolchain](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Toolchain.png)

#### MSVC

![Toolchain2](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Toolchain2.png)

### OpenCV源码
​	在交大校园网下点击下载	[OpenCV Release](https://opencv.org/releases/)

![OpenCV](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/OpenCV.png)

​	双击运行后，build文件夹下的内容就可以给VS用了。但是CLion+MinGW下需要对源码重新编译，build下的内容也不支持vc16。

### CMake-gui

​	一个图形化的CMake配置工具。资源包已提供，双击安装。

### 重启
​	字面意思。


## OpenCV编译

### CMake
​	选中两个路径，第一个是source文件夹路径，第二个是需要新建的目标文件夹(可以随便起名字，不要像我这么随意，可以叫x86mingw，x86vc16)。红色部分理论上应该是不存在的。
![CMake](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/CMake.png)

	#### MinGW

​	点击Configure，选项如图，等好长时间，这个阶段缺什么会自动补什么。

![Configure](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Configure.png)

![Configure2](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Configure2.png)

	#### MSVC

​	注意，如果vc16编译，第一栏应当选中vc16，第二栏选win32。

![Configure1.2](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Configure1.2.png)

​	过程完成后就可以选编译选项了，如果有心情可以选一些Boost、Eigen、CUDA，没心情就算了。为了简化步骤，省略了OpenCV-Contrib的编译。之后Generate即可。

### 清理工作
​	关闭Steam等无关应用。其他的也能关就关。插好电源，准备好散热。

​	如果可能，最好提前三天斋戒以免在下面最容易出问题的步骤遇到玄学问题。以下步骤如果不成功就多试几次，不知道为啥有的时候就会正常。

### 正式编译

​	打开Windows PowerShell，输入
```Linux
cd E:\OpenCV\4.5.1\newBuild
```
​	其中后面的路径需要根据实际情况改成自己的。回车执行。
![Shell](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Shell.png)

​	根据编译器选择下面的步骤。

#### MinGW
​	然后

```Linux
mingw32-make -j4
```
​	这个-j后面的数字可以根据自己电脑的情况来定。我的电脑是R7-4800，通常-j16，几分钟就完成了，结果上次一激动-j24，爆了内存，后5%占用了一半时间才完成。

​	场面会极其惨烈，几百个几百个报warning。可能会报错，如果报错和Python有关，最简单的方法就是把电脑上的Python都卸载干净。同理还可能有JAVA的报错。

​	这个过程时间会比较长，可以看看[猫片1](https://www.bilibili.com/video/BV18J411h7Bj?from=search&seid=6369731823639503698) [猫片2](https://www.bilibili.com/video/BV1dZ4y1x72L?from=search&seid=6369731823639503698) [猫片3](https://www.bilibili.com/video/BV1v54y1W7sd?from=search&seid=6369731823639503698)

​	完成之后继续

```Linux
mingw32-make install
```

​	后面有一步环境变量，我也没太配对，索性不管了。

#### MSVC

```Linux
cmake --build . --config Release
```
[猫片1](https://www.bilibili.com/video/BV18J411h7Bj?from=search&seid=6369731823639503698) [猫片2](https://www.bilibili.com/video/BV1dZ4y1x72L?from=search&seid=6369731823639503698) [猫片3](https://www.bilibili.com/video/BV1v54y1W7sd?from=search&seid=6369731823639503698)

## 测试
​	新建工程，CMakeList

#### MinGW
```CMake
cmake_minimum_required(VERSION 3.17)
project(451Test)

set(CMAKE_CXX_STANDARD 14)
set(OpenCV_DIR E:/OpenCV/4.5.1/newBuild) #这个路径是要改的

add_executable(451Test main.cpp)

find_package(OpenCV REQUIRED)

target_link_libraries(451Test ${OpenCV_LIBS})
```

#### MSVC
```CMAKE
cmake_minimum_required(VERSION 3.17)
project(451Test)

set(CMAKE_CXX_STANDARD 14)
set(OpenCV_DIR E:/OpenCV/4.5.1/vc16x86/lib)
set(CMAKE_PREFIX_PATH   E:/OpenCV/4.5.1/vc16x86)
find_package(OpenCV REQUIRED)

add_executable(451Test main.cpp)

target_link_libraries(451Test ${OpenCV_LIBS})
```

​	main.cpp

```cpp
#include <iostream>
#include <opencv2/highgui/highgui.hpp>

using namespace std;
using namespace cv;

int main() {
    Mat img = imread(R"(C:\Users\bddwy\Desktop\Hero.bmp)"); //路径也是要改的，随便找一张图片
    if (img.empty()) {
        cerr << "Error" << endl;
        return -1;
    }
    namedWindow("figure", WINDOW_FULLSCREEN);
    imshow("figure", img);
    waitKey();
    return 0;
}
```
​	Settings中配置CMake	

![CLionCMake](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/CLionCMake.png)

​	观察运行结果。如果返回奇怪的数值，修改执行策略。
![Edit](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Edit.png)

#### MinGW

![Edit2](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Edit2.png)

#### CLion

![Edit3](https://github.com/bddwyx/CLion-environment-for-AU203/blob/main/figure/Edit3.png)

## Reference
​	https://blog.csdn.net/lwplwf/article/details/77369930

​	https://blog.csdn.net/xiangxianghehe/article/details/70880762

​	https://blog.csdn.net/weixin_40448140/article/details/104720134

​	https://blog.csdn.net/weixin_41115751/article/details/101310690

## 编译生成dll文件（MSVC）
```CMake
cmake_minimum_required(VERSION 3.17)
project(driver_onhand)

set(CMAKE_CXX_STANDARD 14)

add_library(driver_onhand SHARED driver_onhand.cpp driver_onhand.h driver_onhand.def osspec.h tgf.h)
```









作者 ： 席望

邮箱 ： bddwyx@sjtu.edu.cn