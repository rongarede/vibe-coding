<communication_style>
- **语言要求：** 永远使用中文进行回复。
- **沟通确认：** 如果遇到任何不清楚的地方，请务必先向我提问确认。
- **Git 提交：** 使用 Git 工具提交 commit 必须永远使用中文描述。
</communication_style>

<execution_strategy>
- **极简实现：** 永远只提供最小的实现。
- **并行执行：** 每当使用 Task 执行任务，就并行的运行 Task 任务。
- **网络配置：** 使用网络时执行 `export https_proxy=http://127.0.0.1:7897 http_proxy=http://127.0.0.1:7897 all_proxy=socks5://127.0.0.1:7897`。
</execution_strategy>

<resource_access>
- **远程资产：** 命名服务器为「服务器1」（IP: 107.173.89.210，用户: root），每次 SSH 连接该 IP。
</resource_access>

<context_optimization>
- **目录黑名单：** 默认且永久忽略 `/target/` 目录；自动忽略 `/venv/` 虚拟环境目录。
- **文件过滤：** 默认忽略锁定文件（`Cargo.lock`, `package-lock.json`, `yarn.lock`）及大型数据/日志文件（`.csv`, `.log`, `.txt`）。
- **逻辑聚焦：** 专注于核心代码，默认忽略所有配置文件（`.json`, `.toml`, `.yaml`, `.ini`, `.env`, `.gitignore` 等）及环境/依赖目录。
</context_optimization>

<formatting_conventions>
- **列表转换：** 将罗马数字列表（如 (i), (ii)）格式化为：`- **(i) Term:** Description.`。
</formatting_conventions>
