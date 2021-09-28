# Django工程规范

## 创建Django项目和应用

（对比官方模板描述以下规范，方便开发者直接在官方模板生成的项目基础上修改。）

我们提供了按照如下规则的模板，方便开发者直接使用，详见：
- https://quanttide.coding.net/p/opensource/wiki/101

如果使用模板生成，对于量潮开发者，请注意：
- 修改默认为项目名称的`cloudbaserc.json`的`serverPath`变量，建议去掉项目命名中的`qt`，比如`users`，以增强API对外可读性。


## PyCharm的工具箱

- 设置manage.py路径和使用manage.py命令行工具。
- 设置settings.py路径。
- 使用Django Tests和DEBUG功能调试。
- 使用可运行Django的Python Console调试用例。


## 部署前本地调试

建议开发者遵循以下顺序调试：
1. 本地运行Django服务，检验Django服务是否正常运行。
2. 本地运行Docker打包镜像，检验Django服务容器化是否正常。
3. 本地运行CloudBase Framework部署，检验持续部署流程是否正常。

### 本地运行Django服务

略。

### 本地Docker容器打包调试

Dockerfile运行gunicorn服务的时候注意：
```
exec gunicorn <project-name>.wsgi:application --bind 0.0.0.0:8000
```
注意改成本Django项目的名称。


### 本地运行CloudBase Framework

详见[CloudBase Framework部署](./5_6_2_Deploy_with_CloudBase_Framework.md)