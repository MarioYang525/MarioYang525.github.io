# MarioYang525.github.io

Personal cybersecurity blog built with **Hugo**, deployed on **GitHub Pages**.
Dark minimal theme, all English.

Live site: <https://marioyang525.github.io/>

---

## 1. 首次发布（重要，只需做一次）

### 方式 A：GitHub 网页上传（无 Git 也能发）

1. 打开你的仓库 <https://github.com/MarioYang525/MarioYang525.github.io>
2. 点击 **Add file → Upload files**，把本文件夹里的**所有内容**（含 `.github` 隐藏文件夹）拖进去
   - Windows 资源管理器里看不到 `.github` 时：先在文件夹顶部勾选"显示 → 隐藏的项目"
   - 不能上传整个文件夹本身，要上传文件夹**里面的**所有文件
3. 点 **Commit changes**
4. 打开仓库 **Settings → Pages**，把 **Source** 改为 **GitHub Actions**（默认可能是 Branch/None，必须改）
5. 稍等 1~2 分钟，去 **Actions** 标签页看到绿色对勾后，访问 <https://marioyang525.github.io/> 即可

### 方式 B：Git 命令行

先安装 [Git for Windows](https://git-scm.com/download/win)，然后在仓库根目录执行：

```bash
git init
git add .
git commit -m "init: hugo site"
git branch -M main
git remote add origin https://github.com/MarioYang525/MarioYang525.github.io.git
git push -u origin main
```

同样记得去 **Settings → Pages** 把 Source 改成 **GitHub Actions**。

之后每次更新内容，只需：

```bash
git add .
git commit -m "post: 新文章说明"
git push
```

推送后 GitHub Actions 会自动构建并发布，约 1 分钟生效。

---

## 2. 目录结构

```text
MarioYang525.github.io/
├── hugo.toml                  # 站点配置（标题、导航、Welcome 文案）
├── content/                   # 所有文章内容
│   ├── _index.md
│   ├── about/_index.md        # About Me 页
│   ├── writeups/              # Writeups 板块
│   ├── ai-for-security/       # AI for Security 板块
│   ├── ctf/                   # CTF 板块
│   ├── pentest/               # Pentest 板块
│   └── projects/              # Projects 板块
├── themes/simple-dark/        # 自定义暗色主题（一般不用动）
├── .github/workflows/hugo.yml # 自动部署（push 后自动构建发布）
└── README.md
```

---

## 3. 如何填充内容

### 3.1 修改 Welcome 首页文字

编辑 `hugo.toml` 里的这两行：

```toml
welcomeTitle = "Welcome."
welcomeSubtitle = "A quiet place for CTF writeups, pentest notes and AI-driven security research."
```

### 3.2 修改站点标题 / 作者 / 页脚

同样在 `hugo.toml`：改 `title`、`params.author`、`params.footerText`。
导航菜单也在 `hugo.toml` 的 `[[menus.main]]` 部分。

### 3.3 修改 About Me

编辑 `content/about/_index.md`，把正文换成你的介绍（纯 Markdown）。

### 3.4 写新文章（以 Writeups 为例）

每个板块方法相同，只是目录不同（`writeups` / `ai-for-security` / `ctf` / `pentest` / `projects`）。

在对应板块下**新建一个文件夹**，里面放一个 `index.md`：

```text
content/writeups/my-new-writeup/
└── index.md
```

`index.md` 内容示例：

```markdown
---
title: "文章标题"
date: 2026-09-16
description: "一句话摘要，会显示在列表页"
---

正文用 Markdown 写，支持代码高亮：

​```bash
whoami
​```
```

> 注意：front matter（开头两横线之间）的 `title`、`date` 必填，`description` 可选。
> 文章只放 `index.md` 一个文件也完全可以，`files/` 文件夹按需创建。

### 3.5 上传附件文件（PDF / Markdown / 任意文件）

在文章文件夹里建一个 `files/` 子文件夹，把附件丢进去：

```text
content/writeups/my-new-writeup/
├── index.md
└── files/
    ├── report.pdf
    └── exploit.py
```

**所有放在 `files/` 里的文件会自动显示在文章页底部的 "Files" 区块**（带文件大小、可下载），不需要任何额外代码。

如果想在正文中间插入下载链接，使用 shortcode：

```markdown
完整报告见 {{</* attachment src="files/report.pdf" title="Report PDF" */>}}
```

图片也一样：放进 `files/` 后用 `![截图](files/screenshot.png)` 引用。

### 3.6 删除示例文章

把这两个文件夹删掉即可：

- `content/writeups/example-writeup/`
- `content/ctf/example-ctf-post/`

---

## 4. 本地预览（可选）

仓库作者已把 Hugo 下载到 `D:\Trae\Trae project\tools\hugo\hugo.exe`。
在仓库根目录运行：

```powershell
D:\Trae\Trae` project\tools\hugo\hugo.exe server
```

浏览器打开 <http://localhost:1313/> 实时预览，改动保存即刷新。按 `Ctrl+C` 停止。

> 如果提示 hugo 不是内部命令，用 `winget install Hugo.Hugo.Extended` 安装一份即可。

---

## 5. 常见问题

| 问题 | 解决 |
|------|------|
| push 后网站没更新 | 打开仓库 **Actions** 页看构建是否失败；确认 Settings → Pages 的 Source 是 **GitHub Actions** |
| 构建失败 | 多半是某篇文章 front matter 格式错误（少引号/少横线），看 Actions 里的红色报错行 |
| 文章不显示 | 确认文件名是 `index.md`（不是别的名字），且在正确的板块文件夹下 |
| 改了配置没生效 | 配置改动也要 push 才会发布；本地预览是即时生效的 |
