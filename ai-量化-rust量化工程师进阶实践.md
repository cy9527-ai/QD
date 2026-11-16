# AI&量化_Rust量化工程师进阶实践（技术栈补全版）

> **北极星目标（唯一主线）**：从 0 到 1，培养成拥有多个 GitHub 作品、作品说服力很强的量化开发工程师，拿到优秀 offer。
> 学习主线（按你的定调）：**论文研读 + 开源项目研读复现**为主，每个阶段必须有实际产出推到你的 GitHub。
> GitHub 连接：connector-github 已连通（auth ok）；当前会话未暴露直接推送工具，仓库 push 由你执行，我负责逐阶段验收与脚手架。
> 数据来源：star 数与论文编号为 2026-11-16 实时检索；鲸驰寰宇要求来自用户 JD 截图（一手材料）；未核实处如实标注。

---

## 一、目标锚点：offer 从哪来

| 锚点 | 关键要求 | 证明作品 |
|---|---|---|
| 鲸驰寰宇（一手 JD 截图：30-60K·14薪，深圳/远程，Rust 3 年+） | ①高并发交易框架 ②性能调优（CPU 亲和性/内存对齐/无锁队列）③监控告警/部署/实盘运维；Tokio/async、TCP/UDP、epoll、算法；加分：HFT、FIX/WS/REST、低延迟（零拷贝/内存池）、金融认知、**开源高质量 Rust 贡献者优先** | S2/S3/S4/S6 |
| 非凸科技（2026-11 交叉核实） | Rust 主用；硬性 Linux + 性能分析 + 计算机理论基础；加分竞赛/低时延；要求善用 AI-coding | S1/S3 + 算法线 |
| 腾讯 AI 量化投研（Agent 方向） | 回测/因子/组合改造为 Agent 可调用模块；function calling、RAG、多步推理 + qlib/vnpy + 可解释性 | S5 |

**两条铁律**：①加分项按必选项准备（除在职 HFT 经验外四条全部可后天获得）；②年限不足用作品+PR 置换（JD 加分项⑤是官方给出的置换通道）。

---

## 二、技术栈总表（补全版，全部带链接）

### 2.1 Rust 语言与工具链

| 层 | 选型 | 链接 |
|---|---|---|
| 入门教材 | TRPL（官方书） | https://doc.rust-lang.org/book/ |
| 练习 | Rustlings（64.7k star） | https://github.com/rust-lang/rustlings |
| 进阶书 | 《Rust for Rustaceans》、Rust Atomics and Locks（免费） | https://marabos.nl/atomics/ |
| 工具链 | rustup / cargo / clippy / rustfmt / rust-analyzer | https://rustup.rs ；https://rust-analyzer.github.io/ |
| 并发运行时 | Tokio | https://github.com/tokio-rs/tokio （教程 https://tokio.rs ） |
| 阻塞/线程 | std::thread + mpsc → crossbeam（channel/deque/queue） | https://github.com/crossbeam-rs/crossbeam |
| epoll 封装 | mio | https://github.com/tokio-rs/mio |
| 锁 | parking_lot、lock_api | https://github.com/Amanieu/parking_lot |
| 数据并行 | rayon | https://github.com/rayon-rs/rayon |

### 2.2 性能工程（鲸驰职责②对口）

| 层 | 选型 | 链接 |
|---|---|---|
| 基准 | criterion.rs（5.5k star） | https://github.com/bheisler/criterion.rs |
| 剖析 | flamegraph / perf | https://github.com/flamegraph-rs/flamegraph |
| 零拷贝 | bytes、zerocopy | https://github.com/tokio-rs/bytes ；https://github.com/google/zerocopy |
| 定点数 | rust-decimal（1.3k star） | https://github.com/paupino/rust-decimal |
| CPU 亲和性 | core_affinity | https://docs.rs/core_affinity |
| 内存池 | bumpalo（arena）/ 自实现环形缓冲 | https://github.com/fitzgen/bumpalo |

### 2.3 网络与交易所接口（鲸驰加分项②对口）

| 层 | 选型 | 链接 |
|---|---|---|
| HTTP/REST | reqwest | https://github.com/seanmonstar/reqwest |
| WebSocket | tokio-tungstenite | https://github.com/snapview/tokio-tungstenite |
| FIX 协议 | ferrumfix（455 star） | https://github.com/ferrumfix/ferrumfix |
| 沪深北行情协议 | fin-proto-rs（59 star） | https://github.com/xinchentechnote/fin-proto-rs |
| 交易所 API 文档 | 币安 API + 测试网、OKX API v5 | https://developers.binance.com ；https://www.okx.com/docs-v5/ |
| 连接器参考 | hummingbot connectors 源码 | https://github.com/hummingbot/hummingbot |

### 2.4 数据、序列化与存储

| 层 | 选型 | 链接 |
|---|---|---|
| 序列化 | serde / serde_json | https://github.com/serde-rs/serde |
| 表格数据 | Apache Arrow Rust（arrow-rs） | https://github.com/apache/arrow-rs |
| 嵌入式存储 | redb 或 sled（本地 K 线/订单缓存） | https://github.com/cberner/redb |
| CSV | csv crate | https://github.com/BurntSushi/rust-csv |

### 2.5 可观测性与工程化（鲸驰职责③对口）

| 层 | 选型 | 链接 |
|---|---|---|
| 结构化日志/追踪 | tracing | https://github.com/tokio-rs/tracing |
| 指标+告警 | metrics crate + Prometheus + Grafana | https://github.com/metrics-rs/metrics ；https://prometheus.io ；https://grafana.com |
| 部署 | Docker + GitHub Actions（CI 跑 test/bench/clippy，CD 部署流水线） | https://docs.github.com/actions |
| 测试加固 | proptest（性质测试）、cargo-nextest | https://github.com/proptest-rs/proptest ；https://github.com/nextest-rs/nextest |

### 2.6 量化框架与 Python 侧（研读复现对象）

| 项目 | 用途 | 链接（star 为 2026-11-16 快照） |
|---|---|---|
| barter-rs（2,373，MIT） | 纯 Rust 框架精读复现首选 | https://github.com/barter-rs/barter-rs |
| nautilus_trader（31,570） | 分层架构范本，crates/ 精读 | https://github.com/nautechsystems/nautilus_trader |
| hftbacktest（5,085） | L2/排队位置/延迟建模（约 11 个月无推送，维护未确认） | https://github.com/nkaz001/hftbacktest |
| pyxirr（223） | Rust+pyo3 混合架构参照 | https://github.com/Anexen/pyxirr |
| RustQuant（1,844） | 定价/随机过程视野 | https://github.com/avhz/RustQuant |
| pyo3 + maturin | Python↔Rust 绑定与打包 | https://github.com/PyO3/pyo3 ；https://github.com/PyO3/maturin |
| Qlib（约 50,265，MIT） | 数据→因子→模型→回测工作流 | https://github.com/microsoft/qlib |
| FinRL（17,050） | RL 交易入口 | https://github.com/AI4Finance-Foundation/FinRL |
| vnpy（约 3.1 万，待确认） | 事件引擎设计研读 | https://github.com/vnpy/vnpy |
| backtrader（约 1.8 万，停更未验证） | Python 侧对拍基准（你已有基础） | https://github.com/mementum/backtrader |
| akshare | A 股数据源（对拍用） | https://github.com/akfamily/akshare |
| 目录 | awesome-quant / awesome-rust | https://github.com/wilsonfreitas/awesome-quant ；https://github.com/rust-unofficial/awesome-rust |

（`rust-in-finance` 与 `alruccabetter/rust-financial` 已 404，勿找。）

### 2.7 AI/Agent 栈（交叉作品用）

| 层 | 选型 | 链接 |
|---|---|---|
| Agent 编排 | LangGraph（生态最广、有状态编排） | https://github.com/langchain-ai/langgraph |
| RAG | LlamaIndex | https://github.com/run-llama/llama_index |
| 轻量 Agent | OpenAI Agents SDK | https://github.com/openai/openai-agents-python |
| 工具协议 | Anthropic MCP（交叉胶水） | https://github.com/modelcontextprotocol |
| 方法论 | Building effective agents（2024-12-19，已抓取确认） | https://www.anthropic.com/research/building-effective-agents |
| 展示层 | TypeScript（够用即可） | https://www.typescriptlang.org |

### 2.8 算法与底层（非凸硬要求对口）

| 层 | 选型 | 链接 |
|---|---|---|
| 算法 | LeetCode（NeetCode 150 主干，Rust 题解） | https://leetcode.cn ；https://neetcode.io |
| 系统 | CSAPP 第 6/9/11/12 章（存储/虚拟内存/网络/并发） | 无官方免费电子版，纸质/图书馆 |

---

## 三、六阶段学习方案（每阶段必有 GitHub 产出）

> 学习方式：每阶段 = 论文/书（输入）+ 开源项目研读复现（转换）+ 仓库产出（证据）。验收全过我复核。

### 阶段 S1：Rust 地基 → 产出 2 个仓库

- **输入**：TRPL 全本、Rustlings 全通关、CSAPP 按需查阅。
- **研读复现**：pyxirr——读懂其 Rust 核心与 pyo3 绑定结构，照它的架构重写你已有的 `src/quant/performance.py`。
- **产出①**：`rustlings-notes`（练习记录 + 每章概念笔记，积累半年后可整理成博客）。
- **产出②**：`perf-metrics-rs`——年化/波动率/最大回撤/Sharpe/Sortino/Calmar；numpy/akshare CSI 300 对拍完全一致；criterion 基准；GitHub Actions CI；pyo3+maturin 上 PyPI；README 三分钟讲清。
- **并行线**：LeetCode 每日一题（Rust 题解）。

### 阶段 S2：异步与行情 → 产出 1 个仓库

- **输入**：Tokio tutorial 全部（https://tokio.rs/tokio/tutorial ）；论文 FF 三因子/Carhart/五因子（出处见第五节）各一页摘要。
- **研读复现**：barter-rs——按 instrument → data → 引擎主循环顺序精读，跑通其 backtest，自写双均线策略；hummingbot connectors 读连接器三层抽象。
- **产出③**：`md-aggregator-rs`——同时连币安+OKX WebSocket，统一数据模型，order book 增量重建，断线重连，tracing 监控指标；验收：48 小时稳定运行日志 + order book 重建单测。
- **量化认知同步**：Qlib 完整工作流复现（跑通即可，产出复现报告入 repo `qlib-notes`）。

### 阶段 S3：系统与低延迟 → 产出 1 个仓库（需 Linux：WSL2 或云主机）

- **输入**：《Rust Atomics and Locks》全本；CSAPP 第 6/9/11/12 章；论文 Markowitz 1952 一页摘要。
- **研读复现**：mio 源码示例 + crossbeam 队列源码；nautilus_trader `crates/common`、`core` 精读（产出链路笔记入作品 4 的 `docs/`）。
- **产出④**：`low-latency-lab`——mio 单线程 epoll 行情接收器（UDP/TCP 模拟组播）+ 自实现无锁 SPSC 环形缓冲；验收：与 thread-per-connection 的压测对比数据、false sharing 实验记录，全在 README。

### 阶段 S4：完整交易系统 → 产出 1 个核心仓库（本方案最重作品）

- **输入**：fin-proto-rs 报文结构、ferrumfix FIX 模型；hftbacktest L2 回测与排队位置建模（读+跑通，维护风险已标注）。
- **研读复现**：nautilus_trader 五层分层直接借鉴；hftbacktest 撮合逻辑写笔记。
- **产出⑤**：`quant-system-rs`——五层架构（数据→信号→风控→执行→绩效归因）：风控独立 crate（仓位上限/回撤熔断/频率限制）单测全绿；币安测试网 HMAC 签名下单-撤单-对账全流程；与 backtrader 结果对拍；监控告警+Docker 部署+崩溃恢复；B8 落地（零拷贝/内存池/CPU 亲和性任一项，前后 criterion 对比）；**最后小资金实盘（上限 1 万）**，净值曲线从第一天记录，月度归因报告入 `docs/`。

### 阶段 S5：AI 交叉 → 产出 1 个仓库

- **输入**：RAG（arXiv:2005.11401）、Toolformer（arXiv:2302.04761）、ReAct（arXiv:2210.03629）、Reflexion（arXiv:2303.11366）各一页摘要 +《Building effective agents》。
- **产出⑥**：`mcp-backtest-agent`——MCP 工具接口包住 perf-metrics-rs/quant-system-rs 回测能力：自然语言描述策略→生成回测→执行→绩效报告与归因解释；验收：端到端 demo（录屏或 README 步骤可复现）+ 可解释性设计文档。**最小启动：阶段 S1 结束后即可用 MCP 包双均线提前开工。**

### 阶段 S6：开源贡献与 offer 冲刺 → 外部产出 + 求职整合

- **产出⑦（外部）**：3~5 个被合并 PR——barter-rs 优先（文档→测试→benchmark→适配器，91 open issues）；hftbacktest converter（#276/#288 先例）为备选，**若 PR 超 1 个月无人 review 或仓库停滞，切 barter-rs/nautilus_trader**。
- **产出⑧**：GitHub Profile README（置顶排序：quant-system-rs > md-aggregator-rs > perf-metrics-rs > mcp-backtest-agent）+ 简历终稿（作品与 PR 为主线叙事）+ 面试自测（每条 JD 要求能讲 30 分钟）。
- **算法**：累计 120 题后降频，面试前 2 个月重启。

---

## 四、GitHub 作品集运营（「说服力」的硬标准）

每个仓库五件套缺一不可：**README 三分钟讲清**（问题/架构图/运行方式/性能数字）｜**证据链**（`cargo test` 全绿 + criterion 数据 + 与 numpy/backtrader 对拍）｜**工程完整度**（Actions CI、clippy 零警告、tracing 日志、单测+性质测试）｜**叙事**（设计取舍写进 README/docs：为什么无锁、为什么这层抽象）｜**提交节奏**（持续小步提交而非一次性堆砌——面试官会看 commit 历史）。

---

## 五、论文研读主线（9 篇按序，每篇一页纸摘要）

| 顺序 | 论文 | 出处/链接 | 一句话 |
|---|---|---|---|
| 1 | FF 三因子 | JFE 1993, 33(1): 3–56（DOI 本轮未核实，经期刊页/图书馆获取） | 收益不能只用单一 Beta 解释 |
| 2 | Carhart 四因子 | JF 1997, 52(1): 57–82（DOI 未核实） | 动量因子，行业基本词汇 |
| 3 | FF 五因子 | JFE 2015, 116(1): 1–22；DOI 10.1016/j.jfineco.2014.10.010 | 现代多因子完成形态 |
| 4 | Markowitz 1952 | JF 7(1)（DOI 未核实） | 均值-方差优化起点 |
| 5 | RAG | https://arxiv.org/abs/2005.11401 | 检索增强原始定义 |
| 6 | Toolformer | https://arxiv.org/abs/2302.04761 | 「把回测引擎变成工具」的理论起点 |
| 7 | ReAct | https://arxiv.org/abs/2210.03629 | Agent 推理+行动交替 |
| 8 | Reflexion | https://arxiv.org/abs/2303.11366 | 语言反馈自我改进——自动复盘回测失败 |
| 9 | FinRL 系或 GBDT Alpha 挖掘任一 | https://github.com/AI4Finance-Foundation/FinRL | ML 在量化的两类代表用法 |

读法：1→4 建立市场语言（配 Qlib/backtrader 实操），5→8 建立 Agent 语言（配 S5），第 9 篇收束交叉点。只求「问题/方法/与你作品的连接点」，不精读推导。

---

## 六、执行清单（里程碑驱动，逐项交我复核）

**第 0 步（贯穿全程）：LeetCode 每日一题**

**里程碑一（S1 完）**：①rustlings-notes ②perf-metrics-rs（PyPI+对拍+基准+CI）③论文 1–3 摘要 ④Qlib 复现报告
**里程碑二（S2 完）**：⑤barter-rs 精读笔记+双均线 ⑥md-aggregator-rs（48h 稳定）⑦REST/WS demo 代码并入 ⑧论文 4 摘要
**里程碑三（S3 完）**：⑨low-latency-lab（epoll+无锁缓冲+压测数据）⑩nautilus crates/ 笔记
**里程碑四（S4 完）**：⑪quant-system-rs 风控 crate ⑫测试网全流程 ⑬撮合对拍+hftbacktest 笔记 ⑭实盘启动+净值记录 ⑮性能优化前后对比 ⑯监控部署告警
**里程碑五（S5+S6 完）**：⑰mcp-backtest-agent demo ⑱3~5 个被合并 PR ⑲论文 5–9 摘要 ⑳Profile README+简历终稿+面试自测

**保底压缩序列**（投入受限只保这条线）：第 0 步 → S1 → S2 的 ⑤⑥ → S3 的 ⑨ → S4 的 ⑪⑫ → S6 的 ⑱。

### 检查点与应急

| 机制 | 内容 |
|---|---|
| 检查点①（里程碑一后） | Rustlings 全绿；perf-metrics-rs 五件套齐；LeetCode ≥55 题。不达标先补短板不跳关 |
| 检查点②（里程碑三后） | 能徒手讲清 order book 重建与 epoll 原理；压测数据在 README |
| 检查点③（里程碑四后） | 测试网全流程通过；实盘已启动有净值记录。不达标实盘推迟 |
| 触发式应急 | 回撤>20% 停实盘归因；PR 无人 review 换目标仓库；产出停滞回保底序列（砍博客与扩展，作品与算法不动） |
| 风险底线 | 实盘资金上限 1 万；任何「入职先出资/先交钱」信号立即退出 |

---

## 附：数据来源与检索边界

- 鲸驰寰宇 JD：用户提供的招聘截图（一手材料）；此前「未检索到其公开 Rust 岗」已被截图推翻并更正。
- star 数为 2026-11-16 快照；hftbacktest（约 11 个月无推送）、vnpy（2025-07 第三方清单）、backtrader（长期停更，未验证）维护状态已逐项标注。
- 非凸/腾讯 JD 来自招聘页面交叉检索，投递前以官网最新版为准；FF 1993/Carhart 1997/Markowitz 1952 DOI 本轮未核实，已标注获取途径。