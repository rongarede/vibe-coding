<canvas_driven_development>
  
<core_principle>
Canvas白板 = 人机协作的单一真相源  
- 代码是白板的序列化形式  
- 架构变更必先体现在白板  
- AI通过读取Canvas JSON理解项目全貌
</core_principle>

<canvas_structure>
Canvas文件结构：  
- nodes: 系统组件的可视化节点（模块、服务、数据库）  
- edges: 组件间的依赖关系与数据流向  
- 节点属性: id, type, text, x, y, width, height, color  
- 边属性: id, fromNode, toNode, fromSide, toSide, label

Canvas文件生成规则
1. 默认路径：`{项目根目录}/architecture.canvas`
2. 备用路径（如根目录不可写）：`{用户主目录}/architecture_{项目名}.canvas`
3. 文件编码：UTF-8（无 BOM）
4. 格式化：JSON 缩进 2 空格，最后一行留空行

AI解析规则：  
- 节点text字段 = 组件的职责说明 + 关键类/函数  
- 边的方向 = 调用关系或数据流向  
- 节点颜色 = 组件角色分类（入口/业务/存储/外部服务）  
- 节点坐标 = 架构层级（Y轴表示调用层次）
</canvas_structure>

<collaboration_workflow>
人类操作白板 → AI理解意图 → 生成/修改代码

场景1：新增功能  
1. 人类在白板拖入新节点（如 [NotificationService]）  
2. 人类连线到相关模块（[UserService] → [NotificationService] → [EmailAPI]）  
3. 人类提供白板给AI："按这个架构实现通知功能"  
4. AI读取nodes和edges，理解：  
   - 需要创建NotificationService类  
   - 需要从UserService调用  
   - 需要集成EmailAPI  
5. AI生成完整代码，包括import、接口定义、调用链

场景2：重构架构  
1. 人类在白板拖动/删除/重组节点  
2. 人类调整连线关系  
3. 人类提供新白板给AI："按新架构重构"  
4. AI对比新旧Canvas结构：  
   - 识别被删除的节点 → 移除相关代码  
   - 识别新增的边 → 添加调用关系  
   - 识别移动的节点 → 调整模块边界  
5. AI输出重构计划 + 自动执行

场景3：理解遗留项目  
1. AI自动扫描项目生成Canvas白板  
2. 人类通过白板快速理解架构全貌  
3. 人类点击节点查看详细说明  
4. 人类在白板上标注待优化部分  
5. AI根据标注提供重构建议
</collaboration_workflow>

<canvas_generation_protocol>
自动生成Canvas的触发条件：  
- 用户明确要求"生成架构图"  
- 项目结构发生重大变更（新增/删除超过3个模块）  
- 代码审查前（确保架构可视化）

生成流程：  
1. 扫描项目文件树，识别所有源代码文件  
2. 解析import语句，构建依赖图  
3. 检测数据库操作、API调用、文件IO  
4. 根据目录结构和命名规则分类组件  
5. 智能布局节点（按架构层级自动计算坐标）  
6. 生成Canvas JSON并写入 `architecture.canvas`

输出规范：  
- 文件名：项目根目录下 `architecture.canvas`  
- 节点命名：`{组件类型}_{文件名}` 如 `service_payment`  
- 边命名：`edge_{源}_{目标}` 如 `edge_user_payment`  
- 颜色编码：  
  * "1"红 = 入口文件、主程序  
  * "2"橙 = 工具类、公共库  
  * "3"黄 = 业务逻辑层  
  * "4"绿 = 外部服务  
  * "5"青 = 数据存储  
  * "6"紫 = 前端/UI层
</canvas_generation_protocol>

<canvas_update_protocol>
同步策略：双向实时更新  

代码变更 → Canvas更新：  
- 新增文件 → 自动添加节点  
- 新增import → 自动添加连线  
- 删除文件 → 标记节点为灰色（保留历史）  
- 修改依赖 → 更新边的连接关系

Canvas变更 → 代码更新：  
- 新增节点 → 生成对应文件模板  
- 新增边 → 添加import和调用代码  
- 删除节点 → 提示删除文件（需确认）  
- 移动节点 → 调整目录结构（可选）

触发时机：  
- 每次git commit前自动检查Canvas与代码一致性  
- AI检测到不一致时主动询问："Canvas与代码不同步，是否更新？"
</canvas_update_protocol>

<ai_canvas_reading_protocol>
AI接收Canvas文件的处理流程：  

Step 1：解析JSON结构  
```python
canvas_data = json.loads(canvas_content)
nodes = canvas_data["nodes"]  # 所有组件
edges = canvas_data["edges"]  # 所有依赖关系
```

Step 2：构建心智模型  
- 从nodes提取：组件名称、职责描述、关键API  
- 从edges提取：调用链路、数据流向  
- 根据Y坐标推断：架构层级（上层调用下层）  
- 根据颜色推断：组件角色（入口/业务/存储）

Step 3：验证理解  
AI应主动确认：  
"我理解的架构是：  
- 入口层：{列出所有红色节点}  
- 业务层：{列出所有黄色节点}  
- 存储层：{列出所有青色节点}  
- 关键调用链：{A → B → C}  
这样理解对吗？"

Step 4：基于Canvas执行任务  
- 新增功能：找到相关节点，生成符合架构的代码  
- 重构代码：遵循Canvas定义的模块边界  
- 修复Bug：沿着edges追踪可能的影响范围  
- 代码审查：检查实际调用是否符合Canvas设计
</ai_canvas_reading_protocol>

<canvas_editing_protocol>
人类编辑Canvas的最佳实践：  

节点编辑：  
- 双击节点进入编辑模式  
- text格式：`**{模块名}**\n{路径}\n\n{职责描述}\n\n包含：\n- {关键类}\n- {关键函数}`  
- 颜色选择：根据组件角色选择对应颜色  
- 位置调整：Y轴表示调用层级，X轴表示同层内的逻辑分组

边的编辑：  
- 连线方向：从调用方指向被调用方  
- 添加label：标注调用类型（同步/异步/数据流）  
- 删除边：移除不必要的依赖关系  
- fromSide/toSide：选择视觉上最清晰的连接点

架构调整原则：  
- 保持层级清晰：上层不应连到更上层  
- 避免循环依赖：检查是否有环形调用  
- 模块内聚：同一职责的节点靠近放置  
- 接口简洁：一个节点连接数不超过5条
</canvas_editing_protocol>

<documentation_sync_protocol>
Canvas与文档的强制同步：  

每次架构调整后必须更新：  
1. `architecture.canvas` - 可视化架构图（主文档）  
2. `ARCHITECTURE.md` - 架构决策记录（ADR格式）  
   - 为什么这样设计  
   - 考虑过哪些替代方案  
   - 当前设计的权衡  
3. `CHANGELOG.md` - 架构演进日志  
   - 本次调整了哪些节点/边  
   - 影响范围  
   - 迁移指南（如有）

同步检查点：  
- git commit时：检查Canvas与代码一致性  
- PR review时：要求附上Canvas变更对比  
- Sprint结束时：导出Canvas历史版本存档

格式要求：  
- 每个节点的text必须包含"职责一句话"  
- 每条边必须能回答"为什么需要这个依赖"  
- 颜色使用必须符合编码规范  
- 坐标调整必须保持逻辑层次清晰
</documentation_sync_protocol>

<quality_control_protocol>
Canvas质量标准：  

结构完整性：  
- 所有代码文件都有对应节点（孤立文件 < 5%）  
- 所有import都有对应边（遗漏依赖 = 0）  
- 节点分层合理（3-7层为宜）  
- 边密度适中（每节点平均2-4条边）

可读性：  
- 节点大小适中（width=250-300, height自适应）  
- 文字清晰简洁（每个节点 < 150字）  
- 颜色使用一致（同类组件同颜色）  
- 布局整齐（同层Y坐标相近，X轴等间距）

准确性：  
- 节点描述与实际代码一致  
- 边的方向正确反映调用关系  
- 颜色编码符合组件角色  
- 坐标位置反映真实架构层次

维护性：  
- 重大变更有注释（在节点text中标注版本）  
- 历史版本可追溯（git管理.canvas文件）  
- 定期清理过时节点（标记为灰色或删除）  
- 复杂区域有子图拆分（如微服务拆分多个Canvas）
</quality_control_protocol>

<advanced_patterns>
高级协作模式：  

模式1：渐进式重构  
- 在Canvas上用不同颜色标注：绿=已重构，黄=进行中，红=待重构  
- AI按颜色优先级生成重构计划  
- 每次commit更新节点颜色

模式2：多人协作  
- Canvas作为团队共享架构图  
- 每人负责的模块用专属颜色标记  
- 新增功能前在Canvas上"占位"避免冲突

模式3：版本演进  
- 为每个大版本保存Canvas快照  
- 对比不同版本Canvas：git diff architecture.canvas  
- 生成架构演进动画（可选工具）

模式4：AI自主优化  
- 定期让AI分析Canvas："这个架构有什么问题？"  
- AI建议：循环依赖、单点故障、性能瓶颈  
- 人类决策是否采纳，AI执行重构

模式5：跨项目复用  
- 建立Canvas模板库（Web后端/微服务/数据管道）  
- 新项目直接导入模板Canvas  
- AI根据模板生成项目脚手架
</advanced_patterns>

<emergency_protocol>
Canvas丢失或损坏的应急方案：  

预防措施：  
- Canvas文件纳入git版本控制  
- 每周自动备份到云端  
- 重要节点手动导出JSON备份

恢复流程：  
1. 尝试从git历史恢复  
2. 若git无记录，触发AI重新生成：  
   "紧急重建Canvas，扫描当前代码生成架构图"  
3. AI在30秒内生成基础Canvas  
4. 人类补充关键设计决策和注释  
5. 标记为"重建版本"并记录原因

降级方案：  
- 若Canvas完全不可用，AI切换到传统模式（基于代码理解）  
- 提示人类："Canvas不可用，建议尽快重建以恢复最佳协作效率"  
- 生成临时的文本版架构树（Markdown格式）作为过渡
</emergency_protocol>

<principles>
Canvas驱动开发的核心原则：  

1. Canvas First：架构变更先改Canvas，代码跟随  
2. 单一真相源：Canvas = 唯一权威架构文档  
3. 实时同步：代码与Canvas必须保持一致  
4. 人机共享：Canvas既是给人看的图，也是给AI读的数据  
5. 渐进演进：Canvas随项目成长持续更新，永不过时  
6. 可视优先：用图形表达的永远比文字清晰  
7. 零翻译成本：人类编辑Canvas = 直接指挥AI  
8. 架构透明：任何人打开Canvas立刻理解系统全貌


AI与人类的Canvas协作规范：  

语言策略：  
- Canvas节点text：中文描述职责，英文标注类名/函数名  
- 边的label：中文说明调用目的（如"获取用户信息"）  
- AI输出：中文解释架构理解，英文生成代码

沟通流程：  
1. 人类提供Canvas + 任务描述  
2. AI先用中文确认理解：  
   "我看到架构是这样的：{简述}，我将{任务}，是否正确？"  
3. 人类确认或纠正  
4. AI执行任务并更新Canvas（如需要）  
5. AI用中文总结变更："已完成{任务}，Canvas已同步更新"

冲突处理：  
- 若Canvas与代码不一致，AI优先信任Canvas  
- 若发现Canvas设计有问题，AI提出但不擅自修改  
- 若任务超出Canvas定义范围，AI先建议扩展Canvas

错误处理：  
- Canvas JSON格式错误：提示具体错误位置  
- 节点引用不存在：列出可用节点供选择  
- 循环依赖检测：可视化显示依赖环  
- 层级混乱：提供自动布局建议
</principles>

</canvas_driven_development>