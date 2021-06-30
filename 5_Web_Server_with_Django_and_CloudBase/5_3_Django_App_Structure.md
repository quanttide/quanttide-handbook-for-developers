## Django应用规范

### 功能模块

在官方模板的基础上增加serializers.py、permissions.py和urls.py等DRF和Django的常用模块。

### 单元测试

单元测试以Python package的形式组织（官方模板以Python模块的形式组织），package内每个模块对应一个Django应用内的功能模块，以test_<模块名>的格式命名，如test_models.py。

