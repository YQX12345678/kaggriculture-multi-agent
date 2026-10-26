# Kaggriculture Multi-Agent Strategy — The 2945 Farm

**两农场 30 天 / 720 回合竞争模拟：录制路线回放 + 反应式安全层 + 对手建模 + 市场竞价。**

## 1. 竞赛背景

Kaggriculture 是双农场回合制模拟。每天 24 回合、30 天共 720 步，两个农场通过种植、养殖、雇佣、市场买卖竞争最终净收益。Agent 每步输出 farmer / hands / market 三类动作，目标是最大化最终资金。

## 2. 方案概览

核心文件是 `src/main.py`：一个只依赖 Python 标准库的竞赛 agent（从 notebook 中的 `%%writefile main.py` 单元提取，共 5760 行）。整体架构：

- **录制路线回放**：预计算 action tape，按当前局面路由。
- **反应式安全层**：hand_align、weed_repair、sell_lead、budget_guard、room_guard、clamp_sells、dead_stock、terminal_liquidation。
- **市场层**：RACE 销售预留、RACEPX glut gate、COURIER 当日送达、CARROT 作物替换、HERD 畜种选择、OPENING 开局交易。
- **对手/市场预测**：从公开市场库存变化恢复对手销售，按售卖流库预测并提前卖出。
- **终局**：最后七回合物理闭包规划与失败安全。

## 3. 技术亮点

- 只依赖标准库的竞赛提交文件，运行约 3 ms/回合。
- 路线 tape + 反应层：把强路线与局部安全/市场规则解耦。
- 精确销售时序：按对手销售流和 town draw 推断提前量，减少价格冲击。
- 终局物理闭包：在 step 712–718 模拟自身动作、库存与市场，拒绝非支配改进。
- 完整 notebook：官方引擎对局、money ledger、全赛季 GIF、H2H 与消融。

## 4. 关键结果

| 项目 | 结果 |
|---|---|
| Live ladder | 2944.7（submission 56269928） |
| 对 10 个最高公开 notebook agent | 519–21（96.1%），270 fresh seeds × both seats |
| 对 17 个 reactive bots | 645/680（94.9%） |
| 最佳公开 notebook 分数 | 2750.2 |

## 5. 文件结构

    src/main.py                        完整竞赛 agent（标准库）
    src/__init__.py
    notebooks/kaggriculture-agent.ipynb 原始 notebook：对局、ledger、GIF、H2H、消融
    configs/default.yaml               运行参数占位
    docs/experiment_log.md             实验与消融记录
    requirements.txt
    LICENSE
    .gitignore

## 6. 复现

    pip install -r requirements.txt
    python -m py_compile src/main.py
    # 打开 notebooks/kaggriculture-agent.ipynb 运行官方引擎对局与 GIF

数据需从 Kaggle 竞赛页面获取；仓库不包含竞赛数据和大权重。

## 7. 提交

将 `src/main.py` 作为 Kaggle submission 的 `main.py`；notebook 中也有完整写入、SHA256 校验和对局流程。

## 8. 我的贡献

（请按实际情况微调）

- 独立整理并模块化 The 2945 Farm agent，将 notebook 中的单文件提交代码提取为 `src/main.py`。
- 参与/实现销售时序、市场路由、终局物理闭包等层的调优与验证。
- 搭建可复现的 notebook 实验、H2H 统计和消融记录。
