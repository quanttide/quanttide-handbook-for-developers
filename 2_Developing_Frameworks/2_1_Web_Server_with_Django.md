# Django项目

## 创建Django项目和应用

（对比官方模板描述以下规范，方便开发者直接在官方模板生成的项目基础上修改。）

我们提供了按照如下规则的模板，方便开发者直接使用，详见：
- https://quanttide.coding.net/p/opensource/wiki/101


## Django项目规范

除了官方要求，为了方便部署成云原生应用，我们额外在项目模板增加：
- `Dockerfile`，用以制作容器化环境。
- `cloudbaserc.json`，用以使用CloudBase Framework部署到腾讯云云开发。
- `.env`文件，用以填充环境变量。

不包括以上文件的已有Django项目或者未使用模板生成的项目请手动添加以上文件并参考已有应用或者模板手动配置。


## Django应用规范

### 功能模块

在官方模板的基础上增加serializers.py、permissions.py和urls.py等DRF和Django的常用模块。

### 单元测试

单元测试以Python package的形式组织（官方模板以Python模块的形式组织），package内每个模块对应一个Django应用内的功能模块，以test_<模块名>的格式命名，如test_models.py。

