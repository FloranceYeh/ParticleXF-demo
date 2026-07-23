---
title: HEXO-教程-1
date: 2026-07-23 20:30:30
tags:
    - hexo
categories:
    - Tutorial
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
{% endnote  %}

<!-- more -->

{% note info HEXO %}
[HEXO](https://hexo.io/zh-cn/)是一个快速、简洁且高效的博客框架，基于 Node.js 构建。它可以将 Markdown 文件转换为静态网页，并支持多种主题和插件，使得搭建个人博客变得非常容易。
{% endnote  %}

# 安装 Node.js 与 Git

## Node.js

在安装Hexo之前，你需要先安装Node.js。你可以从[Node.js官网](https://nodejs.org/)下载并安装最新的LTS版本。安装完成后，你可以在终端中运行以下命令来验证安装是否成功：

```bash
node -v
npm -v
```

## Git

Git 是一个分布式版本控制系统，用于管理代码和文件的版本。你可以从[Git官网](https://git-scm.com/)下载并安装Git。安装完成后，你可以在终端中运行以下命令来验证安装是否成功：

{% note info Gits %}
使用`Git`可以方便地管理你的博客源代码、HEXO主题和插件，还有很多方便之处。
{% endnote %}

```bash
git --version
```

# 安装 Hexo

新建一个文件夹作为你的博客目录，然后在终端中进入该目录，运行以下命令来安装Hexo：

```bash
npm install -g hexo-cli
```

随后，运行以下命令来初始化Hexo（`my-blog`是你的博客目录名，你可以根据自己的需要修改它）：

```bash
hexo init my-blog
cd my-blog
npm install
```

# Hexo 的一些常用命令

`hexo clean` \ `hexo cl`：清理缓存和生成的文件。
`hexo generate` \ `hexo g`：生成静态文件。
`hexo server` \ `hexo s`：启动本地服务器，默认端口为4000，可以使用 `--debug` 参数以调试模式启动。
`hexo new <filename>`：创建新文章，`<filename>`是文章的文件名。
`hexo new page <pagename>`：创建新页面，`<pagename>`是页面的文件名。

# 结语

至此，你已经成功安装了Hexo，并了解了一些常用的命令。接下来，你可以选择一个喜欢的主题，安装并配置它，然后开始撰写你的博客文章。祝你在搭建个人博客的过程中玩得开心！

{% note quote HEXO  %}
快速、简洁且高效的博客框架
{% endnote  %}

下一篇教程：[HEXO-教程-2](https://particlexf-demo.netlify.app/2026/07/23/hexo-tutorial-2/)