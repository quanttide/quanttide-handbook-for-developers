# 函数计算

## Python依赖配置

相关资源包括：

- 项目根目录的`requirements.txt`。
- 项目根目录的`install_scf_requirements.py`
- 各个云函数的`requirements.txt`。

其中：

- 项目根目录的`requirements.txt`不在云函数部署时使用，主要是为了方便在本地开发时在PyCharm或者VSCode中自动下载通过Layer配置的Python依赖。
- Coding的团队构建模板“函数计算项目”的“构建”步骤运行`install_scf_requirements.py`，把各个云函数配置的`requirements.txt`中的依赖下载到云函数同级文件夹以后部署。因此各个云函数配置的`requirements.txt`应当配置不在设置的层（Layer）中存在的此云函数Python依赖。

<!--
围绕Sls Fmw的SCF的sls.yml来。
● 环境变量
● 层管理
● 其他必要配置，想到再补充，项目里总结。
-->
