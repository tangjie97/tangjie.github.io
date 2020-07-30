---
typora-root-url: ..\posts_image
typora-copy-images-to: ..\posts_image
---

---
layout: post
title:  "VS生成动态链接库MATLAB调用"
date:   2020-07-30 23:31:42 +0800

categories: VS、MATLAB
---	

## **需要的工具**

1. VS
2. MATLAB

## **一、VS设置**

首先，打开你的VS项目，配置管理器，如果你需要生成32位dll则不需要动，如果你需要**生成64位dll则需要将其配置管理器的平台改为x64**。

![](/posts_image/2-1.png)

注释掉你的主函数，接下来在你的**函数前方添加extern "C" __declspec(dllexport)**。其中extern "C"是针对C++也就是.cpp文件添加的，如果是.c则无需添加。

![](/posts_image/2-2.png)

之后需要修改项目属性里的**目标文件扩展，均改为dll**。

![](/posts_image/2-3.png)

接下来重新生成项目，生成后的dll存储在相应的路径里。

![](/posts_image/2-4.png)

## **二、编写dll动态链接库调用头文件**

**在新建的头文件中添加所需要用到的函数**。

![](/posts_image/2-5.png)

## **三、MATLAB加载模型及调用**

MATLAB加载模型语句及卸载如下图所示，一般出现模型输出问题可能是多次运行程序而未卸载库导致。

![](/posts_image/2-6.png)

## 四、常见问题

### 1、未找到支持的编译器

可能原因：1）编译器未安装，需要根据MATLAB版本安装合适的编译器。

​					2）VS版本与MATLAB版本相差过大，如VS2010与MATLAB2019b。需要安装版本相近的VS。

​					3）编译器未配置，在MATLAB命令窗口输入：mex -setup。若提示未找到编译器可能是前两种情							况，否则设置C++编译器。

*未完待续。。*