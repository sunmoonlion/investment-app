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
`k8s-scaffold/` 或四组件 `init.sh`；正式部署的唯一模板来源是
`tpl-app/k8s-deployment`。

## 已完成的迁移边界

- 源码身份改为 `investment-*`，但合法的投资研究领域术语可以继续使用 `research`；禁止全局替换。
- R4 已完成隔离模板同步和应用身份改名；R5 已完成真实数据迁移与切换；R7 已发布 `2.0.0`。
- R7.1 观察窗关闭后，旧 Research Kubernetes 运行面已按白名单退役；历史数据和迁移证据仍保留。
- 当前架构与退役边界以 K8s 仓库 `sunmoonai/docs/architecture-v2/` 为准。

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
提交。两个远端的后端仓库均使用规范名称 `investment-backend`，本地 remote 不得再指向
`investment-admin-backend`。旧 Research 仓库不配置为本地发布 remote；历史追溯使用 tag 和
Git 历史。
