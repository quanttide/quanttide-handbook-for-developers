# Django项目

## 创建Django项目和应用

（对比官方模板描述以下规范，方便开发者直接在官方模板生成的项目基础上修改。）

我们提供了按照如下规则的模板，方便开发者直接使用，详见：
- https://quanttide.coding.net/p/opensource/wiki/101

如果使用模板生成，对于量潮开发者，请注意：
- 修改默认为项目名称的`cloudbaserc.json`的`serverPath`变量，建议去掉项目命名中的`qt`，比如`users`，以增强API对外可读性。


## Django项目规范

除了官方要求，为了方便部署成云原生应用，我们额外在项目模板增加：
- `Dockerfile`，用以制作容器化环境。
- `cloudbaserc.json`，用以使用CloudBase Framework部署到腾讯云云开发。
- `.env`文件，用以填充公共环境变量。
- `.env.local`文件，用以填充本地开发用的密钥。
- `.env.dev`文件，用以填充云端调试用的密钥。

不包括以上文件的已有Django项目或者未使用模板生成的项目请手动添加以上文件并参考已有应用或者模板手动配置。


## Django应用规范

### 功能模块

在官方模板的基础上增加serializers.py、permissions.py和urls.py等DRF和Django的常用模块。

### 单元测试

单元测试以Python package的形式组织（官方模板以Python模块的形式组织），package内每个模块对应一个Django应用内的功能模块，以test_<模块名>的格式命名，如test_models.py。


## 本地调试

### 本地Docker容器打包调试

Dockerfile运行gunicorn服务的时候注意：
```
exec gunicorn <project-name>.wsgi:application --bind 0.0.0.0:8000
```
注意改成本Django项目的名称。