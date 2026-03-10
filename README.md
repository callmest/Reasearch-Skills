# Research-Skills

让agent记住你的实验过程 - Claude Code研究记忆管理技能集

## 📦 包含的Skills

### 1. research-memory

一个全功能的研究项目记忆管理系统，支持：

- ✅ **自动检测和记录**：被动触发，激进捕获研究活动
- ✅ **结构化组织**：5个子目录（ideas/experiments/results/decisions/resources）
- ✅ **强制链条追踪**：想法→实验→结果必须关联
- ✅ **Session捕获**：从当前对话历史中提取研究活动
- ✅ **对话式记录**："帮我记录..." / "帮我总结...并记录"
- ✅ **源文件追踪**：完整的数据文件溯源和智能恢复
- ✅ **渐进式披露**：只加载相关记忆，避免上下文溢出

**安装**:
```bash
claude skill install research-memory.skill
```

**快速开始**:
```
/research-memory init "my-project" "Project goal description"
```

详细文档见：[research-memory/README.md](research-memory/README.md)

## 🎯 使用场景

这个技能集适用于：

- 🔬 **科研项目**：追踪实验、记录结果、管理文献
- 💡 **技术探索**：记录想法、验证方案、决策历史
- 📊 **数据分析**：关联数据文件、追踪分析过程
- 📝 **论文写作**：组织研究材料、追溯实验来源

## 📚 文档结构

```
Reasearch-Skills/
├── README.md                    # 本文件
├── research-memory.skill        # 打包好的skill文件
└── research-memory/             # 源文件目录
    ├── README.md                # 详细使用文档
    ├── SKILL.md                 # 完整skill定义
    ├── IMPROVEMENTS.md          # 改进历史
    └── FINAL_SUMMARY.md         # 功能总结
```

## 🚀 快速示例

```
# 1. 初始化项目
/research-memory init "protein-pocket-detection" "Develop DL model for pocket identification"

# 2. 自动记录（只需正常对话）
用户: "我想用Transformer架构"
Agent: 💡 Recorded: Transformer architecture idea (idea_transformer_001)

# 3. 对话式记录
用户: "帮我总结这篇论文并记录"
Agent: 📚 Recorded: Paper summary (resource_paper_001)

# 4. 查看记忆
/research-memory recent 2h
/research-memory report summary
```

## 🤝 贡献

欢迎提交新的research-related skills！

## 📄 许可

MIT License
