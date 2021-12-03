---
title: `.gitignore`文件规范
author: 张果
created_date: 2021-08-17
updated_date: 2021-08-17
---

# `.gitignore`文件规范

## IDE配置

```text
# IDE config
.vscode/  # VSCode
.idea/  # PyCharm
```

IDE配置过滤有利于防止不同机器和不同开发者导入IDE时可能出现的配置异常。

我们希望可以让内部开发者更灵活地选择自己趁手的IDE和建立自己的开发习惯，无需完全保持一致。


## 环境变量

```text
# env files
.env
*.env
.env.*
```

`*`是通配符，这里表示任何以`.env`结尾或者开头的文件也会被过滤。

云原生标准项目分为代码、声明式配置、环境变量三个部分。环境变量文件一般本地文件使用，通过IDE插件或者语言或框架依赖库导入。环境变量文件通常包括关系到系统安全的关键密钥，因此必须过滤到

在CloudBase项目中`.env`文件的使用略不同。由于CloudBase支持导入`.env`和`.env.<mode>`且后者可以覆盖前者，因此`.env`文件**不过滤**用以放一些多次使用但不太变化的非敏感配置（比如项目名称`PROJECT_NAME=<qtapp>`），在本地开发使用`.env.local`、在本地调试云端开发环境使用`.env.dev`。


## Python

```text
# Python
venv/  # 虚拟环境
```

这里仅列举常用的，后续需要开发者根据项目需要逐步补充。

不建议手动添加，建议使用以下几种方式：
- 在Coding生成`.gitignore`文件时选择“Python语言模板”生成。
- 使用PyCharm或VSCode的`.gitignore`插件自动生成，方法百度搜索教程或官方文档即可。
- 复制GitHub提供的完整的列表：https://github.com/github/gitignore/blob/master/Python.gitignore。
