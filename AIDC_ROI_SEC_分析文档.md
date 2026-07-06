# AIDC / 数据中心 ROI 分析：从实体 X 到收益 Y 的投资框架

日期：2026-07-06  
Topic：数据中心 ROI 分析  
Target：找出驱动数据中心建设的核心变量 X，并建立 X 与收益 Y，尤其是 NPV、IRR、UFCF 之间的最佳联系。  
数据口径：原始研究文档 + 用户补充的卖方/公司资料 + SEC filings + 公开行业资料。所有非 SEC 数据均作为模型参数或交叉验证，不等同于公司正式披露。

---

## 1. 一句话结论

AIDC 本质上是一座生产 AI 算力的工厂。ROI 不是由 GPU 单独决定，也不是由电力单独决定，而是由一组实体资产 X 共同决定：

```text
土地/园区/并网
+ 电力设备
+ 冷却系统
+ 机房与 EPC
+ AI 机柜 / AI Pod
+ 高速互联
+ 运维与控制系统
→ 可稳定运行的 AI 集群
→ 可计费容量与收入
→ UFCF
→ NPV / IRR / ROI
```

因此，本课题最核心的研究问题是：

```text
每一类实体 X 如何影响容量、上线时间、Capex、Opex、PUE、SLA、客户愿付价格和融资成本，
最后如何影响项目 NPV？
```

---

## 2. 三层逻辑链

### 第一层：实体 X

实体 X 是数据中心真正需要建设、采购、安装和运维的资产。

| 实体 X | 典型组成 | 它决定什么 |
|---|---|---|
| 土地、园区与并网 | 土地、输电线、变电站接入、许可 | 能否建、能建多大、何时通电 |
| 电力设备 | 变压器、开关柜、UPS、PDU、母线、备用电源 | 电能否稳定送至机柜、可靠性、冗余 |
| 冷却系统 | 冷水机、冷却塔、CDU、液冷管路、泵、风机 | 可支持的机柜密度、PUE、能耗与稳定性 |
| 机房与 EPC | 建筑、机柜空间、消防、安防、施工、调试 | 建设成本、上线时间、可用性 |
| AI 机柜 / AI Pod | NVIDIA 整机柜或其他高密度 AI 系统 | 每 MW 可承载的 AI 能力、IT Capex、更新风险 |
| 高速互联 | 交换机、光模块、光纤、InfiniBand / Ethernet 集群网络 | 集群是否可用于大规模训练/推理、客户愿付价格 |
| 运维与控制系统 | DCIM、监控、维护、现场团队 | SLA、故障率、运维成本、客户留存 |

### 第二层：中间变量

这些不是最上游 X，而是 X 共同作用后的结果。

| 中间变量 | 含义 | 由哪些 X 决定 |
|---|---|---|
| Facility MW | 园区可获得和使用的总电力 | 土地/并网、电力设备 |
| IT MW | 真正送到 AI 机柜和网络设备的电力 | 电力设备、冷却、PUE |
| Rack / Pod capacity | 可部署多少高密度 AI 机柜 | IT MW、冷却、机房、AI Pod |
| PUE | 总设施用电 / IT 设备用电 | 冷却、电力架构、机房设计 |
| Availability / SLA | 可用性和故障率 | 电力冗余、冷却冗余、运维系统 |
| Time-to-Power / Time-to-Live | 从建设到通电、从通电到客户计费的时间 | 并网、设备交期、EPC、调试 |
| Capex/MW | 每新增 1MW IT 容量需要投入多少钱 | 全部实体 X |
| Opex/MW | 每年维持 1MW 运行需要多少钱 | 电价、PUE、运维、维护 |

### 第三层：收益 Y

最终 Y 是项目值多少钱：

```text
Revenue
- Cash Opex
- Maintenance Capex
- Tax / Working Capital
= UFCF

NPV = Σ UFCF_t / (1 + WACC)^t - Initial Capex
```

所以正确逻辑不是：

```text
NVIDIA 机柜 → NPV
```

而是：

```text
NVIDIA 机柜 + 电力设备 + 冷却 + 高速互联 + 机房/EPC + 运维
→ 可交付 AI 容量、效率、上线速度、SLA
→ 收入、成本、现金流
→ NPV
```

---

## 3. 实体 X 的 Capex 占比：两个口径

这是本分析最重要的数据补充。公开资料通常不会逐项披露“变压器、UPS、冷却、AI Pod、网络”在同一个项目中的精确比例，所以这里使用两个可落地的建模口径。

### 3.1 口径 A：Facility-only capex，不含 GPU / AI 机柜

适用于 wholesale colocation、shell + powered shell、或仅分析基础设施层。参考公开行业资料中 EMEA 数据中心 build cost 约 **$7.3M-$13.3M/MW commissioned IT load**，该口径包含 land、shell、electrical、mechanical、cooling、fire safety 和 fit-out，但不含客户自带的 GPU 云硬件。来源：Savills 数据经 ITPro 报道。

| 实体 X | Facility-only capex 参考占比 | 对 NPV 的核心影响 | 数据依据 |
|---|---:|---|---|
| 土地、园区与并网 | 5%-15% | Facility MW、time-to-power、扩容空间 | 行业 build cost 包含 land；用户补充资料强调 power access 是 NBIS/IREN 的核心约束 |
| 电力设备 | 30%-45% | IT MW、冗余、SLA、上线瓶颈 | 数据中心 build cost 主要由 electrical / mechanical 系统驱动；AI 高密度进一步提高配电压力 |
| 冷却系统 | 15%-30% | PUE、rack density、可支持液冷机柜 | 用户资料：NBIS PUE 1.10-1.13，IREN NVIDIA 合同 PUE 约 1.30；高密度 AI 需要液冷/CDU |
| 机房与 EPC | 20%-35% | 建设周期、机柜空间、消防安防、调试 | Savills/ITPro build cost 包含 shell、fire safety、fit-out |
| 高速互联基础管线 | 3%-8% | 光纤路径、机房内布线、网络可用性 | 传统 facility 口径通常只包含低压/弱电和基础网络，不含大规模 AI 集群交换机 |
| 运维与控制系统 | 2%-5% | DCIM、监控、SLA、故障恢复 | 通常体现在 fit-out、commissioning 和 control systems 中 |
| Contingency / soft cost | 5%-10% | 许可、设计、项目管理、不可预见成本 | 建设模型常用预备费口径 |

Facility-only 口径的关键结论：**电力设备 + 冷却 + EPC 往往占基础设施 capex 的大头**。所以在不含 GPU 的数据中心项目中，电力和冷却是最直接影响 Capex/MW、PUE 和 time-to-power 的 X。

### 3.2 口径 B：Full-stack AI DC capex，含 AI 机柜 / 网络

适用于 CoreWeave、IREN、Nebius 这类 GPU-as-a-Service / neocloud 项目。用户补充资料给出的 IREN 口径显示：Colo 约 **$10M-$15M/MW**，GPU Cloud 约 **$40M-$45M/MW**。这意味着当项目从“有电和机房”升级为“可销售 AI 算力”时，AI 机柜、GPU、网络和相关系统会成为绝对大头。

| 实体 X | Full-stack AI DC capex 参考占比 | 说明 | 数据依据 |
|---|---:|---|---|
| 土地、园区与并网 | 2%-8% | 在 full-stack 中被 GPU/AI Pod 稀释，但仍决定能否开工和扩容 | 用户补充资料：NBIS 签约容量 >3,500MW、IREN secured power portfolio 约 6GW |
| 电力设备 | 8%-15% | 高密度 GPU 需要更强配电、UPS、母线和冗余 | Facility-only 电力占比较高；full-stack 中因 GPU capex 更大而占比下降 |
| 冷却系统 | 5%-10% | 液冷、CDU、冷板、泵和换热系统成为 AI 项目必需项 | 用户补充资料及 Morgan Stanley/Tom's Hardware 对 NVL72 冷却部件成本的报道 |
| 机房与 EPC | 5%-12% | 包括建筑、消防、调试、机柜空间和 fit-out | Savills/ITPro build cost 区间作为基础设施锚 |
| AI 机柜 / AI Pod | 55%-75% | GPU、CPU、内存、整机柜、存储、电源模块是 full-stack 最大 capex | 用户补充 IREN GPU Cloud $40M-$45M/MW；Tom's Hardware 引 Morgan Stanley 对 NVL72 / VR200 rack 成本估算 |
| 高速互联 | 5%-12% | InfiniBand / Ethernet fabric、交换机、光模块、光纤；直接影响训练集群可用性 | AI 训练需要非阻塞、高带宽、低延迟网络；用户资料将其列为客户愿付价格驱动 |
| 运维与控制系统 | 1%-3% | DCIM、集群监控、现场团队、SLA 体系 | 对初始 capex 占比小，但对客户留存和 downtime 成本重要 |

Full-stack 口径的关键结论：**AI 机柜 / AI Pod 是 capex 最大项，但电力、冷却和互联决定这些 GPU 是否真的能变成可销售收入**。如果某一类基础设施 X 延迟，GPU 可能已经采购并开始折旧，但 revenue 尚未启动，NPV 会明显受损。

### 3.3 为什么要分两个口径

同一个 MW 在不同商业模式下含义不同：

| 商业模式 | Capex/MW 口径 | 收入逻辑 | 适用公司 |
|---|---:|---|---|
| BTC mining | $1M-$1.5M/MW | 挖矿收益，设备更新快 | IREN 历史业务 |
| Colo / powered shell | $10M-$15M/MW | $/kW-month 或长期租赁 | IREN 转型后的基础设施残值参考 |
| GPU Cloud / AI DC | $40M-$45M/MW | GPU services、$/GPU-hour、dedicated capacity contract | IREN、CRWV、NBIS |

该对比来自用户补充的 Jefferies / GS 等卖方资料。它说明本研究必须明确 ROI 的分母：如果分母只含基础设施 capex，ROI 会偏高；如果分母包含 AI 机柜、GPU、网络和更新风险，模型才接近真正的 full-stack AI DC 经济性。

---

## 4. 公司数据支撑

### 4.1 CoreWeave：高收入增长、高 Capex、高债务

SEC 来源：

- CoreWeave FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000104/crwv-20251231.htm>
- CoreWeave Q1 2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000222/crwv-20260331.htm>

| 指标 | FY2023 | FY2024 | FY2025 | Q1 2026 |
|---|---:|---:|---:|---:|
| Revenue | $229M | $1.915B | $5.131B | $2.078B |
| PPE purchases / capex | $2.943B | $8.702B | $10.309B | $7.695B |
| PPE, net | n.a. | $11.915B | $30.557B | $36.424B |
| Operating lease liability | n.a. | $2.602B | $8.195B | $10.050B |
| Long-term debt | n.a. | $7.926B | $21.373B | $24.859B |

用户补充资料：

- RPO 约 $99B，但对应 MW 未披露。
- 客户包括 Meta、OpenAI、Microsoft、Anthropic 等。
- GPU 折旧政策约 6 年，市场对实际经济寿命存在争议。

分析含义：CRWV 是“RPO 支撑融资、融资推动 capex、capex 形成未来收入”的典型样本。它最适合用于分析 WACC、债务成本、GPU 折旧年限和 time-to-live 对 NPV 的影响。

### 4.2 IREN：最适合做项目级 ROI base case

SEC 来源：

- IREN FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1878848/000187884825000063/iren-20250630.htm>
- IREN Q3 FY2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1878848/000187884826000026/iren-20260331.htm>

| 指标 | FY2023 | FY2024 | FY2025 | FY2026 YTD / Q3 |
|---|---:|---:|---:|---:|
| Revenue | $75.5M | $187.2M | $501.0M | $569.8M YTD |
| PPE, net | n.a. | $441.4M | $1.931B | $2.115B at Q1 FY2026 |
| PPE purchases / capex | n.a. | n.a. | n.a. | $1.669B YTD to Mar. 31, 2026 |
| Finance lease liability | n.a. | n.a. | n.a. | $274.3M at Mar. 31, 2026 |

SEC 还披露了 NVIDIA GPU purchase commitments，包括 B200、B300 和 GB300 相关采购安排。Q3 FY2026 10-Q 披露与 NVIDIA 的 dedicated GPU services agreement，总合同价值约 $3.4B，五年期，目标 2027 年分批部署。

用户补充资料中，IREN Childress 的 MSFT 项目最适合做 base case：

| 变量 | 口径 |
|---|---:|
| 规模 | 200 MW，液冷 GB300 GPU |
| 合同价值 | 约 $9.7B / 5 年 |
| 预付款 | 约 $1.9B |
| GPU 融资 | 约 $3.65B，约 5.95% 加权成本 |
| 投产时间 | 2026 年底首批，2027 年完成 |
| 项目回报 | 无杠杆 IRR >20%；有杠杆 IRR 约 25.4%；NPV @ 9% 约 $881M |

分析含义：IREN 把“土地/电力资源”转化为“GPU 云合同收入”，链条最完整：

```text
Secured power + site
→ electrical/cooling/EPC buildout
→ 200MW AI capacity
→ MSFT / NVIDIA dedicated GPU services
→ UFCF / NPV / IRR
```

### 4.3 Nebius：大客户长约与未来 capacity ramp

SEC 来源：

- Nebius FY2025 Form 20-F: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926052948/nbis-20251231x20f.htm>
- Nebius Q1 2026 Form 6-K: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926064092/nbis-20260331x6k.htm>

| 指标 | 2023 | 2024 | 2025 |
|---|---:|---:|---:|
| Nebius segment revenue | $9.6M | $68.3M | $480.3M |
| Total revenue | n.a. | n.a. | $529.8M |
| Nebius segment adjusted EBITDA | n.a. | n.a. | $59.0M |
| Long-lived assets | n.a. | n.a. | $6.492B |

SEC 披露的后续事项包括 NVIDIA private placement gross proceeds 约 $2.0B，以及 Meta 五年 AI infrastructure supply agreement 约 $12B dedicated compute capacity，另有最多 $15B 的 additional capacity commitment。

用户补充资料显示，NBIS 签约容量超过 3,500MW，2026 年底目标超过 4,000MW，2026Q1 活跃容量约 220MW。这个差距说明：NBIS 的投资逻辑不是看当前收入，而是看签约容量能否按期转化为 active MW 和 billed revenue。

### 4.4 Oracle：宏观需求和资本约束样本

SEC 来源：

- Oracle FY2026 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1341439/000119312526277521/orcl-20260531.htm>

| 指标 | FY2024 | FY2025 | FY2026 |
|---|---:|---:|---:|
| Cloud revenue as % of total revenue | 37% | 43% | 51% |
| R&D expense | $8.9B | $9.9B | $10.3B |

Oracle 的 OCI 项目 MW、PUE、Capex/MW 和项目债务成本披露不足，因此不适合作为单项目 ROI base case。但它适合证明宏观需求：云收入占比提升、AI 和 cloud infrastructure 正在变成公司资本配置的核心。

---

## 5. 宏观思路：宏观变量如何进入微观 NPV

宏观分析不能脱离主线。它不是另一个故事，而是通过四条路径进入项目模型。

| 宏观变量 | 进入模型的位置 | 对 Y 的影响 |
|---|---|---|
| 利率 / 信用利差 | WACC、债务利息、融资可得性 | 折现率上升，利息现金流上升，NPV 下降 |
| 电力供需 / 电网拥堵 | time-to-power、power price、可获得 Facility MW | 延迟上线或提高 Opex |
| 设备供应链 / 通胀 | Capex/MW、设备交期、contingency | 初始 capex 上升，收入启动后移 |
| AI 需求周期 | utilization、unit price、contract tenor、RPO | 收入可见度和客户愿付价格变化 |
| 政策 / 税收 / 环评 / 水资源 | permit timeline、tax、capex、site selection | 改变建设可行性和长期成本 |

公开宏观数据支持：

- IEA《Energy and AI》报告称，AI 普及使“电力 for data centres”成为能源系统核心问题，并提供 2030 年电力需求情景。来源：<https://www.iea.org/reports/energy-and-ai>
- LBNL《2024 United States Data Center Energy Usage Report》口径被广泛引用：美国数据中心用电 2023 年约 176TWh，2028 年可能升至 325-580TWh。来源：<https://eta-publications.lbl.gov/sites/default/files/2024-12/lbnl-2024-united-states-data-center-energy-usage-report.pdf>
- Savills/ITPro 报道 EMEA 数据中心 build cost 约 $7.3M-$13.3M/MW commissioned IT load，且 power availability 是建设约束。来源：<https://www.itpro.com/infrastructure/data-centres/lack-of-power-supplies-hitting-data-centre-construction>
- JLL 相关报道显示美国商业电价自 2020 年以来上升约 30%，grid connection wait time 约 4 年，power access 已成为“new real estate”。来源：<https://www.techradar.com/pro/1-trillion-worth-of-data-centers-by-2030-us-leads-the-way-when-it-comes-to-colocation-and-hyperscale-capacity-report-posits>

宏观层面的结论是：**利率、电网和供应链不是背景噪音，而是通过 WACC、Capex/MW、time-to-power 和 Opex/MW 直接改变 NPV。**

---

## 6. 最佳 X-Y 关系：建议的核心函数

本研究不应做一个单变量解释，而应建立驱动树：

```text
NPV = f(
  Capex/MW,
  Time-to-Power,
  IT MW,
  Utilization,
  Unit Price,
  Power Price,
  PUE,
  Contract Length,
  WACC,
  Refresh Capex
)
```

建议把变量分成三组：

| 类型 | 变量 | 为什么重要 |
|---|---|---|
| 建设约束 X | 土地、并网、电力设备、冷却、EPC | 决定能否建、建多大、何时上线 |
| 单位经济 X | Capex/MW、PUE、电价、利用率、价格 | 决定每 MW 是否赚钱 |
| 金融与合同 X | WACC、债务成本、合同期限、客户信用 | 决定现金流如何折现，以及融资能否闭环 |

---

## 7. Sensitivity 设计

以 IREN Childress 200MW 项目为 base case，可以做以下 sensitivity：

| 变量 | Base case | Downside | Upside | NPV 影响机制 |
|---|---:|---:|---:|---|
| Capex/MW | $40M-$45M/MW | +10% / +20% | -10% | 初始投资变化 |
| Time-to-power | 2026 年底首批、2027 年完成 | 延迟 6-12 个月 | 提前 3-6 个月 | 收入启动时间变化 |
| Power price | $0.05/kWh | +20% | -10% | Opex/MW 变化 |
| PUE | 1.30 | 1.40-1.50 | 1.15-1.25 | 电力成本和可用 IT MW 变化 |
| WACC | 9% | +100-200 bps | -100 bps | 折现率变化 |
| Contract coverage | 5 年长约 | 未完全签约 | 更高预付款 / 更强客户信用 | 收入确定性和融资成本变化 |
| GPU useful life | 5 年 | 3-4 年 | 6 年 | 折旧、残值、refresh capex 变化 |

最重要的 sensitivity 不是“某个设备涨价多少”，而是：

```text
设备/并网/冷却延迟
→ GPU 或机房 capex 已发生
→ revenue start date 后移
→ early UFCF 下降
→ NPV 对时间高度敏感
```

---

## 8. 证据等级

| 等级 | 来源 | 本文用途 |
|---|---|---|
| Level 1 | SEC 10-K、10-Q、20-F、6-K、material contracts | 正式财务、债务、PPE、收入、重大合同 |
| Level 2 | 公司公告、业绩会、投资者材料 | MW、项目时间线、管理层指引 |
| Level 3 | Citi、Morgan Stanley、Goldman Sachs、Jefferies、行业报道 | Capex/MW、PUE、合同经济性、项目 IRR/NPV 假设 |
| Level 4 | 行业新闻与第三方估算 | 设备价格、grid wait time、宏观供需背景 |

模型应以 Level 1 做财务锚，以 Level 2/3 补项目参数，以 Level 4 做敏感性和风险假设。

---

## 9. 后续还缺什么数据

为了把本文推进成可跑的 Excel 模型，还需要：

| 数据 | 优先级 | 用途 |
|---|---|---|
| 每个项目的 Facility MW、IT MW、active MW | 高 | 计算 capex/MW、revenue/MW |
| Capex breakdown | 高 | 拆分电力、冷却、EPC、AI Pod、网络 |
| 设备价格和交期 | 高 | 量化供应链瓶颈对 NPV 的影响 |
| 合同价格 | 高 | 估算 $/MW、$/GPU-hour、收入 ramp |
| 电价 / PPA | 高 | 估算 Opex/MW |
| 融资条款 | 高 | 估算 WACC、利息支出、DSCR |
| GPU refresh cycle 和残值 | 中 | 估算 terminal value 和 maintenance capex |
| PUE / WUE / availability | 中 | 估算能效、稳定性、SLA 风险 |

---

## 10. 来源清单

SEC filings:

- CoreWeave FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000104/crwv-20251231.htm>
- CoreWeave Q1 2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1769628/000176962826000222/crwv-20260331.htm>
- IREN FY2025 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1878848/000187884825000063/iren-20250630.htm>
- IREN Q3 FY2026 Form 10-Q: <https://www.sec.gov/Archives/edgar/data/1878848/000187884826000026/iren-20260331.htm>
- Nebius FY2025 Form 20-F: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926052948/nbis-20251231x20f.htm>
- Nebius Q1 2026 Form 6-K: <https://www.sec.gov/Archives/edgar/data/1513845/000110465926064092/nbis-20260331x6k.htm>
- Oracle FY2026 Form 10-K: <https://www.sec.gov/Archives/edgar/data/1341439/000119312526277521/orcl-20260531.htm>

用户补充资料:

- `C:\Users\Charlie\.codex\attachments\ee2be4c3-4152-4218-9e25-b3cc45c2a278\pasted-text.txt`，来源标注为 Citi、Morgan Stanley、Goldman Sachs、Jefferies、公司公告等，数据截至 2026-07-06。

公开行业资料:

- IEA, Energy and AI, 2025: <https://www.iea.org/reports/energy-and-ai>
- LBNL, 2024 United States Data Center Energy Usage Report: <https://eta-publications.lbl.gov/sites/default/files/2024-12/lbnl-2024-united-states-data-center-energy-usage-report.pdf>
- ITPro / Savills on EMEA data centre build costs and power constraints: <https://www.itpro.com/infrastructure/data-centres/lack-of-power-supplies-hitting-data-centre-construction>
- TechRadar / JLL on U.S. data center pipeline, power cost and grid connection delays: <https://www.techradar.com/pro/1-trillion-worth-of-data-centers-by-2030-us-leads-the-way-when-it-comes-to-colocation-and-hyperscale-capacity-report-posits>
- Tom's Hardware citing Morgan Stanley estimates for NVIDIA rack-scale system and liquid-cooling component costs: <https://www.tomshardware.com/tech-industry/artificial-intelligence/nvidias-memory-costs-soar-485-percent-latest-ai-systems-now-cost-usd7-8-million-to-build-memory-now-comprises-25-percent-of-the-total-cost-rubin-gpus-a-mere-usd50-000-apiece> and <https://www.tomshardware.com/pc-components/cooling/cooling-system-for-a-single-nvidia-blackwell-ultra-nvl72-rack-costs-a-staggering-usd50-000-set-to-increase-to-usd56-000-with-next-generation-nvl144-racks>
