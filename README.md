# investment-app

Investment 是 App Platform 的投资研究与智能体应用。当前 `architecture-v2` 以原
`research-app` 的 Git 历史为迁移主体，执行原地改名和 R3.2 模板同步。

## 活动拓扑

```text
investment-app/
├── investment-backend/          # FastAPI 统一 Backend；API/Worker/Scheduler 多角色
├── investment-admin-frontend/   # Next.js 管理端
└── investment-web-frontend/     # Next.js 用户端
```

| 组件 | 技术栈 | 职责 |
| --- | --- | --- |
| `investment-backend` | FastAPI / Python | Admin、Web、Internal API，以及 Agent Runtime、任务和数据访问 |
| `investment-admin-frontend` | Next.js / React | 内部管理、配置、诊断和治理界面 |
| `investment-web-frontend` | Next.js / React | 投资研究与智能体用户界面 |

Admin 和 Web 是两个独立前端表面，但共同调用同一个 Backend。旧
`research-web-backend` 已从活动 submodule 拓扑移除并保留为只读归档，不得重新作为第二个运行
Backend 引入。

API、Celery Worker、Scheduler 与 Migration 是同一个 `investment-backend` 镜像的不同运行
角色，不是独立源码项目。父仓不得恢复 `celeryworker-*`、`nodebullworker-*`、旧
`k8s-scaffold/` 或四组件 `init.sh`；Architecture v2 部署的唯一模板来源是
`tpl-app/k8s-scaffold-v2`。

## 迁移边界

- 源码身份改为 `investment-*`，但合法的投资研究领域术语可以继续使用 `research`；禁止全局替换。
- 当前 R4 只做隔离环境中的模板同步、应用身份改名和完整门禁。
- 现有 Research 的 K8s 运行态、数据库、凭据、PVC、镜像和 Casdoor Client 是回滚面，R7 前不得删除。
- 真实数据迁移、切读和切写属于 R5。
- 架构与执行边界以 K8s 仓库的 `sunmoonai/docs/investment清理和改名.md` 为准。

## 子模块协作

推送顺序始终是先子仓、后父仓；父仓只记录子仓提交指针：

```bash
git -C investment-backend push origin architecture-v2
git -C investment-backend push gitee architecture-v2
git -C investment-admin-frontend push origin architecture-v2
git -C investment-admin-frontend push gitee architecture-v2
git -C investment-web-frontend push origin architecture-v2
git -C investment-web-frontend push gitee architecture-v2
git push origin architecture-v2
git push gitee architecture-v2
```

GitHub `origin` 是规范远端，Gitee `gitee` 是镜像远端；两者的 `architecture-v2` 必须指向同一
提交。当前所有 `research-*-archive` remote 只用于追溯和回滚，禁止向其发布 Investment 提交。
