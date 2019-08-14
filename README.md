# YOLOv3-for-Windows


**<font size=5>在python3.6下安装vs2017+Cuda9.0+Cudnn7.1+TensorFlow-gpu1.9.0记录</font>**



[TOC]



# VS2017安装

安装Cuda9.0之前需要去微软官方下载VS2017，[链接](https://docs.microsoft.com/zh-cn/visualstudio/releasenotes/vs2017-relnotes)（**建议还是安装在C盘**）

安装过程：

![](E:\研究生\Python学习\图片\vs2017安装过程1.png)

选择单个组件，然后选择vc++2015,也就是vc14，如下图所选择！！！安装即可

![](E:\研究生\Python学习\图片\vs2017安装过程2.png)



**注意** 安装visual studio的时候，如果有过第一次安装的过程，那么想重新安装的时候必须先将visual studio和visual studio install这两个卸载，然后**一定要将注册表下的SharedInstallationPath项删除**，否则第二次安装会无法更改**共享组件、工具和SDK**的位置。

如下图所示：

![](E:\研究生\Python学习\图片\第二次安装的时候共享组件、工具和SDK的路径显示第一次的位置.png)

**删除注册表**：

点击开始菜单->打开运行->输入regedit

![](E:\研究生\Python学习\图片\删除注册表-regedit.png)

根据路径**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup**打开目标**SharedInstallationPath**

![](E:\研究生\Python学习\图片\打开注册表找到目标SharedInstallationPath.png)

删除就ok了，第二次安装的时候**共享组件、工具和SDK**的路径就不会显示第一次的位置



# Cuda9.0安装

## 关于TensorFlow Cuda Cudnn的版本关系对照表

**Linux下**

![](E:\研究生\Python学习\图片\Linux下的对照表.png)

**Windows下**

![](E:\研究生\Python学习\图片\windows下的对照表.png)



## Cuda的下载安装配置

首先需要确认计算机有独立显卡（而且是英伟达的显卡），然后点击[此处](https://developer.nvidia.com/cuda-gpus)找一下你的显卡是否在列表中

![](E:\研究生\Python学习\图片\查询显卡是否够格.png)

访问[链接](https://developer.nvidia.com/cuda-toolkit-archive)在列表中选中Cuda9.0

![](E:\研究生\Python学习\图片\Cuda列表.png)

之后选择相关参数进行下载

![](E:\研究生\Python学习\图片\下载Cuda9.0.png)

下载Cuda9.0过程建议将Cuda9.0安装在C盘（亲测安装到C盘以外就爆炸）

安装成功后进行环境变量的添加：

![](E:\研究生\Python学习\图片\cuda环境变量设置-new-2.png)

测试Cuda是否安装成功：

![](E:\研究生\Python学习\图片\测试Cuda安装是否成功.png)



# cuDNN7.1下载

访问[链接](https://developer.nvidia.com/cudnn)（需要注册账号）

![](E:\研究生\Python学习\图片\安装Cudnn.png)

注意选择Cudnn，注意7.1.x后面跟着的是Cuda几版本

下载完毕后是一个压缩包，解压完后就可以将里面bin、include、lib文件夹中的内容分别拷入Cuda的安装目录下

Cudnn解压后的文件夹内容：

![](E:\研究生\Python学习\图片\Cudnn文件夹内容.png)

将bin里面的cudnn64_7.dll、include里面的cudnn.h、lib里面的cudnn.lib分别放入Cuda目录下的bin、include、lib文件夹里

![](E:\研究生\Python学习\图片\放置Cuda9.0里的位置.png)



# TensorFlow-gpu安装：

根据版本进行TensorFlow-gpu的安装，点击[此处](http://mirrors.aliyun.com/pypi/simple/tensorflow-gpu/)查看所需要的TensorFlow-gpu版本是多少

安装命令（我需要的TensorFlow-gpu版本是1.9.0）：

```
​```
 pip install tensorflow-gpu==1.9.0
​```
```



最后测试Cuda9.0_+Cudnn7.1+TensorFlow-gpu1.9.0+python3.6是否安装成功

测试代码：

~~~python
```python
import tensorflow as tf

hello= tf.constant('Hello, TensorFlow!')
sess= tf.Session()
print(sess.run(hello)) 
```
~~~

结果：

![](E:\研究生\Python学习\图片\测试cuda+cudnn+tensorflow-gpu+python是否安装成功.png)

最后会输出信息，在这个之前会显示你的显卡信息

------



# openCV安装

官网下载[链接](https://opencv.org/releases/#)

**请不要使用3.4.1，请不要使用3.4.1，请不要使用3.4.1**。yolo的作者已经在github上说明了使用3.4.1会出现编译问题。（亲测，3.4.1是真的有问题，假如有小伙伴使用3.4.1没问题，那就是我太菜的问题(●'◡'●)）

![](E:\研究生\Python学习\图片\opencv3.4.0下载.png)

双击下载好的文件，选择解压路径后点击Extract即可完成解压，解压后就会自动生成一个opencv的文件夹

![](E:\研究生\Python学习\图片\点击下载好的opencv文件.png)

配置环境变量

将你解压后的opencv文件夹中的***\opencv\build\x64\vc14\bin路径添加到环境变量中

![](E:\研究生\Python学习\图片\设置opencv环境变量.png)

ok~ 



# darknet下载

下载[链接](https://github.com/AlexeyAB/darknet)

也可以直接使用git-bash 下载

```
git clone https://github.com/AlexeyAB/darknet
```



## darknet.vcxproj文件的修改

下载完成之后，用文本编辑器、或记事本（我用的是sublime）打开...\darknet-master\build\darknet下面的darknet.vcxproj。分别在55行和299行（也可以全文搜索CUDA ）的CUDA 10.0————>CUDA 9.0

![](E:\研究生\Python学习\图片\修改文件darknet.vcxproj中的conda.png)



## darknet.sln文件的设置

接下来需要打开darknet.sln，**注意**不要直接双击打开，可以先打开vs2017，然后点击**文件—>打开—>项目**选中darknet.sln打开

打开后，vs会显示

![](E:\研究生\Python学习\图片\打开darknet后选择无升级.png)

注意，一定要选择**无升级**，因为，如果点击升级，那就是把vs2015的项目升级成vs2017,这样做的结果就是**白给**。然后将项目改成Release x64，然后右键项目—>属性

![](E:\研究生\Python学习\图片\vs编辑项目属性.png)

然后，VC++目录—>包含目录—>编辑添加目录：...\opencv\build\inclde（...表示各位小伙伴你们各自的安装路径，以下同理）
![](E:\研究生\Python学习\图片\vc++设置.png)

然后，配置库目录，添加：...\opencv\build\x64\vc14\lib

![](E:\研究生\Python学习\图片\vc++库目录设置.png)

然后，C/C++—>常规—>附加包含目录—>编辑添加目录：...\opencv\build\include

![](E:\研究生\Python学习\图片\c++附加目录设置.png)

然后，链接器—>输入—>附加依赖项—>添加目录：...\opencv\build\x64\vc14\lib下库的名字：opencv_world340.lib

![](E:\研究生\Python学习\图片\链接器附加依赖项设置.png)

接着，**需要拷贝安装好的CUDA 9.0.props等文件**：

CUDA 9.0.props等文件就在cuda的安装目录下，本人的路径是：C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\extras\visual_studio_integration\MSBuildExtensions

![](E:\研究生\Python学习\图片\需要拷贝的cuda9.0的文件.png)

将里面的所有的文件考本到C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\VC\VCTargets\BuildCustomizations中，这是vs2017安装后的路径

![](E:\研究生\Python学习\图片\将cuda文件拷贝到vs下的buildCustomizations下.png)

不然可能会报如下错误：

![](E:\研究生\Python学习\图片\因为没有拷贝cuda文件报错.png)

然后，将...\opencv\build\x64\vc14\bin下的opencv_world340.dll 和opencv_ffmpeg340_64.dll 

![](E:\研究生\Python学习\图片\将opencv的文件拷贝到项目下的x64中.png)

复制到E:\darknet\darknet-master\build\darknet\x64 目录下。

最后，还需要修改darknet.vcxproj下158行的compute值,将75改成61，原因貌似是和使用者显卡的计算能力值有关（**这一步小伙伴们可以根据自身情况可以灵活变动**）

![](E:\研究生\Python学习\图片\修改compute值.png)

因为我当时配置的时候也参考了别人的帖子，别人75是可以正常进行工程生产，而我需要降低数值才可以，可能我的显卡太菜了/(ㄒoㄒ)/

完成上述之后，就可以在darknet工程上右键—>生成，就会发现在工程目录下x64下多了些darknet.exe等文件啦，到这里就完成了搭建了

![](E:\研究生\Python学习\图片\成功的生成.png)

![](E:\研究生\Python学习\图片\生成的darknet.exe.png)

完成搭建，之后就是激动人心的测试环节



# 下载yolo3.weights

- 下载作者训练好的模型：[官网地址](https://pjreddie.com/darknet/yolo/)、[GitHub](https://github.com/AlexeyAB/darknet/blob/master/README.md)下载yolo3.weights

![](E:\研究生\Python学习\图片\github下的yolo下载处.png)

为了方便大家，可以直接从我的[网盘，提取码zfib](https://pan.baidu.com/s/1FMXsQW19aSADuDyNF33IhA)下载

下载后放在...\darknet-master\build\darknet\x64目录下

然后进行测试，在当前目录下右键—>在此处打开命令窗口（也可以打开cmd，cd到darknet.exe的目录下），然后输入命令：`darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg`

下面是结果（我用的是自己喜欢的图）：

![](E:\研究生\Python学习\图片\属于命令行成功.png)



