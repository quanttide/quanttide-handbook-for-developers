# Git工作流

我们内部主要使用[GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)和[GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)。

GitHub Flow主要用于语言和框架依赖库或无需多套云资源（环境）的客户项目，GitLab Flow主要用于需要多套云资源部署的自建或客户服务端和客户端项目。GitHub Flow和GitLab Flow的边界主要在于是否需要多套环境。

## GitHub Flow

GitHub Flow要求只有一个`master`长期分支，其他的短期分支都是feature分支，核心机制是通过PR机制把feature分支的代码提交到`master`分支。完整的流程为：
1. 创建一个新feature分支。
2. 在此feature分支上提交（commit）修改。
3. 创建一个合并请求（pull request）。
4. 代码评审（code review）和合并代码（merge）。
5. 删除feature分支。

在Coding中我们常使用“保护分支”对`master`等长期分支进行约束，并通过其一系列设置来保证长期分支的代码质量，包括代码扫描和CI自动化测试、必须通过管理员代码评审等。是否禁止管理员直接提交代码到长期你分支可根据项目实际情况决定，一般原则是稳定性要求越高、自动化测试覆盖越完善，越需要牺牲敏捷性禁止直接提交。保护分支的规则设置主要取决于稳定性和敏捷性的平衡，根据具体项目制定。

在此实践下，feature分支应当只存在**数小时到一两天**。请项目责任人（Owner和Reviewer）特别注意合并和删除团队代码仓库的短期feature分支，项目参与者每次开发必须从**最新的**`master`分支拉取创建新分支或者合并到现有feature分支，以避免新提交和`master`分支发生冲突影响效率。

开发者在本地应当熟练使用fetch和pull拉取云端`master`分支到本地`master`分支。在本地保持跟踪云端的分支命名和云端一致。准备push到云端的feature分支在本地可以通过compare diff等方式确保可提交到云端`master`分支（而不是本地`master`分支）。其他建议实践根据开发者实践再进行进一步总结。


## 从GitHub Flow升级到GitLab Flow

GitLab Flow官方文档对于GitHub Flow的缺点阐述如下：
> GitHub flow assumes you can deploy to production every time you merge a feature branch. > While this is possible in some cases, such as SaaS applications, there are some cases 
> where this is not possible, such as:
> - You don’t control the timing of a release. For example, an iOS application that is  
> released when it passes App Store validation.
> - You have deployment windows - for example, workdays from 10 AM to 4 PM when the
> operations team is at full capacity - but you also merge code at other times.

在我们内部，最常见的需求是隔离：
- 开发者在开发调试过程中使用的开发环境资源
- 测试或上线的预生产或生产资源。

常见的场景是：
- 自建应用，主要是部署在腾讯云云开发产品线的量潮应用系统的各个应用。
- 函数计算应用，主要是部署在腾讯云Serverless产品线的数据服务业务的大数据类项目。

从GitHub Flow升级到GitLab Flow的主要步骤如下：
1. 增加两个长期分支，预生产分支`pre-production`和生产分支`production`，他们在GitLab Flow被称为环境分支。主分支`master`、预生产分支`pre-production`、生产分支`production`分别对应云计算资源的开发环境、预生产环境（测试环境）、生产环境。
2. 改变版本发布策略。（PS：还需要进一步研究。）

云计算资源主要通过命名区分，具体规则如下：
- 在云开发的“环境”中，我们通常以`<system_name>-<env>`命名，其中`<env>`可选开发环境`dev`（比如`qtapps-dev`）、预生产/测试环境`testing`、生产环境`production`。在代码中，使用`ENV`环境变量，可选开发环境`dev`、预生产环境`pre-prod`、生产环境`prod`。
- 在函数计算项目中，遵循Serverless Framework文档提供的规范，使用`STAGE`环境变量，可选开发环境`dev`、预生产/测试环境`testing`、生产环境`master`。（PS：使用master命名生产环境比较容易迷惑，在其他地方我们尽可能不适用。）

同类框架命名一定要有统一的规则，所有开发者一定要**遵循共同的内部命名规范**，以方便开发者理解和后续被代码识别。

官方文档提供了一些指导：
- Serverless Framework建议的开发和发布流程如下：https://cloud.tencent.com/document/product/1154/47288。
- CloudBase文档没有类似流程，只有云原生应用标准。可以参考容器应用基于12-factors原则的实践资料。
