---
title: 基本框架
author: 张果
created_date: 2021-08-16
updated_date: 2021-08-16
---

# 基本框架

## 文件结构

这里使用Markdown格式表达的项目文件和文件夹结构，其中`<dir_name>/`表示文件夹。

```markdown
- README.md
- docs/
  - README.md
  - tutorials/ (optional)
  - dev/ (optional)
- .env
- .gitignore
```

## 项目README

README文件按照标准README规范即可。必须有的内容包括：
- 项目负责人（Owner）和复核人（Reviewer），明确责任人。
- 项目文件夹和文件结构，基于上面的标准进一步明确各个云函数等资源的功能。
- 项目需求或交付目标，明确最终交付给客户的数据、代码、文档等资源的具体内容和具体形式。

一个README示例如下：

```markdown
# README

## 目标

- 实现某需求的算法及GUI。

## 责任人

- 负责人（Owner）：张三
- 复核人（Reviewer）：李四

## 文件结构

- ...
- `analytics.py`: 算法模块
- `gui.py`: GUI模块
- ...
```

## 文档`docs`

包括README.md和若干Markdown文档。其中：
- 文档`README.md`。必须有，需要对客户可读，主要介绍此项目的需求和方案，在项目初期完善、在团队内部达成共识、和客户达成共识以后，才应该开始推进开发工作。
- Markdown文档。根据项目说明需要添加即可，对于项目的一些关键问题和对应解决方案分类说明，比如算法部分、GUI部分等。建议尽可能把文档和模块一一对应，以方便阅读和验证。

对于给开发者使用的依赖包项目，区分用户文档`tutorials/`和开发设计文档`dev/`，只有业务逻辑的自建应用或客户项目无需如此区分，实际上只有开发设计文档。


## 环境变量

`.env`文件（也可以是`*.env`或`.env.*`），此格式为云原生项目的标准。

环境变量在本地项目配置并加入`.gitignore`，在云端通过构建计划的环境变量传入。


## Git配置

`.gitignore`文件配置参考[.gitignore文件规范](../2_General_Principles_for_DevOps/2_2_z_gitignore.md)
