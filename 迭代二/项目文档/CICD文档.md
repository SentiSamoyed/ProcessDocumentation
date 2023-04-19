# CI/CD 文档

| 变更人 | 变更日期   | 变更内容 |
| ------ | ---------- | -------- |
| 谭子悦 | 2023/04/19 | 文档完成 |

[toc]

## 简介

此文档记录了迭代二开发中 CI/CD（持续集成/持续部署）相关信息。

## 部署方案

版本控制平台采用 GitHub，CICD 工具采用 Jenkins，更新方式为 GitHub 通过 Webhook 通知 Jenkins.

```mermaid
sequenceDiagram

User ->> GitHub : pr merged into development
GitHub -->> Jenkins : webhook
Jenkins ->> GitHub : git fetch
Jenkins ->> Jenkins : gradle build
User ->> GitHub : development merged into master
GitHub -->> Jenkins : webhook
Jenkins ->> GitHub : git fetch
Jenkins ->> Jenkins : gradle build
Jenkins ->> Jenkins : gradle release
Jenkins ->> GitHub : gh release
```

_⬆️ 基本流程图_ (Mermaid 绘制)

### 常设分支

版本控制平台上常维护有三条分支：

1. **`development` 分支**

   开发时的主要分支，所有新需求开发都应基于此分支创建新分支，完成开发后再发起 pull request 合并。

2. **`test` 分支**

   测试分支，在 development 分支完成开发后，先合并进 test 分支进行测试部署。

3. **`master` 分支**

   发布分支，在 `test` 分支完成测试后合入此分支。

### 分支操作

Jenkins 会针对不同分支的更新，自动完成不同的 pipeline stage：

| 分支          | Build | Test | Release | Deploy |
| ------------- | ----- | ---- | ------- | ------ |
| `development` | ✅    | ✅   |         |        |
| `test`        | ✅    | ✅   |         | ✅     |
| `master`      | ✅    | ✅   | ✅      | ✅     |

其中包含以下 stages：

- `Build`: 执行 `gradle build`，构建项目并生成 fat jar.
- `Test`: 执行 JUnit 测试。
- `Deploy`: 将生成的 jar 部署到服务器。
- `Release`: 执行 `gradle release`，向 `gradle.properties` 中指定的版本号创建一次 release，附带生成的 jar.

## 成果预览

### Jenkins 账号

- 地址：http://124.223.97.89:8080/
- 账号：supervisor
- 密码：nju19020520

### 截图

![Jenkins 部署项目主页](./assets/image-20230325155042082.png)

![master 分支构建记录](./assets/image-20230325155216264.png)

![最近一次 WebHook 记录（Jenkins）](./assets/image-20230325155847999.png)

![最近一次 WebHook 记录（GitHub）](./assets/image-20230325160002431.png)

![GitHub release 记录](./assets/image-20230325160045655.png)

![image-20230419114735995](./assets/image-20230419114735995.png)
