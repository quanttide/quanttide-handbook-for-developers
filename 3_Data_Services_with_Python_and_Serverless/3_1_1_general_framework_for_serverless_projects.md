---
title: 函数计算项目框架
author: 张果
created_date: 2021-08-16
updated_date: 2021-08-16
---

# 函数计算项目框架

[//]: #(开头这段话写的不好，根据读者阅读体验改。)

本讲介绍函数计算项目的文件结构，在这个框架的基础上规定基本的函数计算项目使用规范。制定此框架的主要原因是方便在使用Serverless Framework部署时让它识别，框架并没有强制规定而只是有一系列识别逻辑。此框架主要参考Serverless Framework提供的对Node.js项目结构的建议（https://cloud.tencent.com/document/product/1154/51119）的思路。


## 文件结构

这里使用Markdown格式表达的项目文件和文件夹结构，其中`<dir_name>/`表示文件夹。

```markdown
- README.md
- serverless.yml
- install_scf_requirements.py (recommended)
- requirements.txt (optional)
- .env (ignored)
- .gitignore
- <scf>/
  - index.py
  - requirements.txt (recommended)
  - serverless.yml
  - <module>.py (optional)
  - <package> (optional)
    - __init__.py 
    - <module>.py 
- db/ (recommended)
  - serverless.yml
- cos/ (recommended)
  - serverless.yml 
- workflow/ (recommended)
  - workflow.json
  - serverless.yml
- docs/
  - README.md
  - <section>/ (recommended)
    - <doc>.md
  - <doc>.md (recommended)
```

注意：
- recommended标记表示尽量有或者大部分情况会有，建议开发者处理；optional表示可选，不需要可以不用；不标记的为必须。
- 云函数（`<scf>/`文件夹）可以有单个也可以有多个。因此此项目规范实际上不像官方文档给的建议一样区分单项目和多项目。
- 每个云函数下可以有0-N个Python模块或包（`<module>.py`文件和`<package>`文件夹），根据项目需要决定即可。
- 文档文件夹下可以有多个文件夹(`<section>`/)和文件（<doc>.md），用Markdown格式写即可。

可以参考根据此规范制作的Outdoorsy项目代码：https://quanttide.coding.net/p/qtservices-lixiang-outdoorsy/d/outdoorsy-images-crawler-serverless/git

下面详细阐述整个项目各个部分构成。


## 文档

### 项目README

README文件按照标准README规范即可。必须有的内容包括：
- 项目负责人（Owner）和复核人（Reviewer），明确责任人。
- 项目文件夹和文件结构，基于上面的标准进一步明确各个云函数等资源的功能。
- 项目需求或交付目标，明确最终交付给客户的数据、代码、文档等资源的具体内容和具体形式。

一个README示例如下：
```markdown
# README

## 交付目标

- 数据：SQL表<table_name>。
- 代码：本项目。
- 文档：本项目文档文件夹。

## 责任人

- 负责人（Owner）：张三
- 复核人（Reviewer）：李四

## 文件结构

[//]: # (这里只以云函数部分举例)

- ...
- `goods/`: 采集某网站的商品
- `comments/`: 采集某网站的评论 
- ...


```

### 文档文件夹`docs`

包括README.md和若干Markdown文档。其中：
- 文档`README.md`。必须有，需要对客户可读，主要介绍此项目的需求和方案，在项目初期完善、在团队内部达成共识、和客户达成共识以后，才应该开始推进开发工作。
- Markdown文档。根据项目说明需要添加即可，对于项目的一些关键问题和对应解决方案分类说明，比如算法部分、GUI部分等。

## Python依赖配置

相关资源包括：
- 项目根目录的`requirements.txt`。
- 项目根目录的`install_scf_requirements.py`
- 各个云函数的`requirements.txt`。

其中：
- 项目根目录的`requirements.txt`不在云函数部署时使用，主要是为了方便在本地开发时在PyCharm或者VSCode中自动下载通过Layer配置的Python依赖。
- Coding的团队构建模板“函数计算项目”的“构建”步骤运行`install_scf_requirements.py`，把各个云函数配置的`requirements.txt`中的依赖下载到云函数同级文件夹以后部署。因此各个云函数配置的`requirements.txt`应当配置不在设置的层（Layer）中存在的此云函数Python依赖。

## Serverless Framework配置

相关资源包括：
- 项目根目录的`serverless.yml`
- 各个云资源文件夹的`serverless.yml`

Serverless Framework识别`serverless.yml`的方式是，用项目根目录中的配置**覆盖**各个云资源文件夹的配置。（PS：此配置十分反人类，腾讯云已经和Serverless Framework反馈，未来有一定可能改变。）基于此规则，我们的实践方式是只在根目录配置少量项目约束层面的参数，包括默认地域、私有网络等，其他情况尽可能不用（也用不到）。云资源文件夹的配置方式在后面几篇详细说明。

## 环境变量

`.env`文件（也可以是`*.env`或`.env.*`）。

环境变量在本地项目配置并加入`.gitignore`。上述团队模板在“部署”步骤从构建环境的环境变量生成临时`.env`，需要开发者维护各个项目的构建计划指定写入环境变量文件的具体环境变量，操作方法在后面介绍。

## Git配置

`.gitignore`文件应当设置：
- 环境变量：`.env`（最好加`*.env`和`.env.*`）
- IDE配置：`.vscode`、`.idea`。
- Python相关
- 其他必要文件

[//]: #(如果需再补充)