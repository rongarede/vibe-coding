# 💡 AI 提示词库 (Prompts)

`prompts/` 存放本仓库的提示词资产：用 **系统提示词** 约束 AI 的边界与品味，用 **任务提示词** 驱动「需求澄清 → 计划 → 执行 → 复盘」的开发流水线。

## 推荐使用路径（从 0 到可控）

1. **先定边界**：选择一个系统提示词版本（推荐 `v8` 或 `v10`）。
2. **再跑流程**：在具体任务里按阶段选用 `coding_prompts/`（澄清 / 计划 / 执行 / 复盘）。
3. **最后产品化**：当你在某领域反复做同类工作，把「提示词 + 资料」升级为 `skills/` 里的 Skill（更可复用、更稳定）。

## 目录结构（以仓库真实目录为准）

```
prompts/
├── README.md
├── coding_prompts/                 # 编程/研发提示词（当前 41 个 .md）
│   ├── index.md                    # 自动生成的索引与版本矩阵（请勿手改）
│   ├── 标准化流程.md
│   ├── 项目上下文文档生成.md
│   ├── 智能需求理解与研发导航引擎.md
│   └── ...
├── system_prompts/                 # 系统提示词（CLAUDE 多版本 + 其他收集）
│   ├── CLAUDE.md/                  # 1~10 版本目录（v9 目前仅占位）
│   │   ├── 1/CLAUDE.md
│   │   ├── 2/CLAUDE.md
│   │   ├── ...
│   │   ├── 9/AGENTS.md             # v9 当前没有 CLAUDE.md
│   │   └── 10/CLAUDE.md
│   └── ...
└── user_prompts/                   # 用户自用/一次性提示词
    ├── ASCII图生成.md
    ├── 数据管道.md
    └── 项目变量与工具统一维护.md
```

## `system_prompts/`：系统级提示词（先把 AI 变“可控”）

系统提示词用于定义 **工作模式、代码品味、输出格式、安全边界**。目录采用版本化结构：

- 路径约定：`prompts/system_prompts/CLAUDE.md/<版本号>/CLAUDE.md`
- 推荐版本：
  - `v8`：综合版，适合通用 Vibe Coding
  - `v10`：偏 Augment/上下文引擎的规范化约束
- 注意：`v9` 目录目前仅占位（无 `CLAUDE.md`）

## `coding_prompts/`：任务级提示词（把流程跑通）

`coding_prompts/` 面向「一次任务」：从需求澄清、计划拆解到交付与复盘。建议把它当作工作流脚本库：

- **入口级**（新会话/新项目必用）
  - `项目上下文文档生成.md`：固化上下文，降低跨会话漂移
  - `智能需求理解与研发导航引擎.md`：把模糊需求拆成可执行任务
- **交付级**（保证输出可审计）
  - `标准化流程.md`：把“先做什么、后做什么”写死，减少失控
  - `系统架构可视化生成Mermaid.md`：把架构输出成可视化（图胜千言）

### 关于 `index.md`（重要）

[`coding_prompts/index.md`](./coding_prompts/index.md) 是自动生成的索引（包含版本矩阵与跳转链接），**不要手工编辑**。如果你批量增删/调整版本，建议通过工具链生成索引再同步。

## `user_prompts/`：个人工作台（不追求体系化）

放一些个人习惯、临时脚手架提示词，原则是 **能用、别烂、别污染主库**。

## 快速使用（复制即用）

```bash
# 查看一个任务提示词
sed -n '1,160p' prompts/coding_prompts/标准化流程.md

# 选定系统提示词版本（建议先备份你当前的 CLAUDE.md）
cp prompts/system_prompts/CLAUDE.md/10/CLAUDE.md ./CLAUDE.md
```

## 维护与批量管理（可选）

如果你需要 Excel ↔ Markdown 的批量维护能力，仓库内置了第三方工具：`libs/external/prompts-library/`。建议把它视为“提示词资产的生产工具”，而把 `prompts/` 视为“日常开发的精选集”。

## 相关资源

- [`../skills/`](../skills/)：把高频领域能力沉淀为 Skills（更强复用）
- [`../documents/`](../documents/)：方法论与最佳实践（提示词设计与工作流原则）
- [`../libs/external/prompts-library/`](../libs/external/prompts-library/)：提示词 Excel ↔ Markdown 管理工具
