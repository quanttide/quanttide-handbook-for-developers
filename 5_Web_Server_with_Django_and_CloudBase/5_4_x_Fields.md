# Field

## 字符类

包括CharField、EmailField、URLField等。

### null选项

CharField的default为空字符串，null=True时是null。官方文档有对于CharField的null选项的详细说明。

在我们的业务逻辑中，null=True打开以表达用户创建空（空字符串）和系统默认空（None）的区别。

