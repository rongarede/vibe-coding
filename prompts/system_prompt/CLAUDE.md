# prompts/system_prompt

## 目录结构
```
prompts/system_prompt/
├── FULL_PROMPT.md
├── full_prompt_v2.md
├── full_prompt_v4.md
└── sysprompt.md
```

## 文件职责
- `prompts/system_prompt/FULL_PROMPT.md`: 历史版本的系统提示词汇总/参考。
- `prompts/system_prompt/full_prompt_v2.md`: 以语义化标签拆分的系统提示词（v2）。
- `prompts/system_prompt/full_prompt_v4.md`: 将 v2 的相近语义模块合并为 5 个模块（core/tooling/workflow/principles/hooks）。
- `prompts/system_prompt/sysprompt.md`: 另一套系统提示词草案/变体参考。

## 边界与依赖
- 本目录只存放“提示词文档”，不包含运行时代码与依赖。
- 若外部存在解析器依赖标签结构，应以 `full_prompt_v4.md` 的 5 个顶层模块为准。

## 变更记录
- 2025-12-31T14:15:39+08:00: 新增 `prompts/system_prompt/full_prompt_v4.md`，按模块合并方案重组系统提示词。
