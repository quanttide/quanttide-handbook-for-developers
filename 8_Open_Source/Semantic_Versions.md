# 语义化版本号

## 介绍

详见：https://semver.org/lang/zh-CN/

## ChangeLog的格式

详见：https://www.jianshu.com/p/622b5f57b965

## Fork项目的版本号

用于以后开源项目的私有版本。

根据语义化版本，规则如下：
- bugfix，增加小版本号
- small new feature，增加中版本号
- 其他，增加大版本号

实际开发中，如果是小的改动，通常指需要增加小版本号和中版本号，并且不定期维护即可。如果是大的改动（比如video_player），可以采用先改中小版本，再跳过现有版本号改大版本的方案。

这里参考了MariaDB作为MySQL的fork项目的策略。一开始，他们的接口完全兼容MySQL，只是代码重新，所以采用了MySQL的5.x。在根本的更变发生以后，他们切换到自己的10.x版本。

