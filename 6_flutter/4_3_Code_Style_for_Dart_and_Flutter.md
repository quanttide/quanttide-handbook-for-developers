# Dart和Flutter项目代码规范

## 项目结构

https://book.flutterchina.club/chapter15/code_structure.html


## 组件嵌套顺序

（TODO）初步思路：

变化的套在外面，不变的套在里面。

大概按照UX > UI动效 > UI比例 > UI颜色的顺序。

比如视频播放器：
InteractiveView，SafeArea，AspectRatio。

2021.02.26更新：这样似乎不太对，SafeArea似乎应该嵌套在InteractiveView外面。这么看UX似乎放在内部比较合适。
