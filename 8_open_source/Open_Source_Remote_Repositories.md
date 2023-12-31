# 开源仓库管理（思路稿）

## 使用场景

总体步骤为：本地开发 -> Coding代码托管 -> GitHub/Gitee开源。

总体思路为：根据分布式仓库的特点，把每个仓库都作为一个独立项目，使用pull request的方式管理。

具体说明如下：
1. 本地开发-> Coding代码托管：最常见的步骤，按照Coding正常的使用方式即可。
2. Coding代码托管 -> GitHub正式开源：Coding内部验证通过以后，手动从本地推送到GitHub。由于GitHub Org的SSH登录需要付费版，而个人SSH又不是特别安全且容易管理（当然企业管理员个人的SSH密钥也不是不行），且目前相关CI CD流程不太熟悉，暂时使用熟悉的手动推送方式。
3. GitHub的PR -> 主分支：暂时使用GitHub正常的方式在本地进行，有成熟方案可以遵循。

以上步骤的前提是以Coding仓库为中心，以GitHub仓库为只读备份（不直接在这个仓库上操作、只做同步）。

不确定手动管理是否会在内部参与人员和社区参与人员增加以后会不会造成比较大的混乱，可以到时候再根据具体情况想解决办法。

## 外部PR管理

主要需要解决的具体问题是，社区向GitHub仓库提交PR的时候，团队也在更新Coding仓库。如何接收PR并加入master分支？一种可能的策略是，增加dev-github分支，PR首先向这个分支提交，然后这个分支被团队合并到主dev分支，最后再提交到master分支上。这样需要：
- 提供详细的分支策略说明，包括：
    - master和dev是保护分支，仅可以从Coding到GitHub同步。
    - 以Coding仓库的dev分支为主dev分支，其他各个分仓库维护用以接收PR的dev-*分支，比如dev-github、dev-gitee等。
    - 外部开发者通过公开仓库提交PR，仓库维护者（即负责的内部成员）合并到dev-*分支，然后内部从本地或者云端（具体流程待定）以dev-*为上游同步所有仓库（只有这个系列的branch上下游策略和其他不同，其他都遵循上述说明）。
- 提供具体的流程控制，包括：
    - 在公开仓库里设置分支保护（如果可以），禁止其他分支提交到master和dev，只允许提交到dev-*分支。
    - 通过**Coding的CI工具约束**以上策略（如果可以）。这是整个方案的关键，约束程度决定了方案的安全性和便捷性。

由于不熟悉Coding和GitHub的分支保护策略，也不熟悉社区在这类问题上的实践，还需要进一步深入研究。

### GitHub分支保护

官方文档：https://docs.github.com/cn/github/administering-a-repository/managing-a-branch-protection-rule

文档里提到的策略都是以人为单位的，似乎没有直接对分支的，不知道如何转化成流程上的约束。

## 社区最佳实践

暂无所需的最佳实践。