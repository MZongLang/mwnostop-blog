# 博客写作、发布与界面更新指南

这份文档面向当前仓库 `Personal Blog`。这个博客是一个 Astro 静态站点，文章用 Markdown 写在仓库里，推送到 GitHub 后由 GitHub Actions 自动构建并发布到 GitHub Pages。

## 一、先认识项目结构

最常用的目录和文件如下：

```text
src/content/blog/          写博客文章的地方
src/content/config.ts      博客文章 frontmatter 字段规则
src/pages/index.astro      首页
src/pages/blog/index.astro 文章列表页
src/pages/blog/[slug].astro 单篇文章页
src/pages/about.astro      关于页
src/layouts/BaseLayout.astro 全站基础布局、导航、页脚、网页标题
src/styles/global.css      全站样式、首页动画样式
public/images/             图片资源
public/CNAME               自定义域名配置
astro.config.mjs           Astro 站点配置
.github/workflows/deploy.yml GitHub Pages 自动部署流程
dist/                      构建生成目录，不要手动写内容
```

日常写博客时，主要改 `src/content/blog/`。只有想改页面结构、导航、样式或首页时，才需要改 `src/pages/`、`src/layouts/` 和 `src/styles/`。

## 二、在哪里写新文章

每篇文章都是一个 Markdown 文件，放在：

```text
src/content/blog/
```

例如你要写一篇叫“我的第一篇项目复盘”的文章，可以新建：

```text
src/content/blog/my-first-project-review.md
```

文件名会变成文章网址的一部分。比如：

```text
src/content/blog/my-first-project-review.md
```

发布后访问路径就是：

```text
/blog/my-first-project-review/
```

建议文件名使用小写英文、数字和短横线，例如：

```text
how-i-built-my-blog.md
learning-astro-notes.md
2026-reading-notes.md
```

## 三、文章格式怎么写

每篇文章顶部必须有 frontmatter，也就是被 `---` 包起来的元信息。当前项目要求这些字段：

```markdown
---
title: "文章标题"
description: "文章摘要，会显示在文章列表和页面描述中。"
publishDate: "2026-06-25"
tags: ["notes", "project"]
---

这里开始写正文。

## 小标题

正文可以使用 Markdown：

- 列表
- **加粗**
- `代码`
- [链接](https://example.com)
```

字段说明：

| 字段 | 是否必填 | 用途 |
| --- | --- | --- |
| `title` | 必填 | 文章标题 |
| `description` | 必填 | 文章摘要，文章列表和 SEO 会使用 |
| `publishDate` | 必填 | 发布日期，文章列表按日期倒序排序 |
| `tags` | 可省略 | 标签数组，不写时默认为空数组 |

如果文章不显示或构建失败，优先检查 frontmatter 是否符合 `src/content/config.ts` 里的规则。

## 四、文章里怎么放图片

把图片放到：

```text
public/images/
```

例如放入：

```text
public/images/my-desk.png
```

文章里这样引用：

```markdown
![我的桌面](/images/my-desk.png)
```

注意路径以 `/images/` 开头，不需要写 `public`。

## 五、本地预览怎么打开

第一次打开项目，先安装依赖：

```powershell
npm install
```

日常写作时启动本地开发服务器：

```powershell
npm run dev
```

终端会显示本地地址，通常是：

```text
http://localhost:4321/
```

打开这个地址就能预览博客。修改 Markdown、页面或样式后，浏览器通常会自动刷新。

## 六、发布前怎么检查

发布前建议运行：

```powershell
npm run build
```

这个命令会先运行 Astro 检查，再构建静态站点。如果成功，会生成：

```text
dist/
```

`dist/` 是构建产物，不需要手动修改，也通常不需要手动上传。真正要提交的是你改过的源码文件，例如 `src/content/blog/*.md`、`src/pages/*.astro`、`src/styles/global.css` 或 `public/images/*`。

## 七、写完后怎么上传并发布

当前项目已经配置了 GitHub Pages 自动部署。流程是：

1. 本地写文章或改页面。
2. 运行 `npm run build` 确认没有错误。
3. 用 Git 提交改动。
4. 推送到 GitHub 的 `main` 或 `master` 分支。
5. GitHub Actions 自动构建并部署。

常用命令：

```powershell
git status
git add src/content/blog/my-first-project-review.md
git commit -m "Add project review post"
git push origin main
```

如果你还加了图片，也要一起添加：

```powershell
git add src/content/blog/my-first-project-review.md public/images/my-desk.png
git commit -m "Add project review post"
git push origin main
```

如果你在其他分支写作，可以先推送分支、开 Pull Request，合并到 `main` 后再部署：

```powershell
git push origin your-branch-name
```

仓库的部署配置在：

```text
.github/workflows/deploy.yml
```

它会在推送到 `main` 或 `master` 时运行：

```text
npm ci
npm run build
deploy to GitHub Pages
```

## 八、在哪里看部署结果

推送后，到 GitHub 仓库页面查看：

```text
Actions
```

找到最新的 `Deploy to GitHub Pages` 任务：

- 绿色成功：页面已经发布或正在刷新 CDN。
- 黄色运行中：等待构建完成。
- 红色失败：点进去看失败日志，通常是 Markdown frontmatter、TypeScript、依赖安装或构建错误。

当前项目配置的正式站点是：

```text
https://mwnostop.cn
```

域名相关配置在：

```text
astro.config.mjs
public/CNAME
```

## 九、如何更新首页、列表页和文章页

### 修改首页

首页文件是：

```text
src/pages/index.astro
```

可以改：

- 首页欢迎文字
- 首页进入动画后的介绍文案
- “查看文章”“关于我”按钮
- 最近文章区域的展示方式

首页背景图目前来自：

```text
public/images/welcome-sky.png
```

相关样式主要在：

```text
src/styles/global.css
```

搜索这些 class 会比较快：

```text
welcome-home
welcome-stage
welcome-word
blog-entry
latest-panel
```

### 修改文章列表页

文章列表页文件是：

```text
src/pages/blog/index.astro
```

它会读取 `src/content/blog/` 下所有文章，并按 `publishDate` 从新到旧排序。

可以改：

- 列表页标题和说明
- 每张文章卡片的结构
- 标签、日期、摘要的显示方式
- 空状态提示

### 修改单篇文章页

单篇文章页文件是：

```text
src/pages/blog/[slug].astro
```

可以改：

- 返回文章列表链接
- 文章标题区域
- 日期格式
- 标签位置
- 正文容器结构

### 修改关于页

关于页文件是：

```text
src/pages/about.astro
```

这里适合写：

- 个人介绍
- 正在做的项目
- 联系方式
- GitHub、社交平台或邮箱链接

### 修改导航、页脚和网页标题

全站基础布局是：

```text
src/layouts/BaseLayout.astro
```

可以改：

- 左上角站点名 `Personal Blog`
- 顶部导航链接
- 页脚文案
- 默认网页描述
- favicon 引用

### 修改颜色、字体、间距和动画

全站样式在：

```text
src/styles/global.css
```

常见入口：

```css
:root
.site-header
.site-footer
.post-card
.article
.prose
.home-page
.welcome-stage
.blog-entry
```

如果只是改颜色，优先改 `:root` 里的变量：

```css
--bg
--surface
--text
--muted
--line
--accent
--accent-strong
--accent-soft
--warm
```

## 十、如何新增文章字段

如果你想给文章增加新字段，比如 `draft`、`updatedDate`、`coverImage`，要先改：

```text
src/content/config.ts
```

例如新增封面图字段：

```ts
coverImage: z.string().optional()
```

然后文章可以这样写：

```markdown
---
title: "文章标题"
description: "文章摘要"
publishDate: "2026-06-25"
tags: ["notes"]
coverImage: "/images/cover.png"
---
```

最后再到 `src/pages/blog/index.astro` 或 `src/pages/blog/[slug].astro` 里把这个字段显示出来。

## 十一、常见问题

### 文章没有出现在列表里

检查：

- 文件是否放在 `src/content/blog/`
- 文件扩展名是否是 `.md`
- frontmatter 是否有 `title`、`description`、`publishDate`
- `publishDate` 日期格式是否正确
- `npm run build` 是否报错

### 图片显示不出来

检查：

- 图片是否放在 `public/images/`
- Markdown 路径是否写成 `/images/xxx.png`
- 文件名大小写是否一致

### 推送后网站没有更新

检查：

- 是否推送到了 `main` 或 `master`
- GitHub 仓库的 `Actions` 是否成功
- GitHub Pages 设置是否使用 `GitHub Actions` 作为 Source
- 浏览器是否缓存了旧页面，可以强制刷新

### 不知道应该提交哪些文件

先运行：

```powershell
git status
```

一般需要提交：

- 新文章：`src/content/blog/*.md`
- 新图片：`public/images/*`
- 页面改动：`src/pages/*`
- 布局改动：`src/layouts/*`
- 样式改动：`src/styles/global.css`
- 配置改动：`astro.config.mjs`、`public/CNAME`、`.github/workflows/deploy.yml`

一般不要手动提交：

- `dist/`
- `.astro/`
- `node_modules/`

## 十二、推荐的日常写作流程

```text
1. 在 src/content/blog/ 新建 Markdown 文件
2. 写 frontmatter：title、description、publishDate、tags
3. 写正文，图片放 public/images/
4. 运行 npm run dev 本地预览
5. 运行 npm run build 检查
6. git status 确认改动
7. git add 文章和相关资源
8. git commit
9. git push origin main
10. 到 GitHub Actions 查看部署结果
11. 打开 https://mwnostop.cn 确认线上页面
```

最重要的一句话：写文章主要去 `src/content/blog/`，改界面主要去 `src/pages/`、`src/layouts/` 和 `src/styles/global.css`，发布主要靠 `git push` 触发 GitHub Actions 自动部署。
