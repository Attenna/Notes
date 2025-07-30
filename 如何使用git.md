# 🚀 Git 多端同步完全指南

> 📚 适用于代码项目、Obsidian笔记、学习资料等多种文件类型的版本控制与同步

---

## 📖 目录

- [🔧 Git 基础设置](#-git-基础设置)
- [📤 推送工作流程](#-推送工作流程)
- [📥 拉取与同步](#-拉取与同步)
- [🔄 多端协作流程](#-多端协作流程)
- [⚠️ 冲突处理](#️-冲突处理)
- [🎯 常用命令速查](#-常用命令速查)
- [📋 最佳实践](#-最佳实践)
- [🛠️ 进阶技巧](#️-进阶技巧)
- [❓ 常见问题解答](#-常见问题解答)

---

## 🔧 Git 基础设置

### 首次配置 Git

```bash
# 设置用户信息（全局配置）
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"

# 查看配置
git config --list
```

### 初始化仓库

```bash
# 方式1：从零开始
git init
git remote add origin https://github.com/username/repository.git

# 方式2：克隆现有仓库
git clone https://github.com/username/repository.git
cd repository
```

### 配置 .gitignore

对于不同项目类型，创建合适的 `.gitignore` 文件：

```bash
# Obsidian 项目
.obsidian/workspace.json
.obsidian/cache/
.trash/

# 通用忽略
*.tmp
*.log
.DS_Store
Thumbs.db
```

---

## 📤 推送工作流程

### 💡 标准推送流程

每次修改文件后的完整流程：

```bash
# 1️⃣ 查看文件状态
git status

# 2️⃣ 暂存修改的文件
git add .                    # 添加所有修改
# 或
git add filename.md          # 添加特定文件
git add folder/              # 添加整个文件夹

# 3️⃣ 提交更改
git commit -m "feat: 添加新的学习笔记"

# 4️⃣ 推送到远程仓库
git push origin main
```

### 📝 提交信息规范

使用清晰的提交信息格式：

```bash
# 功能新增
git commit -m "feat: 添加数据结构与算法笔记"

# 修复问题
git commit -m "fix: 修正数学公式格式错误"

# 文档更新
git commit -m "docs: 更新README使用说明"

# 样式调整
git commit -m "style: 优化Markdown格式"

# 重构代码
git commit -m "refactor: 重新组织文件夹结构"
```

---

## 📥 拉取与同步

### 🆕 首次设置新设备

```bash
# 1. 克隆仓库到本地
git clone https://github.com/username/repository.git
cd repository

# 2. 验证远程连接
git remote -v
```

### 🔄 日常同步操作

```bash
# 开始工作前，先拉取最新版本
git pull origin main

# 如果有本地修改冲突，使用变基合并
git pull --rebase origin main
```

### 📱 移动设备同步

对于移动端 Git 客户端（如 Working Copy）：

1. **下载更新**：点击 Pull 按钮
2. **上传修改**：Stage → Commit → Push

---

## 🔄 多端协作流程

### 💻 设备A（主要工作设备）

```bash
# 工作开始
git pull origin main

# 进行修改...
# 编辑文件、添加笔记等

# 提交并推送
git add .
git commit -m "更新：完成第3章学习笔记"
git push origin main
```

### 📱 设备B（辅助设备）

```bash
# 获取设备A的最新修改
git pull origin main

# 进行补充修改...
# 添加新想法、修正错误等

# 提交并推送
git add .
git commit -m "补充：添加重要概念解释"
git push origin main
```

### 🖥️ 设备C（另一台电脑）

```bash
# 保持同步
git pull origin main

# 查看最新更改
git log --oneline -5
git show HEAD  # 查看最新提交的详细内容
```

---

## ⚠️ 冲突处理

### 🚨 推送冲突的解决

当出现冲突时：

```bash
# 1. 先拉取远程更改
git pull origin main

# 2. 如果有冲突，Git会标记冲突文件
# 手动编辑冲突文件，解决标记如下的冲突：
# <<<<<<< HEAD
# 你的修改
# =======
# 远程的修改
# >>>>>>> commit-hash

# 3. 解决冲突后，标记为已解决
git add 冲突文件名.md

# 4. 完成合并提交
git commit -m "解决冲突：合并学习笔记更新"

# 5. 推送解决后的版本
git push origin main
```

### 🔧 避免冲突的策略

```bash
# 使用变基而非合并，保持历史整洁
git pull --rebase origin main

# 提交前检查状态
git status
git diff HEAD~1  # 查看与上次提交的差异
```

---

## 🎯 常用命令速查

### 📊 状态查看

```bash
git status              # 查看工作区状态
git log --oneline       # 查看提交历史（简洁）
git log --graph         # 查看分支图
git diff                # 查看工作区修改
git diff --staged       # 查看暂存区修改
git show HEAD           # 查看最新提交内容
```

### 🔄 版本控制

```bash
git reset HEAD~1        # 撤销最近一次提交（保留修改）
git reset --hard HEAD~1 # 撤销最近一次提交（丢弃修改）
git checkout -- file.md # 撤销文件的工作区修改
git restore file.md     # 新版本撤销命令
```

### 🌿 分支操作

```bash
git branch              # 查看本地分支
git branch -a           # 查看所有分支
git checkout -b feature # 创建并切换到新分支
git merge feature       # 合并分支
git branch -d feature   # 删除已合并分支
```

### 🔍 搜索与查找

```bash
git log --grep="关键词"  # 在提交信息中搜索
git log -S "代码片段"    # 在代码变更中搜索
git blame file.md       # 查看文件每行的修改历史
```

---

## 📋 最佳实践

### ✅ 推荐做法

1. **🔄 工作前先同步**

   ```bash
   git pull origin main
   ```

2. **📝 频繁提交，明确信息**

   ```bash
   # 好的提交
   git commit -m "feat: 添加线性代数第2章笔记"
   
   # 避免的提交
   git commit -m "修改"
   ```

3. **🗂️ 合理组织文件结构**

   ```text
   📁 课程笔记/
   ├── 📁 数学/
   ├── 📁 计算机科学/
   └── 📁 物理/
   📁 项目代码/
   📁 资源文件/
   ```

4. **⚡ 使用快捷命令组合**

   ```bash
   # 创建别名提高效率
   git config --global alias.ac "!git add . && git commit -m"
   git config --global alias.ps "push origin main"
   
   # 使用：
   git ac "更新笔记"
   git ps
   ```

### ❌ 避免的做法

- 🚫 长时间不同步就推送
- 🚫 提交信息不清楚："fix", "update"
- 🚫 提交临时文件或敏感信息
- 🚫 强制推送（除非必要）：`git push --force`

---

## 🛠️ 进阶技巧

### 🏃‍♂️ 快速工作流

创建快捷脚本 `sync.sh`：

```bash
#!/bin/bash
echo "🔄 拉取最新更改..."
git pull origin main

echo "📁 添加所有修改..."
git add .

echo "💬 请输入提交信息："
read commit_message
git commit -m "$commit_message"

echo "📤 推送到远程仓库..."
git push origin main

echo "✅ 同步完成！"
```

### 📈 高级查看命令

```bash
# 图形化历史
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'

# 统计信息
git shortlog -sn            # 按作者统计提交数
git log --stat              # 查看每次提交的文件统计
git log --since="2 weeks ago" # 查看最近两周的提交
```

### 🔧 自定义配置

```bash
# 设置默认编辑器
git config --global core.editor "code --wait"

# 设置合并工具
git config --global merge.tool vimdiff

# 开启颜色显示
git config --global color.ui auto
```

---

## ❓ 常见问题解答

### Q1: 推送时提示"rejected"怎么办？

```bash
# 通常是远程有新提交，先拉取
git pull origin main
# 解决可能的冲突后再推送
git push origin main
```

### Q2: 误删文件如何恢复？

```bash
# 如果还没提交
git checkout HEAD -- 文件名.md

# 如果已经提交，从历史版本恢复
git log --oneline
git checkout commit-hash -- 文件名.md
```

### Q3: 如何删除远程仓库中的文件？

```bash
# 删除文件并提交
git rm 文件名.md
git commit -m "删除不需要的文件"
git push origin main

# 只从Git中删除，保留本地文件
git rm --cached 文件名.md
```

### Q4: 大文件如何处理？

```bash
# 使用Git LFS处理大文件
git lfs install
git lfs track "*.pdf"
git lfs track "*.mp4"
git add .gitattributes
```

### Q5: 如何查看某个文件的修改历史？

```bash
# 查看文件的提交历史
git log --follow -- 文件名.md

# 查看文件的详细修改
git log -p -- 文件名.md
```

### Q6: 如何回退到某个历史版本？

```bash
# 查看历史提交
git log --oneline

# 回退到指定版本（保留工作区修改）
git reset commit-hash

# 强制回退（丢弃所有修改）
git reset --hard commit-hash

# 创建新提交来撤销某次提交
git revert commit-hash
```

### Q7: 如何重命名文件并保留历史？

```bash
# Git会自动跟踪重命名
git mv 旧文件名.md 新文件名.md
git commit -m "重命名：更新文件名"
```

---

## 🎉 总结

掌握这套Git工作流程，你就能：

- ✅ 在多个设备间无缝同步文件
- ✅ 追踪所有修改历史
- ✅ 安全地协作和分享
- ✅ 永不丢失重要数据
- ✅ 高效管理项目版本

记住核心原则：**Pull → Edit → Add → Commit → Push** 🔄

### 🚀 快速上手清单

对于新手，按以下步骤开始：

1. ✅ 配置用户信息
2. ✅ 创建或克隆仓库
3. ✅ 设置 .gitignore
4. ✅ 熟悉基本四步流程
5. ✅ 学会处理冲突
6. ✅ 建立日常同步习惯

---

*📝 最后更新：2025年7月30日*  
*🔗 参考文档：[Git官方文档](https://git-scm.com/doc)*  
*📚 适用范围：Obsidian笔记、代码项目、学习资料等*
