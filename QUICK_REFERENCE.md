# Research Memory - 快速参考

## 🚀 快速开始

```bash
# 1. 安装
claude skill install research-memory.skill

# 2. 初始化项目
/research-memory init "my-project" "Project goal"

# 3. 开始使用（自动记录）
# 只需正常对话，agent会自动检测和记录
```

## 💬 常用命令

### 项目管理
```
/research-memory init "project" "goal"     # 初始化
/research-memory load "project"            # 加载项目
/research-memory capture-session           # 捕获当前session
```

### 查看记忆
```
/research-memory recent 2h                 # 最近2小时
/research-memory show {memory_id}          # 查看详情
/research-memory search "keyword"          # 搜索
/research-memory list ideas                # 列出想法
```

### 手动记录
```
/research-memory add-idea "topic" "desc"
/research-memory add-experiment "name" "desc"
/research-memory add-result "topic" "findings" --source "path"
/research-memory add-decision "point" "choice" "why"
/research-memory add-resource "type" "path" "desc"
```

### 源文件管理
```
/research-memory verify-sources {memory_id}
/research-memory show-sources {memory_id}
/research-memory update-source {id} "old" "new"
```

### 报告
```
/research-memory report summary            # 摘要
/research-memory report detailed           # 详细
/research-memory report timeline           # 时间线
```

## 🎯 自动触发

Skill会在以下情况自动记录：

| 场景 | 触发词 | 记录类型 |
|------|--------|---------|
| 想法 | "我想...", "如果...", "或许..." | 💡 Ideas |
| 实验 | "我要测试...", "运行实验..." | 🧪 Experiments |
| 结果 | "准确率...", "结果显示..." | 📊 Results |
| 决策 | "我决定...", "我们选择..." | ✅ Decisions |
| 资源 | 论文链接, GitHub链接, 数据集 | 📚 Resources |

## 💬 对话式记录

```
"帮我记录一个想法：使用GNN"
→ 💡 Recorded: GNN idea

"帮我总结这篇论文并记录"
→ 📚 Recorded: Paper summary

"把这个实验记录到research-memory"
→ 🧪 Recorded: Experiment
```

## 📁 目录结构

```
memory/{project}/
├── project_root.md      # 项目概览
├── outline.md           # 技术路线
├── ideas/               # 💡 想法
├── experiments/         # 🧪 实验
├── results/             # 📊 结果
├── decisions/           # ✅ 决策
└── resources/           # 📚 资源
```

## 🔗 链条追踪

```
想法 → 实验 → 结果 → 决策
 💡     🧪     📊     ✅

每个结果必须关联实验
每个实验应该关联想法
```

## 📄 源文件追踪

```yaml
# 在result或resource中
source_files:
  - path: ./results/exp_001.csv
    type: csv
    description: Raw metrics
    last_verified: 2024-03-10
```

**特点**：
- 自动检测文件路径
- 主动询问（如果未提供）
- 懒惰验证（只在访问时）
- 智能恢复（文件移动后）

## 🎨 通知格式

```
💡 Recorded: Transformer idea (idea_transformer_001)
🧪 Recorded: BERT experiment (exp_bert_pdbbind_002)
📊 Recorded: 85% accuracy (result_bert_85acc_003)
📁 Source: ./results/exp_001.csv
✅ Recorded: Use PyTorch (decision_pytorch_004)
📚 Recorded: Attention paper (resource_paper_005)
📝 Updated: idea_transformer_001 with details
```

## ⚡ 快捷技巧

1. **批量记录**：使用 `capture-session` 追溯之前的讨论
2. **对话记录**：说"帮我记录..."让agent处理
3. **源文件**：提到文件路径时自动记录
4. **搜索**：用关键词快速找到相关记忆
5. **报告**：定期生成summary查看进展

## 🔧 故障排除

| 问题 | 解决方案 |
|------|---------|
| Skill未触发 | 尝试显式命令 `/research-memory` |
| 文件未找到 | 运行 `verify-sources` 更新路径 |
| 记忆太多 | 使用 `search` 或 `list` 过滤 |
| 误记录 | 使用 `undo {memory_id}` 删除 |

## 📚 完整文档

- **README.md** - 详细使用指南
- **SKILL.md** - 完整skill定义
- **FINAL_SUMMARY.md** - 功能总结
- **INSTALL.md** - 安装指南
