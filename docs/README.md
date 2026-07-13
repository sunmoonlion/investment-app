# research-app 文档入口

状态：当前有效

本目录是 research-app 根仓唯一的工具无关文档入口。当前 LangGraph 平台架构、任务顺序和 Gate 以 `k8s` 仓库的 MoocManus v5 总体方案、实施计划、ADR、contracts 和 evidence 为准。

## 本仓真相源

1. Research 后端 Graph/Runtime、路由/OpenAPI、数据库 migration、状态模型和自动化测试。
2. Research Web/Admin 的实际路由、typed client、stream adapter 测试和部署配置。
3. k8s 中的 Research desired state、镜像 digest、迁移/回滚证据。
4. Git 历史只用于审计，不代表当前 Runtime、SSE、身份或前端方案。

旧 v4 事件模型、旧 Walking Skeleton、早期 Vue/Next 前端计划和按 AI 工具划分的交接文档均不得覆盖 v5。当前工作必须继续遵守 traffic-off、真实契约和 Gate 纪律。
