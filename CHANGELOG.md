# CHANGELOG

## [2025-12-31T15:05:00+08:00] - 优化系统提示词结构
- **任务名称:** 提示词分类与聚合
- **关键改动点:**
    - 将 `full_prompt_v2.md` 中的散乱提示词按语义分类（沟通风格、执行策略、资源访问、上下文优化、格式约定）。
    - 使用语义化标签包裹分类内容。
- **涉及文件:** `prompts/system_prompt/full_prompt_v2.md`
- **验证方式:** 检查文件内容结构，确认符合语义化分类要求。

## [2025-12-31T15:10:00+08:00] - 精简服务器资产定义
- **任务名称:** 远程资产描述优化
- **关键改动点:** 将服务器1的描述精简为基础的 IP 和用户定义。
- **涉及文件:** prompts/system_prompt/full_prompt_v2.md
- **验证方式:** 检查文件内容确认描述已精简。

## [2025-12-31T15:15:00+08:00] - 合并上下文优化提示词
- **任务名称:** 提示词逻辑聚合
- **关键改动点:** 将目录忽略、文件过滤和逻辑聚焦合并为单一的「核心逻辑聚焦」条目。
- **涉及文件:** prompts/system_prompt/full_prompt_v2.md
- **验证方式:** 检查文件确认三项已合并为一项。

## [2025-12-31T15:20:00+08:00] - 限定列表转换触发条件
- **任务名称:** 格式化规范优化
- **关键改动点:** 将罗马数字列表转换规则限定为仅在处理 LaTeX 论文文本时生效。
- **涉及文件:** prompts/system_prompt/full_prompt_v2.md
- **验证方式:** 检查文件确认已添加场景限定。

## [2025-12-31T14:15:39+08:00] - 生成 full_prompt_v4.md（模块合并）
- **任务名称:** 系统提示词模块合并输出
- **关键改动点:**
    - 新增 `prompts/system_prompt/full_prompt_v4.md`，将 v2 的模块合并为 5 个顶层模块（core/tooling/workflow/principles/hooks）。
    - 新增 `prompts/system_prompt/CLAUDE.md`，补齐目录级架构说明与变更记录。
- **涉及文件:** `prompts/system_prompt/full_prompt_v4.md`, `prompts/system_prompt/CLAUDE.md`, `CHANGELOG.md`
- **验证方式:** 通过 `rg -n \"^<[^/].*>$\" prompts/system_prompt/full_prompt_v4.md` 检查顶层标签完整性。

## [2025-12-31T14:23:40+08:00] - 统一 full_prompt_v4 列表编号
- **任务名称:** 提示词列表格式统一
- **关键改动点:** 修正「元规则」编号跳跃；统一「坏味道清单」编号格式（`1.` 风格）
- **涉及文件:** `prompts/system_prompt/full_prompt_v4.md`
- **验证方式:** `rg -n \"^15\\.|^16\\.|^17\\.|^\\s*\\d+\\)\" prompts/system_prompt/full_prompt_v4.md` 无输出

## [2025-12-31T14:32:43+08:00] - 调整工具使用规则排序
- **任务名称:** 工具规则排序优化
- **关键改动点:** 将「工具使用规则」按约束优先级（工具边界→参数/环境→执行方式→失败与求助）重排并重新编号
- **涉及文件:** `prompts/system_prompt/full_prompt_v4.md`
- **验证方式:** 人工检查 `工具使用规则` 段落编号与顺序

## [2025-12-31T11:45:00+08:00] - 强化系统提示词的 DoD 约束
- **任务名称:** 系统提示词自审计增强
- **关键改动点:**
    - 在 `full_prompt_v4.md` 中新增 `<definition_of_done>` 模块。
    - 明确「规约自检」为任务完成的阻塞级条件。
    - 引入「自我审计流程」，强制 AI 在输出结论前检查日志追加状态。
- **涉及文件:** `prompts/system_prompt/full_prompt_v4.md`, `CHANGELOG.md`
- **验证方式:** 检查文件确认 DoD 模块已正确插入。

## [2025-12-31T11:20:00+08:00] - 重构提示词体系并同步远程
- **任务名称:** 提示词库重构与同步
- **关键改动点:**
    - 移除 `prompts/collected/` 下的大量旧提示词文件。
    - 新增核心技能文件：`prompts/skills/Canvas.md`, `prompts/skills/ReadProgram.txt` 等。
    - 升级系统提示词：新增 `full_prompt_v3.md` 和 `full_prompt_v4.md`。
    - 提交所有更改并推送到 GitHub。
- **涉及文件:** `prompts/`, `CHANGELOG.md`
- **验证方式:** `git status` 确认无遗留更改，`git push` 成功。

## [2025-12-31T11:28:00+08:00] - 配置 .gitignore 忽略 vibe-coding-cn
- **任务名称:** 库忽略配置
- **关键改动点:**
    - 创建根目录 `.gitignore` 文件。
    - 添加 `vibe-coding-cn/` 到忽略列表。
    - 添加通用忽略项（.DS_Store, 编辑器配置, 临时日志等）。
    - 提交并推送到 GitHub。
- **涉及文件:** `.gitignore`
- **验证方式:** `git status` 确认 `vibe-coding-cn/` 已被忽略。

## [2025-12-31T14:33:21+08:00] - 工具使用规则编号从 1 开始
- **任务名称:** 工具规则编号修正
- **关键改动点:** 将「工具使用规则」编号由 `6-14` 改为 `1-9`
- **涉及文件:** `prompts/system_prompt/full_prompt_v4.md`
- **验证方式:** 人工检查 `工具使用规则` 段落编号连续性
