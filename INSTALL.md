# 安装指南

## 方法1：使用打包好的.skill文件（推荐）

### 步骤1：安装skill

```bash
cd /home/tanxu02/mnt/tanxu02/taoshen/project/Reasearch-Skills
claude skill install research-memory.skill
```

### 步骤2：验证安装

```bash
claude skill list | grep research-memory
```

应该看到：
```
research-memory - Research memory management system...
```

### 步骤3：开始使用

在任何Claude Code会话中：
```
/research-memory init "my-first-project" "My research goal"
```

## 方法2：从源文件手动安装

### 步骤1：复制到Claude skills目录

```bash
cp -r research-memory ~/.claude/skills/
```

### 步骤2：重启Claude Code

```bash
# 如果Claude Code正在运行，重启以加载新skill
```

### 步骤3：验证安装

```bash
claude skill list | grep research-memory
```

## 方法3：临时使用（不安装）

如果只想临时测试，可以直接解压.skill文件：

```bash
# .skill文件本质上是一个tar.gz压缩包
tar -xzf research-memory.skill -C /tmp/
cd /tmp/research-memory
cat SKILL.md  # 查看完整文档
```

## 卸载

如果需要卸载skill：

```bash
claude skill uninstall research-memory
```

或手动删除：

```bash
rm -rf ~/.claude/skills/research-memory
```

## 更新

如果有新版本的skill：

```bash
# 先卸载旧版本
claude skill uninstall research-memory

# 再安装新版本
claude skill install research-memory.skill
```

## 故障排除

### 问题1：skill未显示在列表中

**解决方案**：
1. 检查skill文件是否损坏：`tar -tzf research-memory.skill`
2. 重启Claude Code
3. 检查Claude Code版本是否支持skills

### 问题2：skill触发不正常

**解决方案**：
1. 检查description是否正确加载：`claude skill info research-memory`
2. 尝试显式调用：`/research-memory init "test" "test"`
3. 查看Claude Code日志

### 问题3：权限问题

**解决方案**：
```bash
chmod +x research-memory.skill
chmod -R 755 ~/.claude/skills/research-memory
```

## 验证安装成功

运行以下命令测试skill是否正常工作：

```bash
# 在Claude Code中
/research-memory init "test-project" "This is a test"
```

应该看到：
```
✅ Initialized project: test-project
📂 Created directory structure
📝 Created project_root.md and outline.md
```

## 获取帮助

- 查看完整文档：`research-memory/README.md`
- 查看skill定义：`research-memory/SKILL.md`
- 查看功能总结：`research-memory/FINAL_SUMMARY.md`
