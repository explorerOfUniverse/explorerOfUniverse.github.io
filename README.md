# 个人博客

基于 **Hugo + PaperMod + GitHub Pages** 的个人博客，免费、自动部署。

## 本地开发

需要先装 [Hugo Extended](https://gohugo.io/installation/)（`>= 0.146.0`）。

```bash
# 拉取主题子模块
git submodule update --init --recursive

# 本地预览（含草稿）
hugo server -D
# 浏览器打开 http://localhost:1313
```

发新文章：

```bash
hugo new content posts/my-new-post.md
```

## 发布

```bash
git add .
git commit -m "新文章标题"
git push origin main
```

push 之后 GitHub Actions 会自动构建并发布到 GitHub Pages。

## 第一次部署到 GitHub Pages

**情况 A：用 `username.github.io` 域名（推荐入门）**

1. 在 GitHub 上建一个 **public** 仓库，名字必须是 `username.github.io`（把 `username` 换成你的 GitHub 用户名）
2. 把这个项目代码 push 上去：
   ```bash
   git remote add origin git@github.com:username/username.github.io.git
   git branch -M main
   git push -u origin main
   ```
3. 进仓库 **Settings → Pages**，Source 选 **GitHub Actions**（不是 `Deploy from a branch`）
4. 等 1-2 分钟，访问 `https://username.github.io` 就能看到

**情况 B：用自己的域名（比如 `example.com`）**

1. 先去域名注册商（阿里云 / Cloudflare / Namecheap 等）买一个域名
2. 在 GitHub 仓库 **Settings → Pages → Custom domain** 填上域名
3. 在域名注册商那边加 DNS 记录：
   - `www` 子域名：CNAME 指向 `username.github.io`
   - 根域名：用 A 记录指向 GitHub Pages 的 IP（4 个）：
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
4. 等 DNS 生效（5 分钟到几小时不等），勾选 **Enforce HTTPS**
5. 改 `hugo.toml` 里的 `baseURL` 为 `https://example.com/`，push 后就生效了

## 目录结构

```
.
├── content/
│   ├── about.md             # 关于页
│   ├── archives.md          # 归档页
│   └── posts/               # 博客文章
│       ├── hello-world.md
│       └── hugo-github-pages.md
├── themes/PaperMod/         # 主题（submodule）
├── static/                  # 静态资源（头像、favicon 等）
├── .github/workflows/       # GitHub Actions 部署
├── hugo.toml                # 站点配置
└── README.md
```

## 改主题配置

编辑 `hugo.toml` 里的 `params` 块，常见项：

- `params.profileMode` — 首页 Profile 模式（头像 + 简介 + 按钮）
- `params.socialIcons` — 社交链接
- `params.ShowReadingTime` — 是否显示阅读时长
- `hasCJKLanguage` — 写中文的话改成 `true`

主题文档：[PaperMod Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki)

## 头像图片

把头像放到 `static/images/avatar.png`，`hugo.toml` 里已经默认引用这个路径。

## 添加评论 / 统计

- 评论：[Giscus](https://giscus.app/)（基于 GitHub Discussions，免费）
- 访问统计：[Umami](https://umami.is/) 或 [Cloudflare Analytics](https://www.cloudflare.com/web-analytics/)（都免费、不写 cookie）

PaperMod 都内置了对应配置项，按官方文档填上 ID 即可。
