---
layout: post
title:  "安装ObjectARX"
date:   2020-01-10 18:45:42 +0800

categories: arx
---	

## **需要的工具**

1. AutoCAD

2. ObjectARX

3. Visual Studio

## **ARX和VS的版本对应**

| AutoCAD       | ARX版本       | Visual Studio | 版本    |
| ------------- | ------------- | ------------- | ------- |
| AutoCAD(R12)  | ARX1          | VC            | VC2     |
| AutoCAD(R14)  | ARX202        | VC            | VC4.2   |
| AutoCAD2000/2 | ObjectARX2002 | VC            | VC6.0   |
| AutoCAD2004   | ObjectARX2004 | VS2002        | VC7.0   |
| AutoCAD2005   | ObjectARX2005 | VS2002        | VC7.1   |
| AutoCAD2006   | ObjectARX2006 | VS2002        | VC7.1   |
| AutoCAD2007   | ObjectARX2007 | VS2005        | VC8.0   |
| AutoCAD2008   | ObjectARX2008 | VS2005        | VC8.0   |
| AutoCAD2009   | ObjectARX2009 | VS2005        | VC8.0   |
| AutoCAD2010   | ObjectARX2010 | VS2008        | VC9.0   |
| AutoCAD2011   | ObjectARX2011 | VS2008        | VC9.0   |
| AutoCAD2012   | ObjectARX2012 | VS2008        | VC9.0   |
| AutoCAD2013   | ObjectARX2013 | VS2010        | VC10.0  |
| AutoCAD2014   | ObjectARX2014 | VS2010/2012   | VC10/11 |
| AutoCAD2015   | ObjectARX2015 | VS2012        | VC11.0  |
| AutoCAD2016   | ObjectARX2016 | VS2012/2013   | VC11/12 |
| AutoCAD2017   | ObjectARX2017 | VS2015        | VC13.0  |

[Reference](https://blog.csdn.net/a_222850215/article/details/79608721)

## **安装过程**

### **安装VS和AutoCAD**

这个正常安装就行。

### **安装ObjectARX**

[ObjectARX 2017 Wizard](http://images.autodesk.com/adsk/files/ObjectARXWizards-2017.zip) - [2017 SDK](http://download.autodesk.com/esd/objectarx/2017/Autodesk_ObjectARX_2017_Win_64_and_32_Bit.sfx.exe)

[ObjectARX 2018 Wizard](http://images.autodesk.com/adsk/files/ObjectARXWizards-2018.zip) - [2018 SDK](http://download.autodesk.com/esd/objectarx/2018/Autodesk_ObjectARX_2018_Win_64_and_32_Bit.sfx.exe)

[ObjectARX 2019 Wizard](http://damassets.autodesk.net/content/dam/autodesk/www/adn/files/ObjectARXWizard2019.zip) - [2019 SDK](http://download.autodesk.com/esd/objectarx/2019/Autodesk_ObjectARX_2019_Win_64_and_32_Bit.sfx.exe)

[ObjectARX 2020 Wizard](https://github.com/ADN-DevTech/ObjectARX-Wizards/raw/ForAutoCAD2020/ObjectARXWizardsInstaller/ObjectARXWizard2020.zip) - [2020 SDK](http://download.autodesk.com/esd/objectarx/2020/objectarx_for_autocad_2020_win_64_bit.sfx.exe)

其他低版本的可以自行搜索对应的包。

**有些低版本的包只有一个安装包**，例如ObjectARX2010，只有一个安装包，直接解压后的utils下的ObjARXWiz有可安装的msi文件，直接安装（管理员安装）即可。

![ArxWizards](//gitee.com/veboce/ini_file/raw/master/ArxWizards.png)

**注：**管理员安装：可以管理员执行cmd程序，然后把ArxWizards.msi文件拖进窗口执行即可

**如果是上面那种Wizard + SDK的**，这样的安装有一些注意点。先执行SDK程序解压到指定的文件夹后，再（管理员）安装ObjectARXWizards.msi，这个ObjectARXWizards.msi不同于上面的，他的安装需要手动指定SDK的目录和AutoCAD的安装目录（它有个默认值，注意更改），如果选择错误将会导致创建项目失败。

SDK的位置，应选择到你解压位置下的目录（注意包含该位置下的目录，比如解压到了C:\Autodesk，解压后的目录叫Autodesk_ObjectARX_2017，那么SDK的目录就应该是C:\Autodesk\Autodesk_ObjectARX_2017，而不是C:\Autodesk），AutoCAD的位置要选择你CAD实际安装位置的根目录，最好的方法是鼠标右键打开CAD的位置（打开位置后如果显示的是快捷方式，则再打开一次位置），如下图，选择画圈的路径。

![](//gitee.com/veboce/ini_file/raw/master/arx_cad_path.png)

## **创建过程**

**如果**配置SDK路径和CAD路径正确，仍创建ARX项目失败，向下看：

原因是VS安装目录下的 `VC/VCProjects/Autodesk` 下的；**两个vsz后缀的文本文件配置有错误**。

![vsz_ini_file](//gitee.com/veboce/ini_file/raw/master/vsz_ini_file.png)

下图应该是当前你的配置其中一个文件信息（如果配置SDK路径和CAD路径正确，仍创建失败）：

![错误信息](//gitee.com/veboce/ini_file/raw/master/arx_vsz_err_ini.png)

即两个vsz文件的内容**分别**：①将上图中的第二行的`[WIZVERSION]`改成对应版本号，和VS版本有关系。如果是vs2012，对应数字是11.0，同理vs2013-12.0，vs2015-14.0，②将第4行的`[TARGETDIR]`改成下图的路径，**只更改中括号及中括号内容，其他不要动**。

![正确路径](//gitee.com/veboce/ini_file/raw/master/arxAppWiz_vsz_right.png)

这是配置正确后的其中一个文件的截图：

![](//gitee.com/veboce/ini_file/raw/master/arxAppWiz_vsz.png)

最后创建项目成功了，如果要是出现无限创建项目，即创建完了不进入项目又自动重新创建并同时提示安装C++ 2015等信息，这是由于VS默认不安装C++相关，在`新建项目`-->`Visual C++`中安装C++ 2015工具包即可，如下图内容介绍：

![安装扩展](//gitee.com/veboce/ini_file/raw/master/vs_install_c++.png)

## **添加类过程**

如果在向ARX项目中添项目报错。

### **添加ObjectArxMFCsupport等类报错**

#### **报文档顶层存在无效内容**

这是由于配置文件内容错误导致的。

找到`VS安装目录下`的`VC/VCAddClass/ObjectARX`中的以vsz结尾的文件，发现内容与无法创建项目时的相关文件情况一样，是不正确的。

编辑他们，更改为正确的内容，原理同上文中无法创建项目。

### **添加类配置文件正确后报没有Additem方法等问题**

上述vsz配置文件填入正确的内容后，又出现无additem方法等脚本错误问题，并且错误报告位置为default.html文档，且强制继续后，界面出现图标缺失，下拉值为空等问题。

原因在**该default.html文档中，的classid=这一行的CLASSID有问题**。

![CLASSID问题](//gitee.com/veboce/ini_file/raw/master/arx_classid.png)

此文中使用的是ObjectARX2017，对应在网上找到的ID号是：

`087da97a-e2f4-472a-bb48-0bcdfaa20fb3`

其他版本，可以去网上找对应的ID号即可。