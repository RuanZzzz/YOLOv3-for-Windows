# YOLOv3-for-Windows

**<font size=5>在python3.6下安装vs2017+Cuda9.0+Cudnn7.1+TensorFlow-gpu1.9.0记录</font>**



[TOC]



# VS2017安装

安装Cuda9.0之前需要去微软官方下载VS2017，[链接](https://docs.microsoft.com/zh-cn/visualstudio/releasenotes/vs2017-relnotes)（**建议还是安装在C盘**）

安装过程：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/vs2017%E5%AE%89%E8%A3%85%E8%BF%87%E7%A8%8B1.png)

选择单个组件，然后选择vc++2015,也就是vc14，如下图所选择！！！安装即可

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/vs2017%E5%AE%89%E8%A3%85%E8%BF%87%E7%A8%8B2.png)



**注意** 安装visual studio的时候，如果有过第一次安装的过程，那么想重新安装的时候必须先将visual studio和visual studio install这两个卸载，然后**一定要将注册表下的SharedInstallationPath项删除**，否则第二次安装会无法更改**共享组件、工具和SDK**的位置。

如下图所示：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E7%AC%AC%E4%BA%8C%E6%AC%A1%E5%AE%89%E8%A3%85%E7%9A%84%E6%97%B6%E5%80%99%E5%85%B1%E4%BA%AB%E7%BB%84%E4%BB%B6%E3%80%81%E5%B7%A5%E5%85%B7%E5%92%8CSDK%E7%9A%84%E8%B7%AF%E5%BE%84%E6%98%BE%E7%A4%BA%E7%AC%AC%E4%B8%80%E6%AC%A1%E7%9A%84%E4%BD%8D%E7%BD%AE.png)

**删除注册表**：

点击开始菜单->打开运行->输入regedit

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%88%A0%E9%99%A4%E6%B3%A8%E5%86%8C%E8%A1%A8-regedit.png)

根据路径**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup**打开目标**SharedInstallationPath**

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/打开注册表找到目标SharedInstallationPath.png)

删除就ok了，第二次安装的时候**共享组件、工具和SDK**的路径就不会显示第一次的位置



# Cuda9.0安装

## 关于TensorFlow Cuda Cudnn的版本关系对照表

**Linux下**

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/Linux%E4%B8%8B%E7%9A%84%E5%AF%B9%E7%85%A7%E8%A1%A8.png)

**Windows下**

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/windows%E4%B8%8B%E7%9A%84%E5%AF%B9%E7%85%A7%E8%A1%A8.png)



## Cuda的下载安装配置

首先需要确认计算机有独立显卡（而且是英伟达的显卡），然后点击[此处](https://developer.nvidia.com/cuda-gpus)找一下你的显卡是否在列表中

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E6%9F%A5%E8%AF%A2%E6%98%BE%E5%8D%A1%E6%98%AF%E5%90%A6%E5%A4%9F%E6%A0%BC.png)

访问[链接](https://developer.nvidia.com/cuda-toolkit-archive)在列表中选中Cuda9.0

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/Cuda%E5%88%97%E8%A1%A8.png)

之后选择相关参数进行下载

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/下载Cuda9.0.png)

下载Cuda9.0过程建议将Cuda9.0安装在C盘（亲测安装到C盘以外就爆炸）

安装成功后进行环境变量的添加：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/cuda%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E8%AE%BE%E7%BD%AE-new-2.png)

测试Cuda是否安装成功：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E6%B5%8B%E8%AF%95Cuda%E5%AE%89%E8%A3%85%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F.png)



# cuDNN7.1下载

访问[链接](https://developer.nvidia.com/cudnn)（需要注册账号）

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%AE%89%E8%A3%85Cudnn.png)

注意选择Cudnn，注意7.1.x后面跟着的是Cuda几版本

下载完毕后是一个压缩包，解压完后就可以将里面bin、include、lib文件夹中的内容分别拷入Cuda的安装目录下

Cudnn解压后的文件夹内容：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/Cudnn%E6%96%87%E4%BB%B6%E5%A4%B9%E5%86%85%E5%AE%B9.png)

将bin里面的cudnn64_7.dll、include里面的cudnn.h、lib里面的cudnn.lib分别放入Cuda目录下的bin、include、lib文件夹里

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E6%94%BE%E7%BD%AECuda9.0%E9%87%8C%E7%9A%84%E4%BD%8D%E7%BD%AE.png)



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

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E6%B5%8B%E8%AF%95cuda%2Bcudnn%2Btensorflow-gpu%2Bpython%E6%98%AF%E5%90%A6%E5%AE%89%E8%A3%85%E6%88%90%E5%8A%9F.png)

最后会输出信息，在这个之前会显示你的显卡信息

------



# openCV安装

官网下载[链接](https://opencv.org/releases/#)

**请不要使用3.4.1，请不要使用3.4.1，请不要使用3.4.1**。yolo的作者已经在github上说明了使用3.4.1会出现编译问题。（亲测，3.4.1是真的有问题，假如有小伙伴使用3.4.1没问题，那就是我太菜的问题(●'◡'●)）

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/opencv3.4.0%E4%B8%8B%E8%BD%BD.png)

双击下载好的文件，选择解压路径后点击Extract即可完成解压，解压后就会自动生成一个opencv的文件夹

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E7%82%B9%E5%87%BB%E4%B8%8B%E8%BD%BD%E5%A5%BD%E7%9A%84opencv%E6%96%87%E4%BB%B6.png)

配置环境变量

将你解压后的opencv文件夹中的***\opencv\build\x64\vc14\bin路径添加到环境变量中

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E8%AE%BE%E7%BD%AEopencv%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

ok~ 



# darknet下载

下载[链接](https://github.com/AlexeyAB/darknet)

也可以直接使用git-bash 下载

```
git clone https://github.com/AlexeyAB/darknet
```



## darknet.vcxproj文件的修改

下载完成之后，用文本编辑器、或记事本（我用的是sublime）打开...\darknet-master\build\darknet下面的darknet.vcxproj。分别在55行和299行（也可以全文搜索CUDA ）的CUDA 10.0————>CUDA 9.0

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E4%BF%AE%E6%94%B9%E6%96%87%E4%BB%B6darknet.vcxproj%E4%B8%AD%E7%9A%84conda.png)



## darknet.sln文件的设置

接下来需要打开darknet.sln，**注意**不要直接双击打开，可以先打开vs2017，然后点击**文件—>打开—>项目**选中darknet.sln打开

打开后，vs会显示

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/打开darknet后选择无升级.png)

注意，一定要选择**无升级**，因为，如果点击升级，那就是把vs2015的项目升级成vs2017,这样做的结果就是**白给**。然后将项目改成Release x64，然后右键项目—>属性

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/vs%E7%BC%96%E8%BE%91%E9%A1%B9%E7%9B%AE%E5%B1%9E%E6%80%A7.png)

然后，VC++目录—>包含目录—>编辑添加目录：...\opencv\build\inclde（...表示各位小伙伴你们各自的安装路径，以下同理）
![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/vc%2B%2B%E8%AE%BE%E7%BD%AE.png)

然后，配置库目录，添加：...\opencv\build\x64\vc14\lib

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/vc%2B%2B%E5%BA%93%E7%9B%AE%E5%BD%95%E8%AE%BE%E7%BD%AE.png)

然后，C/C++—>常规—>附加包含目录—>编辑添加目录：...\opencv\build\include

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/c%2B%2B%E9%99%84%E5%8A%A0%E7%9B%AE%E5%BD%95%E8%AE%BE%E7%BD%AE.png)

然后，链接器—>输入—>附加依赖项—>添加目录：...\opencv\build\x64\vc14\lib下库的名字：opencv_world340.lib

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E9%93%BE%E6%8E%A5%E5%99%A8%E9%99%84%E5%8A%A0%E4%BE%9D%E8%B5%96%E9%A1%B9%E8%AE%BE%E7%BD%AE.png)

接着，**需要拷贝安装好的CUDA 9.0.props等文件**：

CUDA 9.0.props等文件就在cuda的安装目录下，本人的路径是：C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\extras\visual_studio_integration\MSBuildExtensions

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E9%9C%80%E8%A6%81%E6%8B%B7%E8%B4%9D%E7%9A%84cuda9.0%E7%9A%84%E6%96%87%E4%BB%B6.png)

将里面的所有的文件考本到C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\VC\VCTargets\BuildCustomizations中，这是vs2017安装后的路径

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%B0%86cuda%E6%96%87%E4%BB%B6%E6%8B%B7%E8%B4%9D%E5%88%B0vs%E4%B8%8B%E7%9A%84buildCustomizations%E4%B8%8B.png)

不然可能会报如下错误：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%9B%A0%E4%B8%BA%E6%B2%A1%E6%9C%89%E6%8B%B7%E8%B4%9Dcuda%E6%96%87%E4%BB%B6%E6%8A%A5%E9%94%99.png)

然后，将...\opencv\build\x64\vc14\bin下的opencv_world340.dll 和opencv_ffmpeg340_64.dll 

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%B0%86opencv%E7%9A%84%E6%96%87%E4%BB%B6%E6%8B%B7%E8%B4%9D%E5%88%B0%E9%A1%B9%E7%9B%AE%E4%B8%8B%E7%9A%84x64%E4%B8%AD.png)

复制到E:\darknet\darknet-master\build\darknet\x64 目录下。

最后，还需要修改darknet.vcxproj下158行的compute值,将75改成61，原因貌似是和使用者显卡的计算能力值有关（**这一步小伙伴们可以根据自身情况可以灵活变动**）

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E4%BF%AE%E6%94%B9compute%E5%80%BC.png)

因为我当时配置的时候也参考了别人的帖子，别人75是可以正常进行工程生产，而我需要降低数值才可以，可能我的显卡太菜了/(ㄒoㄒ)/

完成上述之后，就可以在darknet工程上右键—>生成，就会发现在工程目录下x64下多了些darknet.exe等文件啦，到这里就完成了搭建了

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E6%88%90%E5%8A%9F%E7%9A%84%E7%94%9F%E6%88%90.png)

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E7%94%9F%E6%88%90%E7%9A%84darknet.exe.png)

完成搭建，之后就是激动人心的测试环节



# 下载yolo3.weights

- 下载作者训练好的模型：[官网地址](https://pjreddie.com/darknet/yolo/)、[GitHub](https://github.com/AlexeyAB/darknet/blob/master/README.md)下载yolo3.weights

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/github%E4%B8%8B%E7%9A%84yolo%E4%B8%8B%E8%BD%BD%E5%A4%84.png)

为了方便大家，可以直接从我的[网盘，提取码zfib](https://pan.baidu.com/s/1FMXsQW19aSADuDyNF33IhA)下载

下载后放在...\darknet-master\build\darknet\x64目录下

然后进行测试，在当前目录下右键—>在此处打开命令窗口（也可以打开cmd，cd到darknet.exe的目录下），然后输入命令：`darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg`

下面是结果（我用的是自己喜欢的图）：

![](https://raw.githubusercontent.com/RuanZzzz/YOLOv3-for-Windows/master/readmeImages/%E5%B1%9E%E4%BA%8E%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%88%90%E5%8A%9F.png)



