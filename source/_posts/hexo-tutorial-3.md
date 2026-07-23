---
title: HEXO-教程-3|文章小技巧
date: 2026-07-23 22:32:55
tags:
    - hexo
categories:
    - Tutorial
comments: false
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
`Part III`
{% endnote  %}

本文将要介绍 HEXO 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能。

<!-- more -->

# Markdown

由于 Markdown 是非常基础的知识，这里不再赘述。你可以上网搜索相关的 Markdown 教程。

# 文章描述/缩略

其实 ParticleXF 主题是没有自动缩略的，也就是说，如果你没有加额外的限制，那么首页的文章列表将会显示整篇文章的内容。

添加描述/缩略有两种方式：

## description 字段

在文章的 front-matter 中添加 `description` 字段，用于设置文章的描述。内容支持 Markdown 格式的内容。

```yaml
---
description: 这是一篇关于 HEXO 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能的教程。
---
```

{% note warning 注意 %}
description字段内如果要使用Markdown，有以下注意事项：
1. 不要使用 `---`，否则会被 Hexo 解析为 front-matter 的结束标记
2. 最好不要写多行内容
3. 如果开头是代码块，要在`description:` 后面写 `|`，否则会报错

```yaml
---
description: |
    这是一篇关于 `HEXO` 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能的教程。
---
```
{% endnote %}

## more 标签

`<!-- more -->` 可以让文章在首页只显示 `<!-- more -->` 之前的内容，`<!-- more -->` 之后的内容将会在文章详情页显示。

# 评论与TOC

在 `front-matter` 中添加 `toc` 和 `comments` 字段，用于设置文章是否显示目录和评论。

{% note tip 提示 %}
`comments` 字段在 about 页面也是可用的。
{% endnote %}

```yaml
---
toc: false
comments: false
---
```