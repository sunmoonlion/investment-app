# investment-app — AI 协作上下文

本文件只提供仓库级入口，不维护独立于其他 AI 工具的项目事实。

## 开始任务前

1. 阅读根 `README.md`，并核对任务明确指定的权威资料。
2. 核对目标子仓代码、README、依赖锁、测试和当前 Git 状态。
3. 涉及跨仓契约、模板同步或集群部署时，以实际代码、版本化契约和 k8s desired state 为准。

## 工作边界

- Investment 领域能力进入对应子仓；可复用基础能力先在 tpl-app 建设和验证，再按明确任务同步。
- 接口事实来自代码、OpenAPI/schema 和 contract tests，不维护手写的第二份权威契约。
- 未来业务规划尚未冻结时，不把占位模板、旧交接或历史路线图当作当前承诺。
- 不输出或提交 token、cookie、client secret、signed URL、真实凭据或完整敏感响应。
- 安装、网络构建和 Git push 由项目负责人执行；本地提交和验证必须可追溯。

## 文档规则

项目状态只写入任务明确指定的权威计划、ADR、contract、evidence 或代码相邻的必要文档。不要创建任何按 AI 工具命名的平行文档树。
