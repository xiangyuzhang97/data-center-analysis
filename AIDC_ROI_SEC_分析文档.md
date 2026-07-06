# AIDC / 数据中心 ROI 分析框架：核心驱动变量 X 与收益 Y 的关系

日期：2026-07-06  
研究目标：识别驱动数据中心建设的核心变量 X，并建立其与收益 Y，尤其是 NPV / IRR / UFCF 之间的可量化联系。  
数据口径：优先使用 SEC filings 中披露的收入、资本开支、固定资产、租赁、债务、客户合同和采购承诺，辅以项目级运营假设。

---

## 1. 核心结论

数据中心 ROI 的本质不是单一的“建成多少 MW”，而是资本投入、上线速度、可销售算力/机柜容量、客户合约和融资成本之间的动态匹配。对 AI 数据中心而言，最关键的收益变量 Y 可以拆成：

```text
Y = NPV = Σ UFCF_t / (1 + WACC)^t - Initial Capex
UFCF_t = Revenue_t - Cash Opex_t - Maintenance Capex_t - Tax_t - Working Capital_t
```

由此，真正影响 NPV 的核心 X 不是一个变量，而是一组相互传导的变量：

```text
Power / Land / Equipment / GPU / Network / Cooling / Financing / Customer Contract
→ Facility MW / IT MW / GPU Capacity / Time-to-Live / Utilization / PUE
→ Revenue / EBITDA / UFCF
→ NPV / IRR / Payback Period
```

目前 SEC 数据已经可以支持三类关键判断：

1. **AI 数据中心建设高度资本密集**：CoreWeave、IREN、Nebius 的 PPE 和 capex 扩张远快于传统云业务披露口径。
2. **收益端越来越依赖大客户长约**：NVIDIA、Microsoft、OpenAI、Meta 等客户或战略投资方的合同，成为项目收入确定性的核心证据。
3. **利率和融资结构会显著改变项目 NPV**：高债务、高租赁、高前置 capex 的模式，使 WACC 和利息成本成为宏观层面的核心 X。

---

## 2. 分析对象与逻辑链

本研究应分为两个层面：

### 微观层面：单个数据中心 / AI compute 项目的 ROI

微观层面关注一个项目从建设到变现的路径。变量链如下：

| 层级 | 核心变量 | 财务影响 |
|---|---|---|
| 资源输入 | 土地、电力接入、变电站、电力设备、冷却、网络、GPU | 决定初始 capex 和建设瓶颈 |
| 建设过程 | Capex/MW、设备交期、施工周期、time-to-power | 决定现金流前置压力和收入启动时间 |
| 运营能力 | IT MW、rack density、PUE、availability、utilization | 决定可销售容量和单位成本 |
| 商业化 | $/GPU-hour、$/kW-month、合同期限、客户信用 | 决定 revenue visibility 和收入质量 |
| 财务结果 | EBITDA、UFCF、NPV、IRR、payback period | 最终 ROI 输出 |

关键点是避免重复计算。例如，若同一批 IT MW 已被用于自营 AI cloud 收入，就不能再同时作为 wholesale colocation 收入计算。

### 宏观层面：资本成本与外部约束

宏观层面关注项目外部环境如何影响微观模型：

| 宏观变量 | 传导机制 | 对 NPV 的方向 |
|---|---|---|
| 利率 / 信用利差 | WACC 上升、债务利息上升 | 折现率提高，NPV 下降 |
| 电价 | Opex 上升，EBITDA margin 下降 | UFCF 下降 |
| 设备通胀 | Capex/MW 上升 | 初始投资增加，NPV 下降 |
| 设备交期 / 电网排队 | 收入启动延后 | 早期现金流损失，NPV 下降 |
| AI 需求 | 利用率、价格、合同期限改善 | revenue visibility 提高，NPV 上升 |
| 政策 / 水资源 / 环评 | 许可周期或选址约束 | 延迟上线或提高合规成本 |

---

## 3. SEC Filing 数据支撑

### 3.1 CoreWeave：高增长、高资本开支、高杠杆 AI cloud 样本

来源：

- CoreWeave FY2025 Form 10-K：<https://www.sec.gov/Archives/edgar/data/1769628/000176962826000104/crwv-20251231.htm>
- CoreWeave Q1 2026 Form 10-Q：<https://www.sec.gov/Archives/edgar/data/1769628/000176962826000222/crwv-20260331.htm>

核心数据：

| 指标 | FY2023 | FY2024 | FY2025 | Q1 2026 |
|---|---:|---:|---:|---:|
| Revenue | $229M | $1.915B | $5.131B | $2.078B |
| PPE purchases / capex | $2.943B | $8.702B | $10.309B | $7.695B |
| PPE, net | n.a. | $11.915B | $30.557B | $36.424B |
| Operating lease liability | n.a. | $2.602B | $8.195B | $10.050B |
| Long-term debt | n.a. | $7.926B | $21.373B | $24.859B |

分析含义：

CoreWeave 是 AI 数据中心 ROI 分析中非常有价值的样本，因为其收入增长、PPE 增长和债务增长几乎同步发生。该模式说明 AI cloud 的增长并非轻资产 SaaS 模式，而是以大规模前置资本投入换取未来算力收入。其 NPV 对三个变量特别敏感：

1. **Capex/MW 或 Capex/GPU**：固定资产投资越高，初始现金流压力越大。
2. **Time-to-live**：如果设备或电力接入延迟，收入确认会后移，但债务和租赁成本仍可能先发生。
3. **WACC / 利率**：债务规模较高时，利率上行会同时影响折现率和现金利息支出。

### 3.2 IREN：电力资源转 AI cloud 的样本

来源：

- IREN FY2025 Form 10-K：<https://www.sec.gov/Archives/edgar/data/1878848/000187884825000063/iren-20250630.htm>
- IREN Q3 FY2026 Form 10-Q：<https://www.sec.gov/Archives/edgar/data/1878848/000187884826000026/iren-20260331.htm>

核心数据：

| 指标 | FY2023 | FY2024 | FY2025 | FY2026 YTD / Q3 |
|---|---:|---:|---:|---:|
| Revenue | $75.5M | $187.2M | $501.0M | $569.8M YTD |
| PPE, net | n.a. | $441.4M | $1.931B | $2.115B at Q1 FY2026 |
| PPE purchases / capex | n.a. | n.a. | n.a. | $1.669B YTD to Mar. 31, 2026 |
| Finance lease liability | n.a. | n.a. | n.a. | $274.3M at Mar. 31, 2026 |

其他重要披露：

- FY2025 10-K 披露 NVIDIA GPU purchase commitments，包括 4,200 台 B200 GPUs 约 $192.9M、1,200 台 B300 GPUs 约 $71.4M，以及 1,200 台 GB300s 约 $96.2M。
- Q3 FY2026 10-Q 披露与 NVIDIA 的 GPU services agreement：IREN 将在 Texas Childress facilities 提供 dedicated GPU services，五年合同，总合同价值约 $3.4B，服务分三批预计在 2027 年部署。

分析含义：

IREN 的价值在于展示“电力资源 / 站点能力”如何转化为 AI cloud 收益。其原有能力偏电力和基础设施，AI GPU 合同和 NVIDIA 合作使收益端具备更高可见度。对 ROI 模型而言，IREN 可以用于检验：

```text
Power access + site buildout + GPU procurement
→ dedicated GPU services capacity
→ long-term contracted revenue
→ EBITDA / UFCF / NPV
```

这里最关键的 X 是 power availability、GPU procurement cost、deployment timing 和 customer contract value。

### 3.3 Nebius：大客户长约锁定未来收益的样本

来源：

- Nebius FY2025 Form 20-F：<https://www.sec.gov/Archives/edgar/data/1513845/000110465926052948/nbis-20251231x20f.htm>
- Nebius Q1 2026 Form 6-K：<https://www.sec.gov/Archives/edgar/data/1513845/000110465926064092/nbis-20260331x6k.htm>

核心数据：

| 指标 | 2023 | 2024 | 2025 |
|---|---:|---:|---:|
| Nebius segment revenue | $9.6M | $68.3M | $480.3M |
| Total revenue | n.a. | n.a. | $529.8M |
| Nebius segment adjusted EBITDA | n.a. | n.a. | $59.0M |
| Long-lived assets | n.a. | n.a. | $6.492B |

重要后续事项：

- 2026 年 3 月，NVIDIA private placement gross proceeds 约 $2.0B，用于支持 full-stack AI cloud platform 和 greenfield data center development。
- 2026 年 3 月，Meta 与 Nebius 签订五年 AI infrastructure supply agreement，约 $12B dedicated compute capacity，另有最多 $15B 的 additional available compute capacity commitment。
- Nebius 同期发行 convertible senior notes，合计约 $4.34B，用于 data center development 和 AI infrastructure investments。

分析含义：

Nebius 说明了一个核心现象：在 AI 数据中心项目中，长期客户合同本身就是建设融资和 ROI 的关键变量。若未来收入已由高信用客户的合约部分锁定，项目的风险折现率和融资可得性会改善；反之，如果项目依赖 spot demand 或短期 GPU rental，NPV 应使用更高的风险折现率。

### 3.4 Oracle：宏观需求与云迁移背景

来源：

- Oracle FY2026 Form 10-K：<https://www.sec.gov/Archives/edgar/data/1341439/000119312526277521/orcl-20260531.htm>

核心数据：

| 指标 | FY2024 | FY2025 | FY2026 |
|---|---:|---:|---:|
| Cloud revenue as % of total revenue | 37% | 43% | 51% |
| R&D expense | $8.9B | $9.9B | $10.3B |

分析含义：

Oracle 的披露不够细，无法直接支持单个数据中心的 MW / capex / NPV 测算，但可以作为宏观云需求和企业工作负载迁移的背景证据。它适合用于说明 cloud infrastructure demand 的长期方向，不适合作为微观项目 ROI 的核心样本。

---

## 4. ROI 模型的专业化表达

建议将模型分成四个模块：

### 模块 A：建设成本

```text
Initial Capex = Land + Grid Interconnection + Electrical Equipment + Cooling + Building/EPC + Network + GPU/Servers
Capex per IT MW = Initial Capex / IT MW
```

关键敏感变量：

- Electrical equipment cost inflation
- GPU purchase price
- Cooling system cost
- Grid interconnection cost
- Construction delay

### 模块 B：收入

```text
Revenue_t = Sellable Capacity_t × Utilization_t × Unit Price_t × Contract Coverage_t
```

对于 AI cloud：

```text
Revenue_t = GPU Count_t × Available Hours_t × Utilization_t × $/GPU-hour
```

对于 colocation：

```text
Revenue_t = Contracted IT kW_t × $/kW-month × 12
```

### 模块 C：运营成本

```text
Power Cost_t = IT Load_t × PUE × Hours × Electricity Price
Cash Opex_t = Power Cost_t + Labor + Maintenance + Network + Lease Cash Cost
EBITDA_t = Revenue_t - Cash Opex_t
```

关键敏感变量：

- PUE
- Power price
- Utilization
- Maintenance cost
- SLA / downtime

### 模块 D：资本结构与估值

```text
UFCF_t = EBITDA_t - Tax_t - Maintenance Capex_t - Working Capital_t
NPV = Σ UFCF_t / (1 + WACC)^t - Initial Capex
```

宏观敏感性：

- Risk-free rate 上升：WACC 上升，NPV 下降。
- Credit spread 上升：债务成本上升，利息支出和融资可得性恶化。
- Debt share 上升：若项目现金流稳定，ROE 可能提高；若收入延迟，财务风险放大。

---

## 5. 如何把 X 和 Y 建立“最佳联系”

本课题的核心不是找一个单变量回归，而是建立一套可解释的驱动树。建议将 X 分为三类：

### 第一类：硬约束 X

这些变量决定项目能否建成：

- Power availability
- Grid interconnection queue
- Transformer / switchgear / UPS / cooling equipment availability
- Land and permitting
- Water / environmental constraints

这些变量的影响主要体现在：

```text
Delay in time-to-power → Revenue delay → UFCF delay → NPV decline
```

### 第二类：经济性 X

这些变量决定单位产能是否赚钱：

- Capex per MW
- GPU cost per unit
- Power price
- PUE
- Utilization
- Contracted price

这些变量的影响主要体现在：

```text
Unit economics = Revenue per MW - Cash cost per MW - Maintenance capex per MW
```

### 第三类：金融变量 X

这些变量决定现金流如何被折现：

- WACC
- Debt cost
- Lease cost
- Credit availability
- Customer credit quality

这些变量的影响主要体现在：

```text
Same UFCF, higher WACC → lower NPV
Same WACC, higher contract certainty → lower risk premium → higher NPV
```

因此，推荐的核心关系是：

```text
NPV = f(Capex/MW, Time-to-Power, Utilization, Unit Price, Power Cost, PUE, Contract Length, WACC)
```

这条公式能同时容纳微观建设变量和宏观利率变量，也能解释为什么 SEC filings 中的 capex、PPE、debt、lease、contract value 都是关键证据。

---

## 6. 建议的敏感性分析表

后续模型应至少做以下 sensitivity：

| 变量 | Base Case | Downside | Upside | NPV 影响机制 |
|---|---:|---:|---:|---|
| Capex/MW | 100% | +10% / +20% | -10% | 初始投资变化 |
| Time-to-power | 按计划 | 延迟 6-12 个月 | 提前 3-6 个月 | 收入确认时点变化 |
| Utilization | 80%-90% | 60%-70% | 90%+ | 收入和 EBITDA margin 变化 |
| Power price | 当前合约电价 | +20% | -10% | 现金 opex 变化 |
| PUE | 1.2-1.4 | 1.5+ | 1.1-1.2 | 电力成本效率变化 |
| GPU / equipment cost | 当前报价 | +15% / +30% | -10% | capex 和折旧压力变化 |
| WACC | 8%-10% | +100-200 bps | -100 bps | 折现率变化 |
| Contracted revenue coverage | 70%-90% | 低于 50% | 90%+ | 收入确定性和风险溢价变化 |

其中最适合用 SEC filing 支撑的变量是：

- Revenue
- Capex / PPE purchases
- PPE net
- Debt and lease obligations
- Interest expense
- Customer contracts
- Purchase commitments
- Long-term service agreements

最需要外部数据源补充的变量是：

- 设备级价格：transformer、switchgear、UPS、PDU、cooling、generator
- 设备级交期：lead time / backlog
- 项目级 MW：facility MW、IT MW、critical load
- 电价：contracted electricity price、transmission cost、demand charge
- GPU 市场价格与可用性

---

## 7. 初步研究判断

基于现有文档框架和 SEC 数据，本文的投资分析判断可以这样表述：

AI 数据中心的 ROI 不应被简化为“建多少 MW”或“买多少 GPU”。真正决定 NPV 的，是资本投入与可销售算力之间的时间匹配。若项目拥有低成本电力、可快速接入电网、稳定设备供应和高信用客户长约，则即便 capex 较高，也可能通过更高收入可见度和更低风险溢价获得较高 NPV。反之，若电力设备、GPU、冷却或融资任一环节延迟，项目会出现典型的“capex 已发生、revenue 未启动”的现金流错配，NPV 会快速恶化。

SEC filings 提供了这个判断的财务证据：CoreWeave 体现高 capex / 高债务 / 高收入增长的 AI cloud 扩张模式；IREN 体现电力资源向 GPU services 转化的路径；Nebius 体现大客户长约和战略投资对项目融资与收益确定性的作用；Oracle 则提供云需求持续扩张的宏观背景。将这些数据映射回项目模型后，最重要的分析任务是量化每个 X 对 NPV 的边际影响，并识别最具解释力的变量组合。

---

## 8. 下一步数据清单

为了把本文从框架分析推进到量化模型，需要继续补充：

| 数据 | 优先级 | 来源建议 | 用途 |
|---|---|---|---|
| Project IT MW / critical load | 高 | 公司披露、项目公告、地方许可、电网文件 | 计算 capex/MW 和 revenue/MW |
| Capex breakdown | 高 | SEC footnotes、investor presentation、company transcripts | 拆分 electrical / cooling / GPU / building |
| Equipment price and lead time | 高 | 供应商、行业数据库、采购数据 | 量化设备瓶颈对 NPV 的影响 |
| Contract price | 高 | SEC material contracts、customer agreements、industry pricing | 估算 revenue |
| Power price | 高 | PPA、电价数据库、utility tariff | 估算 opex |
| Financing terms | 高 | SEC debt footnotes、credit agreements、notes indentures | 估算 WACC / interest sensitivity |
| Utilization ramp | 中 | management guidance、peer comparison | 估算 revenue ramp |
| PUE / cooling efficiency | 中 | sustainability report、technical disclosure | 估算电力成本 |

---

## 9. 可引用的 SEC 来源清单

- CoreWeave FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000104/crwv-20251231.htm>
- CoreWeave Q1 2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000222/crwv-20260331.htm>
- IREN FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1878848/000187884825000063/iren-20250630.htm>
- IREN Q3 FY2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1878848/000187884826000026/iren-20260331.htm>
- Nebius FY2025 Form 20-F: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926052948/nbis-20251231x20f.htm>
- Nebius Q1 2026 Form 6-K: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926064092/nbis-20260331x6k.htm>
- Oracle FY2026 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1341439/000119312526277521/orcl-20260531.htm>

