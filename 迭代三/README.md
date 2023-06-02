# 迭代三过程文档

## 项目设计、构成与部署

- [设计考虑与 step3 展示.md](设计考虑与step3展示.md)

### 项目构成

GitHub 组织页：[SentiSamoyed](https://github.com/SentiSamoyed)

- [**_SentiStrength_**](https://github.com/SentiSamoyed/SentiStrength)：SentiStrength 的核心部分与后端部分
- [**_SentiStrength-FE_**](https://github.com/SentiSamoyed/SentiStrength-FE)：SentiStrength 的前端部分
- [**_Issue Tracker_**](https://github.com/SentiSamoyed/IssueTracker)：SentiStrength 的 GitHub Issue 获取服务

### 部署

当前 SentiStrength 部署于 [http://124.223.97.89/](http://124.223.97.89/)

Jenkins 部署于 [http://124.223.97.89:1145/](http://124.223.97.89:1145/)

- 账号：supervisor
- 密码：nju19020520

### 数据

在数据获取上，我们通过 GitHub API 获取相关数据，并存储于我们的 MySQL 数据库中。

- **访问者账号**

  此账号只有 `SELECT` 权限，可用于查阅数据或以只读模式运行 SentiStrength 后端（需要修改 `application.yml`）

  - 数据库地址：124.223.97.89

  - 端口：3306

  - 用户名：visitor

  - 密码：sentisamoyed

- **数据库导出数据**：[数据.zip](https://box.nju.edu.cn/f/8e808e8214f6433b9e50/)
- **标注后的数据**：[标注数据](https://box.nju.edu.cn/f/3b9ef58b9f7f42caa545/)
- **前端展示中间数据**：[数据标注下载](https://box.nju.edu.cn/d/67d6999d1ba54d76a56a/)

## 会议记录

- [第一次会议-May.6.md](会议记录/第一次会议-May.6.md)
- [第二次会议-May.10.md](会议记录/第二次会议-May.10.md)
- [第三次会议-May.18.md](会议记录/第三次会议-May.18.md)
- 第四次会议-May.21（记录在[飞书文档](https://sentisamoyed.feishu.cn/docx/K2Psdu1sfoTU3bxWrgvcnZCsn0d)）
- 第五次会议-May.26（步骤三工作确定，未归档）
- [第六次会议-Jun.1-前端标注方案.md](会议记录/第六次会议-Jun.1-前端标注方案.md)

## 任务安排

- [迭代三任务安排.md](迭代三任务安排.md)

## 开发过程文档

- [论文笔记.md](论文笔记/论文笔记.md)
- [需求规格说明文档.md](其他文件/需求规格说明文档.md)
- [接口文档.md](其他文件/接口文档.md)
- [前端设计文档.md](其他文件/前端设计文档.md)
