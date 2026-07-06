# 组件提取：从设计中识别可重用组件 (Component Extract: Identify Reusable Components from a Design)

遍历设计并识别隐藏在其中的可重用组件。输出一个组件清单，用户可以将其提取为真实的组件库或设计系统。当用户有一个完整的页面或流程，并想“使之系统化”、“构建一个组件库”，或交接一组结构化的部件时，请使用此技能。

**页面是组件的排列组合。** 一个没有被识别出组件的设计，只是一堆一次性产物。提取组件才能使设计变得可维护。

## 阶段 1：确定范围 (Phase 1: Identify the surface)

确定要遍历的内容：

- 单个高保真设计文件
- 多页面的流程
- 包含设计的整个项目

阅读所有相关文件。在脑海中建立正在使用的视觉词汇模型。

## 阶段 2：遍历设计并清点 (Phase 2: Walk the design and inventory)

逐块遍历设计界面。对于每个视觉元素，问自己：

1. **这个完全相同的模式是否出现过不止一次？**（三个页面上相同的按钮 → 候选组件。）
2. **这个模式是否合理地可能出现在其他地方？**（即使现在只有一个地方有，以后可能重复吗？例如：一种卡片样式、一个表单输入框、一个页眉。）
3. **它有变体吗？**（按钮有主要的、次要的、幽灵等变体。卡片有带图和不带图的变体。）
4. **它有状态吗？**（悬停 hover、激活 active、禁用 disabled、聚焦 focus、加载 loading。）

如果对任何一个问题的回答是“是”，它就是一个候选组件。

将发现的内容归入标准的组件类别中：

### 基础 (Foundational)

- **颜色令牌 (Color tokens)** — 品牌色、语义色、中性色
- **间距令牌 (Spacing tokens)** — 使用的间距比例尺
- **排版令牌 (Type tokens)** — 字体族、大小、字重、行高
- **圆角令牌 (Radius tokens)** — 圆角半径比例尺
- **阴影令牌 (Shadow tokens)** — 悬浮高度（elevation）比例尺
- **动效令牌 (Motion tokens)** — 过渡持续时间和缓动曲线

（有关令牌级别的详细信息，请参阅 `design-system-extract`。此技能建立在它的基础之上。）

### 原子 (Atoms)

- **按钮 (Button)** — 变体（主要、次要、幽灵、破坏性）；大小；带/不带图标；状态
- **输入框 (Input)** — 文本、邮箱、密码、数字、搜索；带/不带标签；带/不带错误提示
- **复选框 / 单选按钮 / 开关 (Checkbox / radio / toggle)**
- **选择器 / 下拉框 (Select / dropdown)**
- **标签 / 碎片 / 徽章 (Tag / chip / badge)**
- **头像 (Avatar)**
- **图标 (Icon)** — 图标大小列表和正在使用的图标集
- **链接 (Link)** — 内联链接、独立链接

### 分子 (Molecules)

- **表单字段 (Form field)** — 标签 + 输入框 + 提示信息 + 错误提示
- **卡片 (Card)** — 变体（带图像、带页脚、极简）；状态（悬停、被选中）
- **吐司提示 / 警告 (Toast / alert)** — 变体（信息、成功、警告、错误）
- **模态框 / 对话框 (Modal / dialog)**
- **下拉菜单 (Dropdown menu)**
- **工具提示 (Tooltip)**
- **分页控件 (Pagination control)**

### 组织 (Organisms)

- **页眉 / 导航栏 (Header / nav bar)**
- **页脚 (Footer)**
- **侧边导航栏 (Sidebar nav)**
- **标签组 (Tab group)**
- **表格 / 数据网格 (Table / data grid)**
- **表单 (Form)** （字段的组合 + 提交 + 验证模式）
- **首屏展示区 (Hero section)**
- **功能网格 (Feature grid)**
- **空状态 (Empty state)**

### 模板 / 页面级 (Templates / page-level)

- 落地页模板 (Landing page template)
- 详情页模板 (Detail page template)
- 列表/索引页模板 (List/index template)
- 空状态页面 (Empty state page)

## 阶段 3：记录每个组件 (Phase 3: For each component, document)

对于你识别出的每个组件，记录下：

- **名称** — 简短、约定俗成、祈使名词（例如：`Button`、`EmptyState`、`FormField`）
- **用途** — 用一句话描述何时使用它
- **变体 (Variants)** — 命名的视觉或行为上的变化
- **大小 (Sizes)** — 如果存在大小变体
- **状态 (States)** — 默认 (default)、悬停 (hover)、激活 (active)、聚焦 (focus)、禁用 (disabled)、加载中 (loading)（适用哪些写哪些）
- **使用的令牌 (Tokens used)** — 它引用了哪些颜色、间距、排版令牌
- **组合方式 (Composition)** — 它是用哪些其他组件构建的（例如：`Card` 使用了 `Button`）
- **无障碍说明 (Accessibility notes)** — 键盘支持、ARIA、对比度考量
- **建议 / 禁忌 (Do / Don't)** — 至少一条简短的建议和一条禁忌（例如：“不要把两个主要按钮堆放在一行”）

以结构化文档的形式排版 —— 一份组件清单，用户可以将其交给开发人员，或者以此为基础构建组件库。

## 阶段 4：识别缺漏 (Phase 4: Identify the gaps)

在遍历时，你会发现：

- **不一致之处 (Inconsistencies)** — 有三个稍微不同的按钮样式，而其实一个就够了。标记它们并推荐一个规范的版本。
- **缺失的状态 (Missing states)** — 有些组件有 hover 状态，但没有 focus 状态或 disabled 状态。标记这些缺失。
- **缺失的变体 (Missing variants)** — 用户可能合理需要但尚不存在的组件（例如，在有删除操作的设计中需要破坏性的按钮变体，却只有主要按钮）。
- **非规范值 (Off-scale values)** — 使用的间距或尺寸超出了已建立令牌比例尺的组件。标记并进行对齐（snap）。

这些缺漏也是交付物的一部分 —— 它们是将设计转变为真实系统所需的工作。

## 阶段 5：输出清单 (Phase 5: Emit the inventory)

将清单写入文件（例如 `component-inventory.md`），每个组件占一个部分，结构如上所述。如果用户希望将这些组件构建成实际的代码，在后续跟进构建工作 —— 但清单文件是此技能的主要输出。

为了提供视觉参考，可以选择生成一个“组件库”页面来渲染带有其变体和状态的各个组件。如果想要网格布局，请使用 `design_canvas.jsx` 启动模板。

## 阶段 6：建议后续步骤 (Phase 6: Recommend next steps)

在清单之后，建议：

- **提取令牌** (`design-system-extract`)（如果尚未提取）
- **构建组件库代码** 如果用户希望将其作为真实产出
- 对每个组件进行 **`精修通道 (Polish-pass)`**，确保它们在原子层面经得起推敲
- 对组件库应用 **`使之可调 (Make tweakable)`** 技能，以便用户可以实时调整系统

## 阶段 7：总结 (Phase 7: Summarize)

汇报：

- 清点出的组件数量（按类别分类 —— 原子 / 分子 / 组织）
- 标记出的不一致之处和缺失
- 输出文件的路径
- 建议的后续步骤
