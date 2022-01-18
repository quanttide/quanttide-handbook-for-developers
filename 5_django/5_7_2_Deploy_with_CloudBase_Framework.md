# CloudBase Framework部署

首先阅读官方文档：
- 云原生容器应用部署到云开发：https://docs.cloudbase.net/framework/guide/container-app.html
- 云托管部署：https://docs.cloudbase.net/framework/plugins/framework-plugin-container.html
- `cloudbaserc.json`配置说明：https://docs.cloudbase.net/framework/config.html#mo-ban-bian-liang
- 云开发CLI和Framework环境变量配置说明：https://docs.cloudbase.net/cli-v1/config.html#huan-jing-bian-liang

下面说明需要注意的特定问题，请量潮开发者注意遵守内部特定实践规范。

## 开发调试步骤

在开始使用前请务必在本地Docker环境下测试排除Dockerfile的问题;
否则10分钟一次的构建和部署流程以后你会发现你全部白干……

本地安装CloudBase Framework命令行工具：
```
npm install -g @cloudbase/cli@latest
```

用腾讯云密钥登录：
```
cloudbase login --apiKeyId <SECRET_ID> --apiKey <SECRET_KEY>
```

部署到云端：
```
cloudbase framework deploy --mode dev
```
通过mode参数可以调整使用的环境变量。
在云端开发环境中使用`.env.dev`，相比本地开发环境增加了云开发的配置参数；
在预生产环境和生产环境的CI流程中分别使用不在Git内管理的`.env-pre-prod`和`.env.prod`，参考`.env.dev`配置即可。


## 注意

- 资源环境统一在上海。
- 预生产环境和生产环境以不同一个或多个的云开发环境管理。
- 静态网站托管不支持多域名前，采取增加多对云开发环境的方案，或者使用一级域名暂时使用。
- 如果有必要防止不必要的改动，请参考Coding为代码仓库提供的文件锁定功能，详见：https://help.coding.net/docs/host/git/lock.html。