# 命名规范

## 类命名

通常情况下，各个语言的类名都是采用`QCloudAPIClient`的方式命名。这样的命名在OSRM（地图API）、COS（对象存储）等产品缩写时遇到问题，会出现可读性比较差的“OSRMAPIClient”的命名。

我们讨论了“OsrmApiClient”和“OsrmAPIClient”，最终打算采用后者，对于API、SDK等行业通用的概念，保留大写缩写以提高可读性。

因此，关于类名的大小写规范明确如下：

- 通常情况下使用“ClassName”即可。
- 对于行业通用的概念，比如API、SDK等，在类名中保留其全大写；对于OSRM、COS、EIAM等产品名称，则使用首字母大写的方式。比如`OsrmAPIClient`。
