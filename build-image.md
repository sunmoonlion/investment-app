# Investment Architecture v2 镜像构建与发布

状态：生效中
最后更新：2026-08-09

Investment 只构建三个源码镜像：

| 镜像 | 来源 | 运行方式 |
| --- | --- | --- |
| `investment-backend` | `investment-backend/` | 同一镜像分别启动 API、Worker、Scheduler、Migration |
| `investment-admin-frontend` | `investment-admin-frontend/` | Next.js standalone，管理端表面 |
| `investment-web-frontend` | `investment-web-frontend/` | Next.js standalone，用户端表面 |

旧 `research-web-backend`、独立 `celeryworker-*` 与 `nodebullworker-*` 不属于活动拓扑，禁止继续构建。

## 发布规则

1. 每个子仓先通过自身 lint、typecheck、test、build 或 Backend 质量门禁；
2. 候选镜像使用不可变候选 tag，推送到 `harbor.sunmoonai.com:30443/app-images`；
3. 记录 Registry 返回的 manifest digest；
4. 将三个 digest 写入 K8s 仓库 Investment `release-inputs.json`；
5. 使用 `tpl-app/k8s-deployment` 生成、计划、部署并执行完整门禁；
6. 只有 R7 通过后才能把同一 digest 晋级为正式 `2.0.0`，不得重新构建后再打正式 tag。

Kubernetes 清单必须引用 `repository@sha256:...`，不能把可移动 tag 当作发布锁。具体构建参数以三个子仓的 `mybuild/` 为准；具体迁移和发布阶段以 K8s 仓库 `sunmoonai/docs/investment清理和改名.md` 为准。
