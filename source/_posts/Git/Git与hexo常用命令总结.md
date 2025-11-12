---
title: Git与hexo常用命令总结
tags:
  - 软件工具
  - Git
  - 使用教程
categories: 技术笔记
abbrlink: 4218731647
date: 2025-11-12 17:36:31
---
下面分别列出 Git 和 Hexo 的常用命令：

## Git 常用命令

### 基础操作
```bash
# 初始化仓库
git init

# 克隆远程仓库
git clone <repository-url>

# 查看状态
git status

# 添加文件到暂存区
git add <filename>        # 添加特定文件
git add .                 # 添加所有文件

# 提交更改
git commit -m "提交信息"
```

### 分支管理
```bash
# 查看分支
git branch                # 本地分支
git branch -a             # 所有分支（包括远程）

# 创建分支
git branch <branch-name>

# 切换分支
git checkout <branch-name>
git checkout -b <new-branch>  # 创建并切换分支

# 合并分支
git merge <branch-name>

# 删除分支
git branch -d <branch-name>
```

### 远程操作
```bash
# 添加远程仓库
git remote add origin <repository-url>

# 推送到远程
git push origin <branch-name>
git push -u origin main   # 首次推送并设置上游分支

# 拉取更新
git pull origin <branch-name>

# 获取远程信息
git fetch origin
```

### 查看历史
```bash
# 查看提交历史
git log
git log --oneline         # 简洁格式
git log --graph           # 图形化显示

# 查看文件差异
git diff
```

## Hexo 常用命令

### 基础命令
```bash
# 初始化博客
hexo init <folder-name>

# 安装依赖
npm install

# 生成静态文件
hexo generate    # 或 hexo g

# 启动本地服务器
hexo server      # 或 hexo s
hexo s -p 4001   # 指定端口

# 部署到服务器
hexo deploy      # 或 hexo d

# 清理缓存和生成文件
hexo clean
```

### 内容管理
```bash
# 创建新文章
hexo new "文章标题"
hexo new post "文章标题"

# 创建页面
hexo new page "about"

# 创建草稿
hexo new draft "草稿标题"

# 发布草稿
hexo publish draft "草稿标题"
```

### 组合命令
```bash
# 生成并部署
hexo g -d

# 生成并启动服务器
hexo g && hexo s

# 清理后重新生成
hexo clean && hexo g
```

### 其他实用命令
```bash
# 列出所有文章
hexo list post

# 列出所有页面
hexo list page

# 显示Hexo版本
hexo version
```

## 常用工作流程

### Git + Hexo 典型工作流
```bash
# 1. 创建新文章
hexo new "新文章标题"

# 2. 编写内容后生成
hexo g

# 3. 本地预览
hexo s

# 4. 提交到Git
git add .
git commit -m "添加新文章"
git push origin main

# 5. 部署到服务器
hexo deploy
```

这些命令涵盖了日常使用 Git 和 Hexo 的大部分场景，建议根据实际需求灵活组合使用。