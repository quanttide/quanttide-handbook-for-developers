### Android Studio

作用：开发安卓APP，目前内部用于基于Flutter开发跨端APP

##### 1.下载地址

[Download Android Studio and SDK tools   Android Developers](https://developer.android.google.cn/studio)

##### 2.安装及使用教程

[Android Studio超详细安装教程 - 知乎](https://zhuanlan.zhihu.com/p/80051318)

[android studio安装教程，史上最详细(超多图)！！_piupiu78的博客-CSDN博客_android studio安装教程](https://blog.csdn.net/piupiu78/article/details/112170085)

##### 3.插件安装教程（我们目前只要求安装Flutter与Dart）

[Android Studio如何安装插件-百度经验](https://jingyan.baidu.com/article/a24b33cdb5b39a58ff002b60.html)

[AndroidStudio手动安装插件 - TongMeng - 博客园](https://www.cnblogs.com/yjpjy/p/11525511.html)

##### 4.插件市场

[Plugins  JetBrains](http://plugins.jetbrains.com/androidstudio)



### FLutter

作用：Android Studio中Flutter插件的使用需要

##### 1.下载地址及配置教程

[起步:安装Flutter  - Flutter中文网 ](https://flutterchina.club/get-started/install/)

[Flutter入门——安装与开发环境配置 - 知乎](https://zhuanlan.zhihu.com/p/110208018)的前两个部分

##### 2.在Flutter命令行输入flutter doctor可能出现的问题的解决

2.1.Unable to 'pub upgrade' flutter tool

[Unable to 'pub upgrade' flutter tool. Retrying in five seconds_yangchenglangzi的博客-CSDN博客](https://blog.csdn.net/yangchenglangzi/article/details/89981488)

2.2.✗ Flutter plugin not installed; this adds Flutter specific functionality.

   	✗ Dart plugin not installed; this adds Dart specific functionality

非常麻烦的报错，已收集到的解决方法有三种，第一种不行试第二种，第二种不行试第三种

第一种的问题是未安装插件

[Error: Flutter plugin not installed; this adds Flutter specific functionality. - Flutter_survivorsfyh的博客-CSDN博客](https://blog.csdn.net/survivorsfyh/article/details/93407580)

第二种的问题是插件的版本与Android Studio的版本不匹配

[Android Studio 3.5以后 Plugins中搜索不到flutter插件，本地无法安装？？_okeyzero的博客-CSDN博客](https://blog.csdn.net/weixin_43695321/article/details/104932287)

第三种的问题是Flutter检查插件是否安装时检查的位置是错误的，需要手动修改

[Android Studio (version 4.1) ✗ Flutter plugin not installed; this adds Flutter specific functiona... - 简书](https://www.jianshu.com/p/03201f4f69f6)

2.3卡在Running pub upgrade状态

[Flutter:  Running pub upgrade.. Flutter Setup:Building flutter tool..._a1050762704的博客-CSDN博客](https://blog.csdn.net/a1050762704/article/details/106250840)

2.4这篇文章总结了作者在配置Flutter过程中遇到的所有问题，可以帮助你更准确的定位你的问题

[flutter 安装以及遇到的坑 - 简书](https://www.jianshu.com/p/4836bcbc8b38)