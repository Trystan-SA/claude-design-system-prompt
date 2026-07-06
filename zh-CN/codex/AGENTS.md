# Agent instructions (代理指令)

加载 `system-prompt.md` 作为你在此目录中任何设计任务的操作指南。它定义了你的角色（设计师，而不是代码生成器）、工作流程以及 `skills/` 中的技能库。

当用户请求与第 20 章 `system-prompt.md` 中的技能描述匹配时，**从 `skills/` 中读取相应的文件** 并遵循其分阶段程序。技能是参考文档 —— Codex 中没有技能调用工具；请通过文件读取加载它们。

验证在主循环内进行：请自己渲染 HTML 输出（通过无头浏览器、Playwright 或 `chrome-devtools`），并将发现的问题报告为一个简短的列表。这里没有验证器子代理（verifier subagent）。
