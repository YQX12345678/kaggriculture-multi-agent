# Experiment Log

## Head-to-head

| 对手 notebook | 作者 | 公开分数 | v9/4 胜-负 | 平均分差 |
|---|---|---:|---:|---:|
| Demand-Preserving Turn Sale Timing | tetsutani | 2750.2 | 55-5 | 3446 |
| First in Line: Stock Into Income | Alperen Aydın | 2746.0 | 54-6 | 3196 |
| V47 Reactive Market Coordination | Ahmed Berat Özer | 2686.0 | 55-5 | 3698 |
| V48 Clear the Queue | Ahmed Berat Özer | 2670.4 | 55-5 | 3534 |
| V38 Smarter Feed, Stronger Margins | Ahmed Berat Özer | 2625.2 | 60-0 | 7379 |
| V39 Ready Before the Rush | Ahmed Berat Özer | 2621.2 | 60-0 | 7198 |
| v34 Observed Market Timing | Ahmed Berat Özer | 2601.6 | 60-0 | 10801 |
| V41 Review Candidate | Ahmed Berat Özer | 2586.4 | 60-0 | 7188 |
| v31 Production and Sale Priority | Ahmed Berat Özer | 2575.6 | 60-0 | 10929 |

总体：519-21（96.1%），270 fresh seeds × both seats；官方引擎 80-0。

## 消融/单步实验（摘要）

- 销售预留 horizon 40 / margin 12：对 6/4 版本 73-7；对 32/12 版本 74-6。
- 预留窗口从 step 288 提前到 192：三组镜像 32-0、30-2、30-2。
- RACEPX glut gate：镜像 35-13；对 6/4 祖先 41-7。
- 终局物理闭包：最后七回合仅接受正物理交付、零溢出、非支配改进。
- 失败安全：单成员失败降权；权重缺失保留 0.5 基准；时间预算耗尽已完成成员出分。

## 未解决问题

- Fracture / Contusion 样本极少，Macro AUC/收益方差大。
- 更深销售预留（44/12、48/12）并不稳定优于 40/12。
