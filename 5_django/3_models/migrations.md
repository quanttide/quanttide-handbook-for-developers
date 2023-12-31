# Django数据库迁移

## 关注点

使用Migration的原因见[文章](https://nextlinklabs.com/insights/naming-django-migrations-improving-projects)给的理由。

## 流程

### 本地开发环境

每轮更新`Model`以后，执行下述操作：

1. 执行`makemigrations`生成迁移文件。
2. 把新迁移文件手动编写到云端未提交的迁移中。主要目的是减少`migration`文件，方便手动维护和写数据库变更文档。
3. 通过`migrate`命令指定应用和迁移文件编号的方式回退到上个版本后重新运行迁移。

### 云端开发环境

- 手动维护关联使之符合迁移命令运行要求。
- 不行就删库重新创建。

### 云端预生产环境

还可以删库重建，但生产环境不能这么干，需要为生产环境预演更合适的方案。

### 云端生产环境

手动切换流量。

考虑制定蓝绿数据库的方案。已经看到一些社区实践。

## 注意事项

### 命名迁移文件

为每一个migration文件命名一个可读的名字，类似于Django官方应用做的。

命名风格统一采用官方习惯的动名词短语。

### 避免删除字段

云端环境处理删除字段和表的操作容易异常。云开发采取重试10次的方式（实际上是初始化启动10个实例），如果迁移异常导致记录没有进入数据库，下次迁移再执行删除字段就会异常。且正式数据库和测试数据库都会执行一遍。

云端数据库目前缺乏运行命令行工具的方法，数据库做了迁移以后无法运行回退命令。

在没有成熟的方法之前，只能遵循云原生对数据库的实践“只增加不删除”。避免预留的表和字段进入数据库，通过禁止迁移等方式处理。

## 问题

### 官方Auth应用

有几张表且和其他应用耦合，但DRF里用不到这几张表，最好是可以拆掉。

目前看只能手动在Dockerfile指定迁移的Django应用，没办法通过参数设置auth应用的表不迁移。
