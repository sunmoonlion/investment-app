# Research 历史资料边界

状态：只读历史说明
最后更新：2026-08-09

本目录中名称仍含 `Research`、`P0-009` 或旧四组件拓扑的材料，仅用于说明
`research-app` 到 `investment-app` 的来源、恢复和迁移证据，不是当前运行手册。

当前有效事实只有：

- 活动源码拓扑为 `investment-backend`、`investment-admin-frontend`、
  `investment-web-frontend` 三个子模块；
- API、Worker、Scheduler、Migration 是统一 Backend 的运行角色；
- 当前部署模板来源为 `tpl-app/k8s-deployment`；
- R7.1 已关闭回滚观察窗并退役 Research K8s 运行态；
- R7.1 退役回执已退出当前工作树，按 K8s 仓库
  `sunmoonai/docs/legacy-backlog/verification-index.md` 的固定 Git 版本查询；
  当前迁移、回滚与数据保护以前述目录中的 `deployment-checklist.md` 为入口。

不得从历史文档复制旧 `research-admin-backend`、`research-web-backend`、独立 Worker
源码项目或 v1 K8s 脚手架重新进入活动架构。
