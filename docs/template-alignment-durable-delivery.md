# Investment 模板对齐：可靠投递开发候选

## 2026-09-13 暂停集成

所有者改为暂停并同步现有成果，本次父仓固定后端 `68f776edf6f8155f4e5ebfc4e321a17da229dc95`。
后续 B7u 固定完整回归 402 passed / 0 skipped；累计证据与未完项见 k8s
`sunmoonai/docs/v5-backlog-disposition-luna.md` 和 `v5-backlog-joint-runtime-identity-luna.md`。
下文“本地/尚未推送”保留为各包当时历史；源码同步不是正式镜像发布或业务身份切换。

## 2026-09-13 B7j 回执进展（本地，未发布）

模板最终 `tpl-backend@a91eb3e284ae91d4bc6b82fe567c4163cfa728f0` 全量 255 项，
Info 500 项、Knowledge 415 项修订后依次通过，再复验 Investment 最终提交
`investment-backend@3d9531d1250d035aa13eb197198b6c5672450856`：
**399 passed / 0 skipped，79.13 秒**，Ruff/Pyright 通过。
六个公共文件与模板一致；既有 Agent 观测测试另补七条回执字段断言及一项归档保护
测试，保留实际 agent.executor consumer 和 notification 无回执语义，不修改领域生产代码。

首轮 `c90f522c620e9bedb09728e609b773aafad91c28` 在 167 passed 后新 gauge 下降测试
失败：DELETE Outbox 经 CASCADE 触发旧 Agent 归档的语句级只读保护，即使旧表为空
也拒绝。未禁用保护或改迁移；公共测试从模板重新修正为移除隔离合成回执，再按固定
顺序完整复验。新增领域回归确认上述保护仍生效、失败后原 Outbox 数据保留。
这不是批准/实现归档清理；后续保留策略须另处置旧归档引用和回滚窗。

差异分类：AgentDelivery/租约/领域 handler 原样保留；无配置新增差异、临时兼容或
公共增量违规漂移，领域测试是显式扩展，不宣称全仓相同。
真实共用 prefork/PG/Redis/契约场景通过；回执不是业务成功量、per-worker 健康或
真实 Provider/部署验收。监控仍未来 N4-OPS-01，本轮无 Secret/迁移/镜像/部署变更。
六文件摘要、失败根因和门禁见 k8s `sunmoonai/docs/v5-backlog-worker-progress-luna.md`；
父仓 gitlink 不暂存、master 不改、不推送，等待最终统一集成。

## 2026-09-13 B7i 本地增量（尚未发布）

模板固定 `tpl-backend@ed157e41f11e5e20e6b77812890cb55d382b58f4` 全量 243 项，
Info 488 项、Knowledge 403 项逐仓通过后，才同步本仓。Investment 固定
`investment-backend@6a5bff975649a548079e5eb82ee2b7cdb0872981` 的 Ruff/Pyright
通过，完整 **386 passed / 0 skipped，68.66 秒**。
五个新增 Scheduler 活动/CLI/测试/说明文件逐字同步，bootstrap 只加观察类选择。
差异分类：AgentDelivery、Pilot、租约、领域任务及调度清单保留；配置无新增差异，
使用原 schedule 路径；无临时兼容层或公共增量违规漂移，不宣称全仓相同。

真实本仓 Beat 发布及暂停/恢复/重启、既有真实 PG/Redis 故障与契约回归通过。
观察的是 Linux 本机循环和发送调用，不当作 Agent/Worker 业务完成或实际部署验收；
无镜像/部署/迁移/身份修改。监控安装/采集/告警送达由未来 N4-OPS-01 接收，未实施。
本地提交与证据见 k8s `sunmoonai/docs/v5-backlog-scheduler-activity-luna.md`；
父仓 gitlink 不暂存、不推送，master 和云端留待最终统一集成。

## 2026-09-13 B7h 本地增量（尚未发布）

模板 `c66654a591b186ac814cadb907defc421e94aba6` → Investment
`3b6c215fd80cc66057ea82bb762fd02fc42da30b`，等 Knowledge 完整门禁通过后实施。
新增 `GET /api/internal/v1/delivery/metrics`，签名服务身份与 `delivery:observe`
隔离浏览器身份；使用既有只读 collector/API 池，进程单次准入、失败无假零/旧值。
公共 endpoint、24 项 HTTP 测试、观测说明三文件 SHA-256 与模板相同；路由和响应头
仅同一增量。AgentDelivery 的真实 consumer/租约及 notification 语义、Agent/Pilot
路由完全保留，没有用模板空 handler 覆盖领域 observer。

差异分类：领域扩展保留；Investment 身份/audience 配置保留且无默认授权；没有新增
兼容层；本包公共三文件无违规漂移。前端、迁移、部署与依赖未变。首轮 Ruff/Pyright
通过，完整回归 342 passed / 0 skipped（55.48 秒），固定提交复验回执见 k8s
`sunmoonai/docs/v5-backlog-metrics-http-luna.md`；本节不宣称重新完成全量模板比较。
父仓 gitlink、master、远端/云端均保持原位，最后统一集成；非业务部署或真实告警验收。

同轮 Info 复验发现的恢复期预算泄漏已由模板确定性复现并修正，逐仓过门禁后同步
到 Investment；只追加两份同模板的测试范围修正，正式 2 秒预算及运行代码不变。
最终本地检查点 `681256f5c39941cfc7573b44a2e3702f0f7eaeb1`，固定提交
Ruff/Pyright 通过，343 passed / 0 skipped（56.40 秒）；342 项为首轮历史。

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

## 2026-09-13 B7a：公共日志增量对齐

本节不改写以上 2026-09-11 历史证据。模板固定 `tpl-backend@553c36b`，
Investment 固定 `investment-backend@9622af0`；日志策略、Postgres 包装器、专项测试和
说明逐字相同。Worker 只同步信号注册，保留 Agent/Pilot 任务及两个对账调度条目，
此差异属领域扩展。无新增配置差异、临时兼容或违规漂移；不重新宣称全仓对齐。

模板 → Info → Knowledge 均完成固定提交门禁后才同步 Investment。
静态检查通过，固定提交全量 **223 passed / 0 skipped**（22.93 秒），真实一次性
PG/Redis 与共享契约向量；新增 8 项日志测试。没有调用真实 LLM 或金融数据。
不改 Agent 状态、租约、投递、前端、迁移或服务契约；没有 KIND、真实身份或发布回滚
验收。源码日志降噪不等于完整脱敏、告警/指标或运行态验收。

## 2026-09-13 B7b：API schema readiness 增量对齐

模板 `tpl-backend@ed8d5dc`、Info、Knowledge 固定提交依次过门禁后才同步本仓。
Investment 固定 `investment-backend@85f8cb7` 完整 **242 passed / 0 skipped**（26.87 秒），
Ruff/Pyright 通过。新增 19 项真实隔离 PG 的迁移/降级/再升级、SELECT 权限、
锁等待超时及恢复测试；旧 Agent/Redis/契约回归保留，没有调用真实 LLM 或金融数据。

共 4 文件：schema_readiness、测试、说明逐字同步，API 只加入相同探测增量。
领域路由/身份与 Agent 执行保留，期望 revision 取本仓迁移链，无新增影子配置、
临时兼容或违规漂移。本次增量对齐不等于全仓或全部角色验收。
没有改迁移/前端/契约/部署；业务 API principal、KIND、真实身份和联合发布/回滚未验收。
严格 revision 不匹配会拒绝 ready，不能以旧镜像直连新库作为默认回滚。

## 2026-09-13 B7d：只读投递观测增量对齐

模板 `tpl-backend@1f8941f`、Info@9ea1c5e、Knowledge@d16fb6c 固定提交依次过门禁后
接入本仓。Investment 固定 `investment-backend@7113e52` 全量 **269 passed / 0 skipped**
（30.52 秒），Ruff/Pyright 通过；真实隔离 PG/Redis 与共享契约，没有调用金融数据或 LLM。

6 个新文件：CLI、聚合器、公共 24 项测试、说明四文件与模板逐字一致；observer 工厂增加
实际 AgentDelivery，此差异属领域扩展，另有 3 项 Agent 观测测试。不复制 topic/consumer/
lease 策略，不修改 Agent 执行/重放/对账或公共 handler。新增工厂确保空通用 registry 不会
漏掉 Agent；缺领域租约表失败而非降级为零，notification 发布完成不要求 agent.executor 回执。
本增量无配置差异、临时兼容或违规漂移，不以此重新声明全仓对齐。

未建立受保护 scrape/告警/角色活性探针，不修改 API/前端/迁移/契约/部署，也不宣称
业务 principal、KIND、真实身份或发布回滚验收。只读 gauge 不等于全套 Agent 产品指标。

## 2026-09-13 B7e：Worker 消费配置检查增量

模板 `5369862` → Info `7755da2` → Knowledge `7b11608` 依次通过原始完整门禁后接入。
Investment 固定 `investment-backend@d231266` 完整 **305 passed / 0 skipped**
（50.76 秒），Ruff/Pyright 通过。新增 CLI、35 单元、1 真实 RabbitMQ/本仓 prefork
Worker 场景及说明，四文件逐字同步；旧观测锁超时测试同步局部故障作用域修正。
公共五文件与模板一致，原 Agent 专项观测与真实领域任务注册保留，CLI 从本镜像注册表
取得全部 app.tasks 任务，不另建领域清单。不调用金融数据、真实 Provider 或模型。

领域 overlay 原样保留；无新增配置差异、临时兼容或违规漂移，仅本包增量对齐。
未改历史 release/bundle、业务数据/Secret/迁移/前端/DTO；下次新镜像发布才接实例探针。
不把控制面队列/注册检查当实际消费进展、Scheduler 活性或真实身份/KIND/回滚验收。


## 2026-09-13 B7f：显式投递状态与时钟回退

模板本地固定 `tpl-backend@1c5173b` 先过 176 项完整门禁，再串行 Info→Knowledge→Investment。
本仓本地固定 `investment-backend@24a7512` 全量 **318 passed / 0 skipped**，Ruff/Pyright 通过。
公共四生产文件、9 项故障回归及说明六文件与模板 SHA-256 一致。
新增四项领域租约回归；AgentDelivery 的释放/完成分支及 Pilot 取消同步明确失效状态，保留独立 session 租约、取消 epoch 递增和权限检查。
没有新增配置差异、临时兼容或违规漂移；这是增量对齐，不重新声称全仓相同。

释放使用负无穷而不删除 epoch 行，立即入队/重放/对账不添加墙钟门槛；真正预约与退避保留。
原失败断言未改，先在旧代码确定性复现再验证修复；详细记录在 k8s 的
v5-backlog-clock-regression-luna.md。没有改系统校时、迁移/前端/契约/Secret/镜像或业务部署。
本轮按所有者要求只保存本地 Luna 候选，父仓 gitlink 暂未更新，未合并 master 或推送同步；
待剩余处置完成后统一集成。真实身份/KIND/发布回滚与运行监控不因本次通过而自动销账。
