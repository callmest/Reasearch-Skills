# Research Memory Skill

一个用于研究项目记忆管理的Claude Code skill，支持自动追踪研究进展、结构化组织记忆、源文件溯源等功能。

## 📦 安装

### 方法1：使用打包好的.skill文件

```bash
# 安装到Claude Code
claude skill install research-memory.skill
```

### 方法2：从源文件安装

```bash
# 复制到Claude skills目录
cp -r research-memory ~/.claude/skills/
```

## 🎯 核心功能

### 1. 自动检测和记录
- **被动触发**：自动检测想法、实验、结果、决策、资源
- **激进模式**：宁可过度记录，不遗漏信息
- **简短通知**：单行通知，不打断对话流

### 2. 结构化组织
- **5个子目录**：ideas, experiments, results, decisions, resources
- **渐进式披露**：只加载相关记忆
- **描述性命名**：`{type}_{keywords}_{id}.md`

### 3. 强制链条追踪
- **想法 → 实验 → 结果**：必须形成链条
- **自动询问**：结果没有实验时主动询问
- **关系图**：通过 `related` 字段建立连接

### 4. Session捕获
- **命令**：`/research-memory capture-session`
- **功能**：从当前对话历史中提取所有研究活动
- **场景**：中途开始使用skill时追溯之前的讨论

### 5. 对话式记录
- **触发**：
  - "帮我记录..."
  - "帮我总结...并记录"
  - "把...记录到research-memory"
- **功能**：agent帮助处理信息并记录

### 6. 源文件追踪
- **自动检测**：识别文件路径提及
- **主动询问**：结果没提供路径时询问
- **懒惰验证**：只在访问时验证
- **智能恢复**：文件缺失时搜索并提供匹配

## 📝 使用示例

### 初始化项目

```
/research-memory init "protein-pocket-detection" "Develop deep learning model for protein binding pocket identification"
```

### 自动记录（被动模式）

```
用户: "我想用Transformer架构处理3D蛋白质结构"
Agent: 💡 Recorded: Transformer for 3D structures (idea_transformer_3d_001)

用户: "我要在PDBbind数据集上测试BERT"
Agent: 🧪 Recorded: BERT on PDBbind (exp_bert_pdbbind_001)

用户: "实验完成，准确率85%，结果在 ./results/bert_exp.csv"
Agent: 📊 Recorded: 85% accuracy result (result_bert_85acc_001)
       📁 Source: ./results/bert_exp.csv
```

### 对话式记录

```
用户: "帮我总结这篇Attention论文并记录到resources"
Agent: [读取和总结论文]
       📚 Recorded: Attention Is All You Need (resource_attention_paper_001)
```

### Session捕获

```
[用户已经讨论了30分钟研究内容]

用户: "/research-memory capture-session my-project"
Agent: → Analyzing current session...
       → Found: 3 ideas, 2 experiments, 2 results, 1 decision
       → ✅ Created 8 memory files with proper linkage
```

### 查看记忆

```
/research-memory load "my-project"          # 加载项目上下文
/research-memory recent 2h                  # 查看最近2小时的记忆
/research-memory show result_bert_85acc_001 # 查看特定记忆
/research-memory search "transformer"       # 搜索记忆
```

### 源文件管理

```
/research-memory verify-sources result_bert_85acc_001  # 验证源文件
/research-memory show-sources result_bert_85acc_001    # 显示所有源文件
/research-memory update-source result_bert_85acc_001 "./old/path" "./new/path"  # 更新路径
```

## 📂 目录结构

```
memory/{project_name}/
├── project_root.md         # 项目根节点
├── outline.md              # 技术路线图
├── ideas/
│   ├── register.md         # 想法索引
│   └── idea_transformer_3d_001.md
├── experiments/
│   ├── register.md         # 实验索引
│   └── exp_bert_pdbbind_001.md
├── results/
│   ├── register.md         # 结果索引
│   └── result_bert_85acc_001.md (with source_files)
├── decisions/
│   ├── register.md         # 决策索引
│   └── decision_pytorch_001.md
└── resources/
    ├── register.md         # 资源索引
    └── resource_attention_paper_001.md
```

## 🔧 命令参考

### 初始化
- `/research-memory init "{project_name}" "{goal}"`

### 手动记录
- `/research-memory add-idea "{topic}" "{description}"`
- `/research-memory add-experiment "{name}" "{description}"`
- `/research-memory add-result "{topic}" "{findings}" [--source "{path}"]`
- `/research-memory add-decision "{point}" "{choice}" "{rationale}"`
- `/research-memory add-resource "{type}" "{path}" "{description}"`

### Session管理
- `/research-memory capture-session ["{project_name}"]`
- `/research-memory load "{project_name}"`

### 查看和搜索
- `/research-memory recent [1h|2h|6h|1d|3d|7d]`
- `/research-memory show {memory_id}`
- `/research-memory search "{keywords}"`
- `/research-memory list [ideas|experiments|results|decisions|resources]`

### 源文件管理
- `/research-memory add-source {memory_id} "{path}" ["{description}"]`
- `/research-memory verify-sources {memory_id}`
- `/research-memory update-source {memory_id} "{old_path}" "{new_path}"`
- `/research-memory show-sources {memory_id}`

### 更新和维护
- `/research-memory update {memory_id} "{content}"`
- `/research-memory link {memory_id_1} {memory_id_2}`
- `/research-memory status {memory_id} {new_status}`
- `/research-memory undo {memory_id}`

### 报告
- `/research-memory report [summary|detailed|timeline]`
- `/research-memory export "{output_path}"`

## 🎯 设计原则

1. **激进捕获，智能检索** - 宁可多记录，渐进式加载
2. **强制链条** - 想法→实验→结果必须关联
3. **一文件一主题** - 不混合内容，通过`related`连接
4. **懒惰验证** - 只在访问时验证文件存在性
5. **项目目录搜索** - 文件缺失时只搜索项目目录

## 📚 文档

- **SKILL.md** - 完整的skill文档（~1300行）
- **IMPROVEMENTS.md** - 第一次改进总结
- **FINAL_SUMMARY.md** - 最终版本完整总结

## 🤝 贡献

欢迎提交issue和PR来改进这个skill！

## 📄 许可

MIT License
