# Hexo + Butterfly 静态博客搭建全流程指南

本指南详细记录了从零开始搭建基于 **Hexo** 框架和 **Butterfly** 主题的静态博客的完整流程。

---

## 目录
1. [环境准备](#1-环境准备)
2. [安装 Hexo 框架](#2-安装-hexo-框架)
3. [初始化博客目录](#3-初始化博客目录)
4. [安装与配置 Butterfly 主题](#4-安装与配置-butterfly-主题)
5. [Hexo 基本命令与日常写作](#5-hexo-基本命令与日常写作)
6. [博客部署（以 GitHub Pages 为例）](#6-博客部署以-github-pages-为例)
7. [Butterfly 主题进阶配置推荐](#7-butterfly-主题进阶配置推荐)

---

## 1. 环境准备

在开始搭建之前，请确保电脑上已安装以下基础环境：

- **Node.js**（建议选择 LTS 长期支持版，版本需在 v14.0.0 以上）
  - 验证命令：`node -v` 和 `npm -v`
- **Git**（用于版本控制和部署博客至 GitHub 等平台）
  - 验证命令：`git --version`

---

## 2. 安装 Hexo 框架

打开终端（Command Prompt 或 PowerShell），运行以下命令全局安装 Hexo CLI：

```bash
npm install -g hexo-cli
```

安装完成后，可使用以下命令验证是否安装成功：

```bash
hexo -v
```

---

## 3. 初始化博客目录

在电脑上选择一个用于存放博客源文件的目录（例如：`D:\MyBlog`），在此目录下打开终端执行：

```bash
# 初始化博客，hexo-blog 为你的博客文件夹名称
hexo init hexo-blog

# 进入博客目录
cd hexo-blog

# 安装依赖
npm install
```

**初始目录结构说明：**
- `_config.yml`：**站点配置文件**（控制整个网站的标题、作者、语言、路径、部署等）。
- `package.json`：应用程序的信息及所需的各种依赖包。
- `scaffolds/`：模版文件夹（新建文章时会以此为模板）。
- `source/`：资源文件夹（存放你的 markdown 文章、图片等源文件）。
  - `source/_posts`：存放文章。
- `themes/`：主题文件夹（存放博客主题，若通过 npm 安装主题则此文件夹下可能无明显文件）。

---

## 4. 安装与配置 Butterfly 主题

Butterfly 主题是 Hexo 最受欢迎、功能最丰富的响应式主题之一。推荐通过 npm 方式安装，这样更便于后续升级。

### 步骤 A：安装主题及必要渲染器

在博客根目录下（`hexo-blog`）执行以下命令：

```bash
# 安装 Butterfly 主题
npm i hexo-theme-butterfly

# 安装 Butterfly 所必需的 Pug 和 Stylus 渲染器
npm i hexo-renderer-pug hexo-renderer-stylus --save
```

### 步骤 B：在站点配置中启用主题

打开博客根目录下的 **`_config.yml`**（站点配置文件），找到 `theme` 字段，将其修改为 `butterfly`：

```yaml
theme: butterfly
```

### 步骤 C：创建主题配置文件

为了避免在升级主题时覆盖你的个性化配置，Butterfly 推荐使用 Hexo 的 **重写机制**：
1. 在博客根目录下新建一个名为 **`_config.butterfly.yml`** 的文件。
2. 建议前往 [Butterfly 官方文档](https://butterfly.js.org/) 或 GitHub 仓库，下载或复制最新的 `_config.yml` 完整内容到你新建的 `_config.butterfly.yml` 中。
3. 以后所有的主题样式、菜单、侧边栏、社交链接、评论系统等配置，都直接在 **`_config.butterfly.yml`** 中进行修改。

---

## 5. Hexo 基本命令与日常写作

### 5.1 日常开发命令

在博客根目录下，最常用的命令组合：

*   **本地预览**（清理缓存、生成静态文件、启动本地服务）：
    ```bash
    hexo clean && hexo g && hexo s
    ```
    运行后，可在浏览器中打开 `http://localhost:4000` 实时预览博客。

*   **其他独立命令**：
    *   `hexo clean`：清除缓存文件 (`db.json`) 和已生成的静态网页文件夹 (`public/`)。
    *   `hexo generate` (简写 `hexo g`)：生成静态文件。
    *   `hexo server` (简写 `hexo s`)：启动本地预览服务器。

### 5.2 撰写新文章

使用以下命令创建一篇新文章：

```bash
hexo new post "我的第一篇博客"
```

该命令会在 `source/_posts/` 目录下生成一个名为 `我的第一篇博客.md` 的 Markdown 文件。

打开该文件，你会看到顶部的 Front-Matter（前置信息）配置，例如：

```markdown
---
title: 我的第一篇博客
date: 2026-06-25 10:00:00
tags:
  - 生活
  - 学习
categories:
  - 碎碎念
---

这里开始写你的正文内容（支持标准 Markdown 语法）...
```

---

## 6. 博客部署（以 GitHub Pages 为例）

将博客部署到 GitHub Pages，使其可以通过互联网访问：

### 步骤 A：创建 GitHub 仓库
1. 登录 GitHub。
2. 创建一个名为 `<你的用户名>.github.io` 的**公开(Public)**仓库（例如：如果你的用户名是 `john`，仓库名必须是 `john.github.io`）。

### 步骤 B：安装 Git 部署插件
在博客根目录下运行：

```bash
npm install hexo-deployer-git --save
```

### 步骤 C：配置站点 `_config.yml`
打开博客根目录下的 **`_config.yml`**，拉到最底部，修改 `deploy` 配置（请替换为你的实际仓库地址）：

```yaml
deploy:
  type: git
  repo: git@github.com:你的GitHub用户名/你的GitHub用户名.github.io.git  # 或 HTTPS 链接
  branch: main  # 或者 master
```

### 步骤 D：一键部署
执行以下命令，一键构建并推送到 GitHub 仓库：

```bash
hexo clean && hexo g -d
```

推送成功后，即可通过 `https://你的GitHub用户名.github.io` 访问你的个人静态博客！

---

## 7. Butterfly 主题进阶配置推荐

在 `_config.butterfly.yml` 中，你可以轻松开启以下常用功能：

1.  **导航栏菜单 (menu)**：配置主页、归档、标签、分类等页面的路径。
2.  **代码高亮 (highlight/prismjs)**：在 `_config.yml` 中配置代码块主题，使代码段更加美观。
3.  **社交图标 (social)**：配置置顶栏或侧边栏的 GitHub、知乎、微博等社交媒体链接。
4.  **打赏功能 (reward)**：支持配置支付宝、微信等收款二维码。
5.  **评论系统 (comments)**：支持接入 Valine, Gitalk, Twikoo, Artalk, Giscus 等多种流行评论系统。
6.  **搜索功能 (local_search)**：安装 `hexo-generator-search` 插件后，可开启丝滑的站内本地搜索。

---

*祝您建站顺利！如有疑问，可随时翻阅 [Hexo 官方文档](https://hexo.io/zh-cn/) 与 [Butterfly 主题官方文档](https://butterfly.js.org/)。*
