# OPC Skills

一套面向一人企业（One-Person Company, OPC）的工作流技能库，源自 Hermes Agent 的 `one-person-business` 技能家族。

涵盖资源盘点、利基定位、价值主张、商业模式、MVP 设计、转化闭环、经营复盘等完整阶段。适合自用学习、团队分享、二次开发。

[![license][license-badge]][license-url]

---

## 目录

- [核心组成](#核心组成)
- [快速开始](#快速开始)
- [目录结构](#目录结构)
- [工作流时序](#工作流时序)
- [开发与部署](#开发与部署)
- [贡献与许可](#贡献与许可)

---

## 核心组成

### `opc-*` 技能 — 一人企业工作流主链

| 技能 | 阶段 | 一句话说明 |
|---|---|---|
| `opc-orchestrator` | 总编排 | 自动路由与阶段跳转控制 |
| `opc-resource-audit` | 01 资源盘点 | 8 类资源全面扫描与成熟度评分 |
| `opc-niche-positioning` | 02 利基定位 | 三重环筛选与定位声明生成 |
| `opc-value-proposition` | 03 价值主张 | 客户痛点与价值主张提炼 |
| `opc-business-model-design` | 04 商业模式 | 画布设计 + 定价与收款路径 |
| `opc-mvp-designer` | 06 MVP 设计 | 最小可行产品与验证实验规划 |
| `opc-conversion-loop` | 07 转化闭环 | 获客-转化-交付闭环设计 |
| `opc-dashboard-review` | 09 经营复盘 | 指标看板与周度/月度复盘模板 |
| `opc-asset-ops` | 08 资产沉淀 | 知识资产化与可复用的资产库 |
| `opc-context-synthesis` | 综合 | 阶段性上下文摘要与上下文压缩 |

### `me-*` 技能 — 个人运营与自我管理

| 技能 | 作用 |
|---|---|
| `me-processize` | 关键流程 SOP 化与可复制性检查 |
| `me-first-customers` | 种子客户的获取与筛选策略 |
| `me-pricing` | 价值定价法、价格锚定与价格测试 |
| `me-marketing-plan` | 营销计划的三段式结构搭建 |
| `me-grow-sustainably` | 优先顺序判断与健康增长模型 |
| `me-minimalist-review` | 极简复盘与一二三四法则 |
| `me-validate-idea` | 假设验证与最小化测试设计 |

---

## 快速开始

### 直接克隆使用

```bash
git clone https://github.com/liaosong0187765-maker/opc-skills.git
cd opc-skills
```

### 安装到 Hermes / Codex

```bash
# 一次性安装全部 17 个技能
npx skills add . --yes
```

或单独安装某个技能：

```bash
# 进入技能目录后安装
cd opc-orchestrator
npx skills add .
```

> 注：`npx skills add` 支持本地目录作为技能源。把本仓库的任意子目录作为 source 传入即可。

---

## 目录结构

```text
opc-skills/
├── README.md                   # 本文件
├── LICENSE                     # MIT 许可
├── DESCRIPTION.md              # 技能家族概述
├── opc-orchestrator/           # 总编排与路由
├── opc-resource-audit/         # 资源盘点
├── opc-niche-positioning/      # 利基定位
├── opc-value-proposition/      # 价值主张
├── opc-business-model-design/  # 商业模式
├── opc-mvp-designer/           # MVP 设计
├── opc-conversion-loop/        # 转化闭环
├── opc-dashboard-review/       # 经营复盘
├── opc-asset-ops/              # 资产沉淀
├── opc-context-synthesis/      # 上下文综合
├── me-processize/              # 流程化
├── me-first-customers/         # 首客获取
├── me-pricing/                 # 定价策略
├── me-marketing-plan/          # 营销规划
├── me-grow-sustainably/        # 健康增长
├── me-minimalist-review/       # 极简复盘
└── me-validate-idea/           # 想法验证
```

> 提示：每个技能目录中：`SKILL.md` 为技能定义，`agents/` 为各模型的专用提示，`references/` 为方法论模板与参考文件。

---

## 工作流时序

推荐执行顺序（由 `opc-orchestrator` 自动管理）：

```
opc-orchestrator
  → opc-resource-audit
  → opc-niche-positioning
  → opc-value-proposition
  → opc-business-model-design
  → opc-mvp-designer       (可选跳过)
  → opc-conversion-loop
  → opc-asset-ops
  → opc-dashboard-review   (周期循环)
```

也可以根据现况跳阶段（例如已有明确利基，可直接从 `opc-business-model-design` 开始）。

---

## 开发与部署

### 本地调试

```bash
# 进入某个技能目录，使用 hermes 执行
cd opc-diagnosis
hermes --skill . --prompt "我的问题是..."
```

### 输出约定

多数 `opc-*` 技能会将结果写入项目工作目录下的 `opc-doc/` 子目录，结构示例：

```text
opc-doc/
├── outputs/
│   ├── 01-resource-audit/
│   │   ├── inventory.md
│   │   └── scorecard.json
│   ├── 02-niche-positioning/
│   │   ├── three-ring-analysis.md
│   │   └── positioning-statement.md
│   └── ...
├── state/
│   ├── current-stage.json
│   └── decisions.json
└── reviews/
    └── dashboard.json
```

---

## 贡献与许可

本仓库为镜像与解放出，技能版权归原作者与 Hermes 生态所有。

- License：MIT（代码/配置骨架） + 知识内容遵循 Hermes Skill Sharing 协议
- Issues：用于报告技能使用问题与改进建议
- PRs：欢迎提交 typo、文档优化、新的 `me-*`  companion 技能

---

## 相关链接

- Hermes Agent 项目主页：https://github.com/NousResearch/hermes
- Skills 文档中心：https://hermes-agent.nousresearch.com/docs/skills
- OPC 方法论 Wiki：`~/wiki/docs/topics/one-person-business/`

---

<!-- Badges -->
[license-badge]: https://img.shields.io/github/license/liaosong0187765-maker/opc-skills
[license-url]: https://github.com/liaosong0187765-maker/opc-skills/blob/main/LICENSE
