---
title: "Hugo + GitHub Pages 搭建记录"
date: 2026-06-12T11:00:00+08:00
draft: false
tags: ["hugo", "blog", "github-pages"]
categories: ["技术"]
description: "把整个从零搭建博客的过程记一下，方便以后自己回顾，也给想搭博客的人一个参考。"
---

## 选型

为什么选 Hugo + GitHub Pages：

- **完全免费**。GitHub Pages 静态托管免费，Hugo 本身开源。
- **内容即文件**。所有文章都是 `.md` 文件，丢在 `content/posts/` 下，用 Git 管理。
- **构建快**。Hugo 用 Go 写的，几千篇文章也能秒级生成。
- **部署简单**。push 代码就自动触发 Actions 构建并发布。

## 目录结构

```
myblog/
├── hugo.toml          # 站点配置
├── content/           # 文章
│   ├── about.md
│   └── posts/
├── themes/PaperMod/   # 主题
├── static/            # 静态资源（图片、favicon）
└── .github/workflows/ # Actions 部署配置
```

## 常用命令

```bash
# 本地预览（带草稿）
hugo server -D

# 本地预览（正式）
hugo server

# 构建静态文件到 public/
hugo
```

## 部署流程

每次改完内容，`git push` 到 GitHub，Actions 自动：

1. 拉代码
2. 安装 Hugo
3. 执行 `hugo` 构建
4. 把 `public/` 部署到 GitHub Pages

## 几个小坑

1. **PaperMod 需要 Hugo extended 版本**。`hugo version` 后面带 `extended` 字样才是。
2. **baseURL 一定要写对**。本地写 `http://localhost:1313/`，部署前改成你自己的域名，不然 RSS 和 sitemap 会出问题。
3. **中文文章的换行**。Hugo 默认按空格分词，中文一句话会变成一长行。在 `hugo.toml` 里加 `hasCJKLanguage = true` 就行。

---

整个流程跑下来大概半天，剩下就是写内容了。
