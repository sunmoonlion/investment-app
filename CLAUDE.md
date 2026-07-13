# research-app — AI 协作上下文

本文件只提供仓库级入口，不维护独立于其他 AI 工具的项目事实。

## 开始任务前

1. 阅读 `docs/README.md`。
2. 核对目标子仓代码、README、Graph/Runtime、OpenAPI/migration、测试和当前 Git 状态。
3. MoocManus 的架构、任务和 Gate 只以 k8s 仓库的 v5 总体方案、实施计划、ADR、contracts 和 evidence 为准。

## 工作边界

- Research 拥有 Session/Thread/Run/Attempt/Invocation、Graph/Runtime 和 Agent 产品状态，不接管 Info/Knowledge 领域事实。
- Walking Skeleton、旧事件模型和历史 frontend plan 不是生产基线；`AGENT_V4_TRAFFIC_ENABLED` 在授权前保持关闭。
- 任何时刻只推进实施计划中一个已激活任务；不得以 fake SSE、fake citation、mock retrieval 或 hardcode graph 验收。
- 不输出或提交 token、cookie、client secret、signed URL、真实凭据或完整敏感响应。
- 安装、网络构建和 Git push 由项目负责人执行；本地提交和验证必须可追溯。

## 文档规则

项目状态只写入中性 `docs/` 或 k8s 权威文档。不要创建任何按 AI 工具命名的平行文档树。
