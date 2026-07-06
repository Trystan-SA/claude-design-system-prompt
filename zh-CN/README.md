> 🌏 **中文翻译版** | [English original](../README.md)

# Claude 设计系统提示词（Design System Prompt）

Anthropic Claude Design 的逆向工程系统提示词（System Prompt）。

一套系统提示词与技能（Skill）库，能将 LLM 转变为具有明确设计主张、无障碍性（Accessibility）意识、抵抗 AI 套路化产出（AI Slop）的设计协作者。

开源项目，MIT licensed。将提示词放入任何支持系统提示词的 LLM（Claude、GPT、Gemini、本地模型）中，按需搭配流程化技能使用。

## 这是什么

大多数"设计助手"提示词产出的是千篇一律的 SaaS 模板 —— 激进的渐变、emoji 装饰、圆角加左边框的卡片、清一色的 Inter 字体。本提示词明确拒绝这些模式，并以完整的设计哲学取而代之，涵盖：

- 内容纪律（无填充 —— 每个元素都必须证明自己的存在价值）
- 审美纪律（避免 AI 套路，坚持统一的配色与调性）
- 视觉层级（Visual Hierarchy）与节奏（大小、颜色、字重、位置、密度、间距比例）
- 无障碍性（WCAG、语义化 HTML、键盘导航、焦点环、动效偏好）
- 交互与反馈（hover、active、disabled、focus、loading、验证状态）
- 系统化思维（组件（Component）与设计令牌（Design Token）优先于一次性页面）
- 尊重媒介（真正的 CSS Grid、`oklch()`、`text-wrap: pretty`、真正的交互原型）
- 质量优于数量（深度优于广度，打磨每一个细节）

外加 14 个可供代理调用的流程化技能，用于生产、提取和审查工作。

## 包含内容

```
claude-design-system-prompt/
├── claude/                              Claude Code / Claude.ai 变体
│   ├── system-prompt.md                 主系统提示词 — 20 章
│   └── skills/                          14 个可调用技能
│       ├── discovery-questions.md       启动问题协议
│       ├── frontend-aesthetic-direction.md  在无品牌时确定视觉方向
│       ├── wireframe.md                 低保真探索，3+ 种变体
│       ├── make-a-deck.md               HTML 幻灯片演示
│       ├── make-a-prototype.md          可交互点击原型
│       ├── make-tweakable.md            浮动调参面板
│       ├── generate-variations.md       3+ 种高保真变体，沿多轴探索
│       ├── design-system-extract.md     从来源提取设计令牌
│       ├── component-extract.md         盘点可复用组件
│       ├── accessibility-audit.md       WCAG、语义化、键盘、动效审计
│       ├── ai-slop-check.md             渐变 / emoji / 字体 / 套路风格检测
│       ├── hierarchy-rhythm-review.md   大小 / 字重 / 颜色 + 间距比例审查
│       ├── interaction-states-pass.md   hover / active / disabled / focus / loading 审查
│       └── polish-pass.md              综合终审精修通道
├── codex/                               OpenAI Codex 变体（单循环，无子代理）
│   ├── AGENTS.md                        Codex 自动发现的入口文件
│   ├── system-prompt.md                 相同提示词，适配 Codex
│   └── skills/                          相同技能，串行审查替代并行代理
├── README.md                            本文件
└── LICENSE                              MIT
```

## 如何使用

### 直接使用系统提示词

将 `system-prompt.md` 的内容作为系统提示词粘贴到任何支持此功能的 LLM 中。代理将遵循设计哲学，并在任务匹配时按名称引用技能。

### 将技能作为流程使用

`skills/` 中的每个技能都是独立的、分阶段的流程。技能名即触发器 —— 当用户请求匹配技能描述时，代理加载该技能并按步骤执行。

技能分为三类：

**生产** —— 构建产出
`discovery-questions` · `frontend-aesthetic-direction` · `wireframe` · `make-a-deck` · `make-a-prototype` · `make-tweakable` · `generate-variations`

**系统** —— 提取结构
`design-system-extract` · `component-extract`

**审查** —— 审计与修复
`accessibility-audit` · `ai-slop-check` · `hierarchy-rhythm-review` · `interaction-states-pass` · `polish-pass`

技能可以链式组合。典型的从零开始流程：

```
discovery-questions → frontend-aesthetic-direction → wireframe → make-a-prototype → polish-pass
```

品牌驱动的流程：

```
design-system-extract → generate-variations → make-tweakable → polish-pass
```

### 适配你的平台

本提示词假设输出环境为 HTML（类似于 Claude.ai 的设计工具）。如果你的目标环境不同 —— Figma 插件、纯代码助手、纯对话设计顾问 —— 你需要调整工作流章节和工具引用。核心原则（第 5–16 章）适用于任何媒介。

## 模型校准

`claude/` 变体针对当前 Anthropic 前沿模型（Fable 5 及 Opus 4.7/4.8 系列）进行了校准，这些模型比早期版本更严格地遵循指令，所需的强制性提示更少：

- **条件而非配额。** 不使用"至少问 N 个问题"或"关键：你必须"。当前模型将配额视为字面合约并过度触发；提示词改为声明行动条件，辅以自主性条款（对次要决策自行选择合理选项并标注，而非反复询问）。
- **技能与子代理（Subagent）的显式触发。** 当前模型默认不会主动使用可选能力，因此每个技能描述都明确了*何时*调用，验证委派也有显式触发条件（"每次实质性视觉变更后"）。
- **覆盖优先的审查。** 审查代理报告所有发现并附带置信度/严重性评估，由聚合步骤进行过滤。当前模型对"仅报告重要问题"的指令过于字面化，会悄悄压制发现。
- **套路风格防护。** 当前模型的默认审美（奶油色背景、衬线展示字体、赤陶/琥珀色强调色）会被 `ai-slop-check`（规则 9）检测到，并被 `frontend-aesthetic-direction` 的四方向协议预先规避。这些模型已不再支持采样参数（`temperature`），因此视觉多样性必须来自显式的逐变体规格说明，而非随机性。

对于较旧的模型（Claude Opus/Sonnet 4.6 及更早版本，或非 Anthropic 模型），温和的措辞可能导致触发不足 —— 如果发现模型跳过提问环节或审查步骤，请恢复更强的祈使语气。`codex/` 变体独立维护，不受以上说明影响。

## 设计原则概览

`system-prompt.md` 中的 20 章涵盖：

| #   | 章节                                      |
| --- | ----------------------------------------- |
| 1   | 身份与角色                                 |
| 2   | 工作流                                     |
| 3   | 先提问                                     |
| 4   | 基于现有上下文进行设计                       |
| 5   | 内容原则 —— 无填充                          |
| 6   | 审美原则 —— 有目的的视觉表达                 |
| 7   | 视觉层级与节奏                              |
| 8   | 字体排印系统                                |
| 9   | 色彩系统                                    |
| 10  | 无障碍性与包容性                             |
| 11  | 交互与反馈                                  |
| 12  | 简洁性与唯一的行动号召（CTA）                 |
| 13  | 系统化思维                                  |
| 14  | 尊重媒介                                    |
| 15  | 理解用户                                    |
| 16  | 质量优于数量                                |
| 17  | 输出原则                                    |
| 18  | 协作与交付                                  |
| 19  | 知识产权与内容边界                           |
| 20  | 可用技能                                    |

## 参与贡献

欢迎提交 Issue 和 PR。以下贡献尤其有价值：

- 新增审查技能（如文案审查、动效审查、暗色模式一致性检查）
- 适配其他环境的提示词（Figma、纯代码、纯终端）
- 提示词应当防御的真实失败案例
- 将提示词翻译为其他语言

请保持同样的操作性语气，避免膨胀提示词 —— 每一章都必须证明自己的存在价值，这与提示词对代理本身的要求一致。

## 许可证

MIT —— 参见 `LICENSE`。

你可以出于任何目的使用、修改和分发本提示词及技能库，包括商业用途。无需署名，但我们感谢你的标注。
