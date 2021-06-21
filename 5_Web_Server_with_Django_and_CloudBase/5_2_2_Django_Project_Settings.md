# Django项目配置文件

根据官方规范，Django配置文件通常在项目根目录的<project_name>/settings.py。

## 社区规范

### Django默认支持设置

Django官方提供的参数遵循官方文档即可，详见：
- 原理介绍：https://docs.djangoproject.com/en/3.1/topics/settings/
- 参数列表：https://docs.djangoproject.com/en/3.1/ref/settings/

其中，查找具体参数请参考“参数列表”；理解Django settings工作原理用以完善单元测试或者自建Django包请参考“原理介绍”。


### Django REST Framework支持设置

DRF的参数配置在`REST_FRAMEWORK`变量，以字典方式传入具体值。

DRF官方提供的参数遵循DRF官方文档接口，详见：
- https://www.django-rest-framework.org/api-guide/settings/

具体的参数含义需要参考各个部分API文档。

### 其他第三方Django应用

参考各个Django应用提供的文档规范即可。


## 内部规范

以下所有变量已经在Django项目模板中实现，详见：
- https://quanttide.coding.net/p/qtapps-django/d/django-project-template/git/tree/master/project_name/settings.py

下面再对项目模板中实现的关键变量详细说明。如果想了解全部参数的内部默认设置，或者想了解以下参数的实现方式，请阅读源码。

### ENV 环境标记

可选：
- `dev`: 开发环境。此时`IS_DEV_ENV`为`True`，`IS_DEPLOY_ENV`为`False`。
- `pre-prod`: 预生产环境。`IS_DEPLOY_ENV`为`True`，`IS_DEV_ENV`为`False`，`IS_PRE_PROD_ENV`为`True`。
- `prod`: 生产环境。此时`IS_DEPLOY_ENV`为`True`，`IS_DEV_ENV`为`False`，`IS_PROD_ENV`为`True`。

### DEBUG 调试标记（官方）

在我们制作的内部模板中，我们把`DEBUG`和`ENV`环境标记关联起来：
- 当`ENV`为预生产环境(`pre-prod`)或者生产环境(`prod`)时，`DEBUG`强制为`False`。
- 当`ENV`为开发环境(`dev`)时，`DEBUG`可根据开发者在环境变量中的设置调整；在本地开发环境中通常设置为`True`，云端CI中通常设置为`False`，其他情况根据需要调节。

### TODO

- 如果有其他变量需要说明，再继续完善本部分。