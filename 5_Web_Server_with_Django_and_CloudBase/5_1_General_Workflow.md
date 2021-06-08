# Django项目

## 创建Django项目和应用

（对比官方模板描述以下规范，方便开发者直接在官方模板生成的项目基础上修改。）

我们提供了按照如下规则的模板，方便开发者直接使用，详见：
- https://quanttide.coding.net/p/opensource/wiki/101

如果使用模板生成，对于量潮开发者，请注意：
- 修改默认为项目名称的`cloudbaserc.json`的`serverPath`变量，建议去掉项目命名中的`qt`，比如`users`，以增强API对外可读性。


## 本地调试

### 本地Docker容器打包调试

Dockerfile运行gunicorn服务的时候注意：
```
exec gunicorn <project-name>.wsgi:application --bind 0.0.0.0:8000
```
注意改成本Django项目的名称。