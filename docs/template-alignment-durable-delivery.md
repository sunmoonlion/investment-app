# Investment 模板对齐：可靠投递开发候选

日期：2026-09-11。模板、Info、Knowledge 依次验证后接入；保留上一轮
Agent 可靠性提交 `5e9898e`。本文是开发证据，不是正式发布、真实模型或业务交易验收。

## 全量源码比较

三个子仓全部 Git 可见文件逐路径计算 SHA-256，仅自动归一 tpl/Tpl/TPL；
未使用模板覆盖领域扩展。清单为接手目录 `investment-source-alignment.json`，
可复跑 `audit-source-alignment.py investment`。最终干净 commit/tree 由父仓
`development-source-lock.json` 固定，不能只把工作区 HEAD 当候选全部内容。

| 组件 | 完全一致 | 身份归一后相同 | 其它同路径差异 | Investment 独有 | 模板独有 |
| --- | --- | --- | --- | --- | --- |
| Backend | 109 | 8 | 39 | 135 | 3 |
| Admin Frontend | 100 | 9 | 16 | 2 | 0 |
| Web Frontend | 74 | 9 | 18 | 1 | 0 |

公共 8 文件逐字同模板：durable_tasks、messaging/durable_delivery、delivery_schema、
repositories/outbox、tasks/durable_delivery、cli/durable_delivery、delivery_runtime_probe、
test_durable_delivery_db。默认 handler 注册为空，Agent 经 DurableDelivery 的 topic/consumer
映射和 active_execution_sql 扩展；公共 pump 类型标注先在模板放宽到已有策略基类，
再按 Info 128、Knowledge 145 完整回归顺序同步，没有改变模板运行逻辑。

## 差异分类与处置

| 类别 | 路径组与结论 |
| --- | --- |
| 领域扩展 | application/agent、domain/agent、infrastructure/agent 与 graph、Knowledge/LLM client、Pilot 服务身份和路由、对应测试、ADR、golden/spike 资产；保留原 run/事件/副作用/取消/会话租约/Port，不把领域写入模板。 |
| 领域扩展 | AgentDelivery 只保留会话执行与过期副作用对账；领取/发布完成/重放/死信方法就是模板方法，Agent pump 委托公共循环，只适配 Celery 与 Redis。旧直接 producer 方法已删除。 |
| 领域扩展 | Web create/cancel DTO、Port、路由和 reference adapter，前端 research-workspace、runtime 面板、交互 client/cancel hook、契约测试。保留已有实例 overlay；当前默认 Web adapter 仍拒绝，不能宣称生产已接 Agent。 |
| 领域扩展 | 七条本 App 线性迁移，新增公共死信迁移调用模板 DDL；Agent 会话租约不是第二份投递租约。旧死信只读档案不再是真源，降级携带新增/重放回执。 |
| 配置 | App 名称、标题、身份 enum 增补 investment、cookie/auth 参数名、服务身份/scope、config/env、库/角色/桶/索引、LangGraph/psycopg 依赖及 lock；保留认证/授权/日志/审计公共骨架。 |
| 配置 | Admin 品牌/layout/navigation，Web dashboard/public-home 与翻译、Playwright 显式后端路径及禁复用 server；都属既有研究实例 UI，不清空替换。 |
| 暂时兼容 | 旧 graph 任务拒绝执行但保留注册与测试辅助；LeaseLost 是公共异常兼容导出；Agent task 清理自己 PG/Redis 池以与通用任务共存。 |
| 暂时兼容 | UUID Python/DB 双侧默认、固定虚拟 tpl audience、原 E501/B008/UP046 lint 例外、脚本中既有格式差异。未以公共同步为由重排 6 个非本轮 scripts 文件。 |
| 暂时兼容 | Redis 额外 ACL SAVE、前端 TPL_SSR_* 模板接口；删除未消费的 ADMIN_FRONTEND/WEB_FRONTEND 影子配置。未验证 ACL SAVE 重启持久化或修复既有 Redis CLI 服务端错误传播。 |
| 违规漂移（已修正） | Redis 缺 resetchannels；Backend rebuild 使用正式标签；前端沿用历史候选 tag 并默认自动推送。同步模板/Info 已验证保护、开发 tag、默认不推送及当前说明。 |
| 接入缺陷（实测修正） | Agent/通用任务交替运行留下跨循环 PG 池；Agent 任务边界成功/失败都清理资源。随后新进程先导入公共 task 暴露循环依赖；先补失败测试，再延迟导入共享 pump。两轮失败现场保留。 |
| 验证工具缺陷（修正） | Calico 脚本仍给目标贴 knowledge-r5，与当前 Investment 策略的 knowledge 不匹配；只修测试目标标签，未放宽部署策略。 |

## 最终开发证据

- 后端原始完整 173 passed；当前完整 **198 passed，无跳过**。含原 Agent DB 16 项、
  公共 DB 13 项、新共享迁移/新进程恢复 6 项、新 Celery 边界/导入顺序 6 项以及共享契约。
  Ruff、app/core 格式、Pyright 通过；镜像同样执行这些静态门禁。
- Admin 44 单元 +10 配对；Web 49 单元（含共享向量）+7 配对，两端完整 check/build。
  真实 Casdoor 两面匿名401/登录200/跨面401/CSRF403/退出204/撤销401；TLS开启，
  回调转交候选进程内 ASGI，DB/Redis独立，不是完整部署态领域 UI 验收。
- 最终镜像 `luna-investment-delivery:20260911-verified`，清单
  `sha256:1c085f92cd5a339e1d50bcf8c0520fcba685f5761ce65388eecec467424dde75`。
  全新专用库与队列，真实 KIND Worker/Beat/RabbitMQ 公共重复投递通过；继而实际
  Agent/Graph/PostgreSQL checkpoint/独立 Redis 通知通过：completed、Agent Inbox=1、
  本地 effect=1、events=10、checkpoints=4、unpublished=0，重复投递完全不改变快照。
  没有调用真实 LLM、远程业务副作用或执行金融交易。
- 新进程持有 Agent 租约后被测试 SIGKILL，旧 epoch 过期，新执行者 epoch=2 完成，
  Inbox=1；这是隔离测试，不是生产故障演练。
- 备份实际恢复新库，**19 张表**逐表行数与完整行内容指纹一致，包含 Agent run/事件/
  checkpoint、共享投递、非空模拟重放死信和本地副作用。恢复后的旧档案写入仍拒绝；
  非空旧死信、新增死信和重放时间的 downgrade/re-upgrade 另外由真实 DB 测试覆盖。
- Calico v3.28.2 修正探针后完整通过：内部/前端到 Backend 放行、无标签拒绝，
  仅 Worker 可到 Knowledge，API/Scheduler 拒绝。两轮临时集群已删，诊断保留。
- 三个组件正式标签保护、隔离 Redis 本地/生成 k8s 命令频道收敛通过；没有推正式镜像。

当前默认 Web 尚未接 Agent、预算与完整 Profile 执行等既有未接线项未在本轮扩张。
历史发布清单与部署 bundle 未改写；开发源码锁 `formal_release=false` 不代替正式
源码/镜像/部署/数据联合发布锁。最终 master/worktree 同步另行核验，不由本报告推定。
