# 设计系统提取：从源中提取设计令牌 (Design System Extract: Pull Tokens from Sources)

从品牌参考资料、代码库或屏幕截图中提取设计令牌（颜色、排版、间距、圆角、阴影），并输出结构化的令牌文件。当开始一项需要匹配现有视觉语言的设计工作时，请使用此技能。

令牌文件是系统化思维的基础。一旦有了令牌，未来的设计就会引用它们 —— 在保持系统一致性的同时，无需每次都向用户询问具体数值。

## 阶段 1：确定来源 (Phase 1: Identify sources)

确定从哪里提取。用户可能会提供：

- **一个代码库** —— 读取主题文件（`theme.ts`、`tokens.css`、`_variables.scss`、`tailwind.config.js`、设计系统源代码）。
- **一个在线网站或屏幕截图** —— 通过类似 DevTools 的检查工具从 CSS 中提取值，或仔细阅读屏幕截图。
- **一份品牌指南** —— PDF、Figma 文件或列出颜色、字体、间距的文档。
- **一个现有的设计系统项目** —— 你可以列出并阅读的 UI 套件。

如果用户没有具体说明，请询问。不要根据你自己的假设进行提取 —— 凭空发明的令牌违背了初衷。

## 阶段 2：按类别提取 (Phase 2: Extract by category)

遍历每个类别。对于每一个类别，从源中捕获具体的值 —— 绝不要猜测。

### 颜色 (Colors)

提取：
- **品牌主色 (Brand primary)**（及其深色/浅色变体，如果有定义）
- **品牌强调色 (Brand accent)**（及其变体）
- **语义颜色 (Semantic colors)** —— 成功、警告、错误、信息（及其浅色背景，如果有定义）
- **中性色阶 (Neutral scale)** —— 通常是从近乎白色到近乎黑色的 9-11 个阶梯，具有一致的色调（暖色 / 冷色 / 中性色）
- **表面颜色 (Surface colors)** —— 背景、前景、卡片、叠加层、边框

对于每种颜色，记录：
- 它的 hex（或 oklch）值
- 它在源中的名称
- 它的预期用途（源文档中说明的用途）

标记不一致之处 —— 多个略有不同的蓝色、不同色调的中性色 —— 作为发现报告给用户。不要默默地合并它们；不一致本身也是一种信息。

### 排版 (Typography)

提取：
- **字体族 (Font families)** —— 无衬线（sans）、衬线（serif）、等宽（mono）。包括完整的字体栈及回退字体。
- **字体大小 (Font sizes)** —— 实际使用的阶梯（`12 / 14 / 16 / 18 / 20 / 24 / 30 / 36 / 48 / 60` 很常见，但不是绝对的）
- **字重 (Font weights)** —— 实际加载了哪些字重（不要列出未部署的字重）
- **行高 (Line heights)** —— 至少包括：紧凑（约 1.1，用于标题）、正常（约 1.5，用于正文）、宽松（约 1.7，用于长文）
- **字间距 (Letter spacing)** —— 通常只对全大写标签有影响
- **文本样式 (Text styles)** —— 命名的组合（例如，"Heading 1"、"Body Large"、"Caption"），如果源中有定义的话

### 间距 (Spacing)

提取使用的间距比例尺。常见基数：4px 或 8px。比例尺通常从 0 到 64-128px。记录实际使用的比例尺，而不是通用的比例尺。

如果源文件对 插入 / 内联 / 块级 / 组件间 有单独的比例尺，把它们全部捕获。

### 圆角 (Radii)

提取使用的圆角半径值。通常有 3-5 个不同的圆角（`0`, `4`, `8`, `12`, `9999` 用于胶囊形）。

### 阴影 (Shadows)

提取阴影系统。通常有 3-5 个层级（从 `shadow-sm` 到 `shadow-2xl`）。捕获完整的 CSS 值（偏移、模糊、扩散、颜色、不透明度）。

### 其他令牌（如果存在）(Other tokens)

- **Z-index 层级** —— 模态框、下拉菜单、吐司提示、工具提示
- **动画令牌** —— 持续时间（`fast`, `normal`, `slow`）和缓动曲线
- **断点 (Breakpoints)** —— 如果系统是响应式的
- **容器宽度 (Container widths)** —— 内容的 max-width 值

## 阶段 3：输出令牌文件 (Phase 3: Emit the tokens file)

编写一个 `tokens.css`（或源语言使用的匹配格式：`tokens.ts`，`tokens.json` 等）。结构如下：

```css
:root {
  /* ---------- Colors ---------- */

  /* Brand */
  --color-primary:        #...;
  --color-primary-dark:   #...;
  --color-primary-light:  #...;
  --color-accent:         #...;

  /* Semantic */
  --color-success: #...;
  --color-warning: #...;
  --color-error:   #...;
  --color-info:    #...;

  /* Neutrals */
  --color-gray-50:  #...;
  --color-gray-100: #...;
  /* ... */
  --color-gray-900: #...;

  /* Surfaces */
  --color-bg:      #...;
  --color-surface: #...;
  --color-border:  #...;

  /* ---------- Typography ---------- */

  --font-sans:  "...", -apple-system, sans-serif;
  --font-serif: "...", serif;
  --font-mono:  "...", monospace;

  --text-xs:    12px;
  --text-sm:    14px;
  --text-base:  16px;
  --text-lg:    18px;
  --text-xl:    20px;
  --text-2xl:   24px;
  --text-3xl:   30px;
  --text-4xl:   36px;
  --text-5xl:   48px;

  --weight-regular:  400;
  --weight-medium:   500;
  --weight-semibold: 600;
  --weight-bold:     700;

  --leading-tight:  1.1;
  --leading-normal: 1.5;
  --leading-loose:  1.7;

  /* ---------- Spacing ---------- */

  --space-0:   0;
  --space-1:   4px;
  --space-2:   8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-5:  24px;
  --space-6:  32px;
  --space-7:  40px;
  --space-8:  48px;
  --space-10: 64px;

  /* ---------- Radii ---------- */

  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 9999px;

  /* ---------- Shadow ---------- */

  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);
}
```

适应源语言和命名约定。如果源使用 Tailwind，输出一个 `tailwind.config.js` 扩展。如果使用 TypeScript，输出带有类型导出的 `tokens.ts`。与项目的风格保持一致。

## 阶段 4：记录发现 (Phase 4: Document findings)

在输出令牌后，总结：

- **使用的来源** —— 代码库路径、屏幕截图、品牌指南
- **提取的类别** —— 找到了哪些令牌集
- **缺失 (Gaps)** —— 源未定义令牌的类别（例如，没有记录的阴影层级）。这些应由用户来做决定；不要默默填补它们。
- **不一致之处** —— 源文件中存在近似重复值或偏离比例尺异常值的地方。这些往往代表着值得整合的临时决策。
- **建议的后续步骤** —— 通常是：与用户一起审查令牌文件，然后在后续设计中使用它。

这项技能的输出是用户可以直接使用的一个令牌文件，外加一份清晰的报告，指出源设计系统存在哪些缺失或不一致的地方。
