# Django项目

## 创建Django项目和应用

对比官方模板描述以下规范，方便开发者直接在官方模板生成的项目基础上修改。我们提供了按照如下规则的模板，方便开发者直接使用。

## Django项目规范

## Django应用规范

### 功能模块

在官方模板的基础上增加serializers.py、permissions.py和urls.py等DRF和Django的常用模块。

### 单元测试

单元测试以Python package的形式组织（官方模板以Python模块的形式组织），package内每个模块对应一个Django应用内的功能模块，以test_<模块名>的格式命名，如test_models.py。

## 参考资料

自定义模板的使用方式详见： https://quanttide.coding.net/p/opensource/wiki/101。