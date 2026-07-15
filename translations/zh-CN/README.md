# Claude Design 系统提示词：简体中文版

这里存放 `claude/` 版本的简体中文翻译。

当前译文对应英文原文 commit：[`3c3ddb0`](https://github.com/Trystan-SA/claude-design-system-prompt/commit/3c3ddb07d7aa3fef051d83608596470c95cfd8fe)。

## 文件

- [`claude/system-prompt.md`](./claude/system-prompt.md)：Claude 版本的系统提示词

## 翻译原则

- 保留英文版的章节顺序、规则强度、代码和具体数值。
- skill 名称、CSS 属性、HTML 元素和常用设计术语保留英文，避免翻译后无法对应代码或文件。
- 中文句子以清楚、可执行为准，不逐字硬译。容易产生歧义的表达，会直接写明它要求模型做什么。
- 这份译文不会加入文章式评论。原文没有给出的判断，不写进系统提示词。

## 使用

把 [`claude/system-prompt.md`](./claude/system-prompt.md) 的内容作为 system prompt 使用。它仍然假设模型在一个以 HTML 为主要输出形式、支持文件操作和 subagent 的环境中工作。

这个仓库来自第三方逆向整理，不是 Anthropic 发布的官方系统提示词。中文版只翻译仓库内容，不改变这一来源说明。
