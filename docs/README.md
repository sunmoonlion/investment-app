# investment-app 文档入口

状态：当前有效

本目录是 investment-app 根仓唯一的工具无关文档入口。项目事实不得按 Claude、Cursor、Codex 或其他 AI 工具分别复制。

## 权威顺序

1. Investment 各子仓的代码、依赖锁、路由/OpenAPI、数据库 migration、测试和构建配置。
2. 根仓及子仓当前 README、部署配置和自动化验证结果。
3. k8s 仓库中的 desired state，以及未来经评审生效的计划、ADR 和版本化跨仓契约。
4. Git 历史仅用于审计，不代表当前产品范围或运行状态。

## 维护规则

- Investment 业务规则进入对应业务子仓；通用能力优先回到 tpl-app 建设和验证。
- 接口与跨仓契约必须拥有单一真相源，并由 provider/consumer tests 验证。
- 当前任务、状态、决策和证据写入明确的权威文档或任务系统，不创建按 AI 工具命名的平行文档树。
- 文档与代码冲突时先核验代码和运行证据，再修正文档。
