# investment-app — AI 协作上下文

本文件只提供仓库级入口，不维护独立于其他工具的平行项目事实。

## 开始任务前

1. 阅读根 `README.md`；
2. 阅读 K8s 仓库的 `sunmoonai/docs/investment清理和改名.md`；
3. 核对目标子仓、Graph/Runtime、OpenAPI、migration、测试和 Git 状态；
4. 只执行当前已激活的 Architecture v2 阶段。

## 工作边界

- Investment 拥有 Session/Thread/Run/Attempt/Invocation、Graph/Runtime 和 Agent 产品状态，
  不接管 Info/Knowledge 领域事实；
- `investment-backend` 是 Admin、Web 和 Internal 的统一 FastAPI Backend；
- Admin/Web 是两个 Next.js 表面，不得重新引入活动的第二个 Web Backend；
- 合法领域概念可保留 `research`，应用和基础设施身份必须逐项迁为 `investment-*`；
- 现有 Research 运行态是回滚面，R7 前禁止删除；
- 不得用 fake SSE、fake citation、mock retrieval 或 hardcode graph 作为验收；
- 不输出或提交 token、cookie、client secret、signed URL 或真实凭据。

## 文档规则

状态只写入任务指定的权威计划、ADR、contract、evidence 或代码相邻的必要文档，不创建按 AI
工具命名的平行文档树。
