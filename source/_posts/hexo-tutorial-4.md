---
title: HEXO-教程-4|部署
date: 2026-07-25 10:22:33
tags:
    - hexo
categories:
    - Tutorial
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
`Part IV`
{% endnote  %}

本文将要介绍如何将你的 HEXO 博客部署到远程服务器上，使其可以被访问。

<!-- more -->

# 部署前准备

在正式部署之前，先确认本地博客可以正常生成静态文件：

```bash
hexo clean
hexo g
hexo s
```

如果本地预览没有问题，再继续后面的部署步骤。

{% note tip %}
部署的本质其实就是把 Hexo 生成出来的 `public` 目录发布到一个可以被外网访问的静态站点上。
{% endnote %}

# hexo d 部署到 GitHub Pages

这是最经典的 Hexo 部署方式。你只需要在本地执行一次命令，就能把生成后的静态文件推送到 GitHub Pages。

## 安装部署插件

首先安装 Hexo 的 Git 部署插件：

```bash
npm install hexo-deployer-git --save
```

## 配置站点的 deploy 信息

在站点根目录的 `_config.yml` 中加入或修改以下内容：

```yaml
url: https://username.github.io
deploy:
    type: git
    repo: https://github.com/username/username.github.io.git
    branch: gh-pages
```

{% note warning 注意 %}
这里的 `username` 要替换成你的 GitHub 用户名。

如果你的仓库名不是 `username.github.io`，而是普通项目仓库，那么 `url` 也要改成对应的项目地址，例如 `https://username.github.io/project-name/`。
{% endnote %}

## 执行部署

完成配置后，执行以下命令：

```bash
hexo clean
hexo g
hexo d
```

第一次执行时，可能会提示输入 GitHub 用户名、邮箱，或者需要你登录授权。完成后，Hexo 会把生成的静态文件推送到 `gh-pages` 分支。

## 在 GitHub Pages 中开启站点

打开 GitHub 仓库的设置页面，找到 Pages 相关配置，把发布源改为：

- Branch: `gh-pages`
- Folder: `/ (root)`

保存后，GitHub 会自动生成一个可访问的站点地址。

{% note info %}
如果你使用的是用户主页仓库，也就是 `username.github.io` 这种命名方式，站点地址通常就是 `https://username.github.io`。
{% endnote %}

# 使用 GitHub Actions 自动部署

如果你不想每次都在本地执行 `hexo d`，可以把部署流程交给 GitHub Actions。这样只要你把文章推送到仓库，GitHub 就会自动构建并发布站点。

## 准备仓库

通常做法是：

- `main` 分支保存 Hexo 源码
- `gh-pages` 分支保存生成后的静态站点

这样源码和发布结果分开管理，结构会更清晰。

## 添加工作流文件

在仓库中创建 `.github/workflows/pages.yml`，内容可以参考下面的示例：

```yaml
name: Deploy

on:
    push:
        branches:
            - main
    workflow_dispatch:

permissions:
    contents: write

jobs:
    build-and-deploy:
        runs-on: ubuntu-latest

        steps:
            - name: Checkout
                uses: actions/checkout@v4
                with:
                    submodules: recursive

            - name: Setup Node.js
                uses: actions/setup-node@v4
                with:
                    node-version: 20
                    cache: npm

            - name: Install dependencies
                run: npm ci

            - name: Build site
                run: npm run build

            - name: Deploy to GitHub Pages
                uses: peaceiris/actions-gh-pages@v4
                with:
                    github_token: ${{ secrets.GITHUB_TOKEN }}
                    publish_dir: ./public
                    publish_branch: gh-pages
```

{% note info %}
如果你使用的是 pnpm 或 yarn，只需要把安装命令改成对应的包管理器命令即可。
{% endnote %}

## 配置 GitHub Pages

进入仓库的 Settings -> Pages，把发布来源设置为 `gh-pages` 分支。

之后每次你向 `main` 分支提交内容，GitHub Actions 就会自动完成构建和部署。

## 这种方式的优点

GitHub Actions 的优点很明显：

- 不依赖本地环境
- 提交代码即可自动部署
- 适合团队协作
- 出问题时更容易追踪构建日志

# 部署到 Netlify

Netlify 是部署 Hexo 静态站点的另一个常用选择，配置很简单，而且自带预览环境和持续部署能力。

## 连接仓库

登录 Netlify 后，选择从 Git 仓库导入项目，连接你的 GitHub 仓库。

{% note info %}
一般来说，之后只要一直点继续就可以完成导入和部署。
如果没有成功，那么可以按照接下来的步骤手动设置。
{% endnote %}

## 设置构建参数

对于 Hexo 项目，一般填写如下：

- Build command: `npm run build`
- Publish directory: `public`

## 适合什么场景

Netlify 比较适合以下情况：

- 想快速上线静态博客
- 希望自动生成预览链接
- 不想手动管理 GitHub Pages 的发布分支

{% note warning %}
如果你的网站依赖非常特殊的自定义重写规则，记得在 Netlify 里额外配置重定向文件；不过 Hexo 博客通常不需要复杂配置。
{% endnote %}

# 部署到 Vercel

Vercel 也可以很好地托管 Hexo 站点。对于静态博客来说，它的配置同样非常直接。

## 导入仓库

在 Vercel 中选择 Import Project，然后连接 GitHub 仓库。

{% note info %}
一般来说，之后只要一直点继续就可以完成导入和部署。
如果没有成功，那么可以按照接下来的步骤手动设置。
{% endnote %}

## 设置构建命令和输出目录

建议填写：

- Build Command: `npm run build`
- Output Directory: `public`

如果 Vercel 没有自动识别项目类型，也可以手动选择 Other。

## 这种方式的优点

Vercel 的优点主要是：

- 部署速度快
- 自动预览分支提交
- 控制台界面清晰
- 适合个人博客和静态展示站

上一篇教程：[HEXO-教程-3|文章小技巧](/2026/07/23/hexo-tutorial-3/)