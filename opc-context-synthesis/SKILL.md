---
name: opc-context-synthesis
description: Produce a full OPC diagnosis from existing context (chat records, repos, business info, prior conversations) without interactive Q&A. Use when the user asks for OPC analysis but rich data already exists in memory, session_search, or attached documents, skipping the interactive questionnaire and going straight to resource audit → niche positioning → MVP recommendations.
tags: [opc, diagnosis, synthesis, direct-analysis, one-person-business]
---

# OPC 上下文直出分析

## 目标

当用户已经有大量上下文（聊天记录、项目链接、业务信息、历史对话）时，**跳过 OPC 交互式问卷**，直接基于已有数据产出完整的 OPC 诊断和行动建议。

这是对 `opc-orchestrator` 交互模式的补充——不是替代，而是"数据充足时的快捷通道"。

## 适用场景（满足任一即可触发）

- 用户转发了一段聊天记录/对话，要求用 OPC 视角分析
- 用户分享了项目链接/产品/竞品，要求判断 OPC 意义
- 用户说"帮我用 OPC 分析一下"，但 memory/session_search 中已有足够业务信息
- 用户不想走完整问卷流程，直接要结论

## 前置数据采集（必须完成，不可跳过）

在产出分析之前，**先花一轮工具调用**收集上下文：

1. **读 memory**：获取用户画像、业务信息、历史决策
2. **session_search**：搜索相关关键词，获取过去对话中的业务数据
3. **读取用户提供的链接/文档**：GitHub repos、飞书文档、网页等
4. **检查 opc-doc/ 是否存在**：如果有历史 OPC 产出，直接读取，不重复收集

**原则**：宁可多花一轮采集，不可基于空洞假设产出结论。如果上下文确实不足，退回 `opc-orchestrator` 走交互模式。

## 执行步骤

### Step 1：数据采集与提炼

从所有来源中提炼以下 OPC 结构化信息：

| 信息类别 | 采集来源 |
|----------|----------|
| 创始人资源 | memory user profile + 对话中提及的能力/关系/渠道 |
| 业务定位 | memory + 当前对话 + 历史 session |
| 目标客户 | memory + 用户转发的对话中的线索 |
| 现有产品/服务 | memory + skills 列表 + 工具链 |
| 约束条件 | memory + 对话中提及的资金/时间/精力限制 |
| 外部信号 | 用户提供的链接/文档/对话中的行业信息 |

### Step 2：直接产出 OPC 诊断（跳过交互）

按以下结构直接输出，每一步不需要用户确认即可推进：

**一、资源盘点摘要**
- 从已有信息中提取 8 类资源，标注"已确认"和"推测"
- 标注信息缺失的类别

**二、利基定位分析**
- 使用三环合一框架（新杠杆 × 边界变动 × 资源匹配）
- 产出 2-3 个候选利基（不要 3+1 模式，直出模式下给精炼结论）
- 每个利基附机会评分六维

**三、瓶颈诊断**
- 基于 OPC 经营健康度框架，识别当前最大瓶颈
- 明确"最值得修正的一点"

**四、MVP 建议**
- 基于最优利基，给出具体的产品化建议（档位/定价/交付物）
- 明确验证假设和成功标准

**五、下一步行动**
- 按优先级排列 3-5 个具体行动项
- 每项附时间线和预期产出

### Step 3：落盘

将分析结果写入 `opc-doc/`（如果用户确认要落盘）：

```
opc-doc/outputs/XX-context-synthesis/
├── diagnosis-YYYYMMDD.md    # 完整诊断报告
└── action-plan-YYYYMMDD.md  # 行动计划
```

更新 `opc-doc/state/current-stage.json` 标记直出分析已完成。

## 与 opc-orchestrator 的关系

| 场景 | 使用哪个 |
|------|----------|
| 用户第一次接触 OPC，没有业务信息 | `opc-orchestrator` 交互模式 |
| 用户有明确业务但想系统梳理 | `opc-orchestrator` 引导模式 |
| 用户转发聊天/链接，要求 OPC 分析 | `opc-context-synthesis` 直出模式 |
| 用户已有丰富 memory + session 数据 | `opc-context-synthesis` 直出模式 |
| 直出分析后用户想深入某个阶段 | 切换到对应的 OPC 单阶段 skill |

## 核心原则

- **数据优先**：没有采集到足够上下文前，不产出结论
- **标注推测**：基于已有信息推断的部分，明确标注为"推测"而非"已确认"
- **精炼输出**：直出模式不搞 3+1 选项仪式感，直接给最优结论+理由
- **可回退**：如果直出后发现某个阶段信息不足，建议回到交互模式补充

## 越界检测

- 如果 memory/session 中几乎没有业务信息 → 退回 `opc-orchestrator`
- 如果用户只是问了一个简单问题而不是要完整诊断 → 不要过度展开
- 如果用户提供的内容跟 OPC 无关（纯技术问题等）→ 不适用此 skill
