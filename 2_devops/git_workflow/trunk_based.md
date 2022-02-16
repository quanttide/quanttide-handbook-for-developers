# 主干分支

本文接着上一篇，主要讲如何把特性分支改为主干分支。

## 配置CI触发规则

发布规则如下：

1. alpha发布在开发环境。版本号为x.x.x-alpha().x)
2. beta发布在预生产环境。版本号为x.x.x-beta(.x)
3. pre-release和release发布在生产环境。版本号为x.x.x-rc(.x)或者x.x.x。

### 正则表达式

用语义化版本正则表达式工具制作。暂不清楚为什么不可用。

正式版：

```regex
^refs/tags/(?P<major>0|[1-9]\d*)\.(?P<minor>0|[1-9]\d*)\.(?P<patch>0|[1-9]\d*)$
```

Alpha+:

```regex
^refs/tags/(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)(?:-(?:alpha|beta|rc)(?:\.(?:0|[1-9]\d*))?)?$
```

Beta+:

```regex
^refs/tags/(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)(?:-(?:beta|rc)(?:\.(?:0|[1-9]\d*))?)?$
```

RC+:

```regex
^refs/tags/(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)\.(?:0|[1-9]\d*)(?:-(?:rc)(?:\.(?:0|[1-9]\d*))?)?$
```

## 参考资料

主干分支：https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development

语义化版本：

- https://semver.org/lang/zh-CN/spec/v2.0.0.html
- 正则工具：https://regex101.com/r/Ly7O1x/3/
